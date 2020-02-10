---
title: 瀏覽器的安全連線（HTTPS）與實作
date: 2018-01-02 23:36:20
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
## 前言
今天來談談瀏覽器的安全性連線，也就是講講 HTTPS 是甚麼以及怎麼做？
老樣子我們又回到講解 [Servo](https://github.com/servo/servo) 的時候囉～

## What?
相信大家瀏覽網站的時候常常會看到「綠色的?」，點擊一下他會告訴你是安全連線
![](https://user-images.githubusercontent.com/18013815/34487501-8bf635d2-f00f-11e7-83d8-1fbeeedb1c5d.png)
以 Firefox 來說它就會告訴你：
> 當 Firefox 連線到一個使用安全連線的網站（網址以 "https://" 開頭）時，Firefox 會檢驗網站憑證的正確性以及連線的加密強度以確保您的隱私。如果憑證無法被驗證，或連線使用了不夠強的加密演算法，Firefox 會中斷與網站的連線

想暸解 HTTPS 更多的話可以看 [維基百科](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%AE%89%E5%85%A8%E5%8D%8F%E8%AE%AE) 和 [這篇](https://ithelp.ithome.com.tw/articles/10000019)。礙於篇幅就不重述。

## How？
Servo 在網路連線上的實現都在 [`servo/components/net/`](https://github.com/servo/servo/tree/master/components/net)。裡面包含處理 http、https 協定、headers、cookies、resources 等等。

而今天的重點是瀏覽器的安全性連線，那麼重點當然就在 HTTPS 和 SSl 的連線部分囉！

相關的程式碼在 [/components/net/connector.rs](https://github.com/servo/servo/blob/master/components/net/connector.rs)，並不會很長，大家可以點進去看看。（以下的範例碼我有把原始碼重新排版過）

這邊程式的實現是處理「連線」，同時可以應付 HTTP 和 HTTPS。而如果是 HTTPS 的連線就用 SSL 的 Client 去包裝。
 
這邊先定義連線的物件
```
pub struct HttpsConnector {
    ssl: OpensslClient,
}

impl HttpsConnector {
    fn new(ssl: OpensslClient) -> HttpsConnector {
        HttpsConnector {
            ssl: ssl,
        }
    }
}
```

這邊是在連線時決定要採用 HTTP 還是 HTTPS 協議
```
impl NetworkConnector for HttpsConnector {
    type Stream = HttpsStream<<OpensslClient as SslClient>::Stream>;

    fn connect(&self, host: &str, port: u16, scheme: &str) 
        -> HyperResult<Self::Stream>
    {
        if scheme != "http" && scheme != "https" {
            return Err(HyperError::Io(
                io::Error::new(io::ErrorKind::InvalidInput,
                               "Invalid scheme for Http")));
        }

        // Perform host replacement when making the actual 
        // TCP connection.
        let addr = &(&*replace_host(host), port);
        let stream = HttpStream(TcpStream::connect(addr)?);

        if scheme == "http" {
            Ok(HttpsStream::Http(stream))
        } else {
            // Do not perform host replacement on the host that is
            // used for verifying any SSL certificate encountered.
            self.ssl.wrap_client(stream, host).map(HttpsStream::Https)
        }
    }
}
```

對連線方式不熟的話，建議把本文一開始建議閱讀資料看完。
使用 SSL 的時候會用到 TLS，所以這邊有 `SslMethod::tls()`，此外還要檢查憑證（CA）
都沒問題就可以順利用 SSL 傳輸囉！
```
pub type Connector = HttpsConnector;

pub fn create_ssl_client(ca_file: &PathBuf) -> OpensslClient {
    let mut ssl_connector_builder = 
        SslConnectorBuilder::new(SslMethod::tls()).unwrap();
    {
        let context = ssl_connector_builder.builder_mut();
        context.set_ca_file(ca_file).expect("could not set CA file");
        context.set_cipher_list(DEFAULT_CIPHERS)
            .expect("could not set ciphers");
        context.set_options(
            SSL_OP_NO_SSLV2 | SSL_OP_NO_SSLV3 | SSL_OP_NO_COMPRESSION);
    }
    let ssl_connector = ssl_connector_builder.build();
    OpensslClient::from(ssl_connector)
}

pub fn create_http_connector(ssl_client: OpensslClient) 
-> Pool<Connector> {
    let https_connector = HttpsConnector::new(ssl_client);
    Pool::with_connector(Default::default(), https_connector)
}
```

---
希望對大家有幫助，我們明天見！
                                                        
