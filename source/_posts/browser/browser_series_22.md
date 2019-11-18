---
title: 瀏覽器的安全連線（HTTPS）與實作
date: 2018-01-02 23:36:20
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
<h2>&#x524D;&#x8A00;</h2>
<p>&#x4ECA;&#x5929;&#x4F86;&#x8AC7;&#x8AC7;&#x700F;&#x89BD;&#x5668;&#x7684;&#x5B89;&#x5168;&#x6027;&#x9023;&#x7DDA;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x8B1B;&#x8B1B; HTTPS &#x662F;&#x751A;&#x9EBC;&#x4EE5;&#x53CA;&#x600E;&#x9EBC;&#x505A;&#xFF1F;<br>
&#x8001;&#x6A23;&#x5B50;&#x6211;&#x5011;&#x53C8;&#x56DE;&#x5230;&#x8B1B;&#x89E3; <a href="https://github.com/servo/servo" target="_blank">Servo</a> &#x7684;&#x6642;&#x5019;&#x56C9;&#xFF5E;</p>
<h2>What?</h2>
<p>&#x76F8;&#x4FE1;&#x5927;&#x5BB6;&#x700F;&#x89BD;&#x7DB2;&#x7AD9;&#x7684;&#x6642;&#x5019;&#x5E38;&#x5E38;&#x6703;&#x770B;&#x5230;&#x300C;&#x7DA0;&#x8272;&#x7684;?&#x300D;&#xFF0C;&#x9EDE;&#x64CA;&#x4E00;&#x4E0B;&#x4ED6;&#x6703;&#x544A;&#x8A34;&#x4F60;&#x662F;&#x5B89;&#x5168;&#x9023;&#x7DDA;<br>
<img src="https://user-images.githubusercontent.com/18013815/34487501-8bf635d2-f00f-11e7-83d8-1fbeeedb1c5d.png" alt><br>
&#x4EE5; Firefox &#x4F86;&#x8AAA;&#x5B83;&#x5C31;&#x6703;&#x544A;&#x8A34;&#x4F60;&#xFF1A;</p>
<blockquote>
<p>&#x7576; Firefox &#x9023;&#x7DDA;&#x5230;&#x4E00;&#x500B;&#x4F7F;&#x7528;&#x5B89;&#x5168;&#x9023;&#x7DDA;&#x7684;&#x7DB2;&#x7AD9;&#xFF08;&#x7DB2;&#x5740;&#x4EE5; &quot;<a href="https://%22" target="_blank">https://&quot;</a> &#x958B;&#x982D;&#xFF09;&#x6642;&#xFF0C;Firefox &#x6703;&#x6AA2;&#x9A57;&#x7DB2;&#x7AD9;&#x6191;&#x8B49;&#x7684;&#x6B63;&#x78BA;&#x6027;&#x4EE5;&#x53CA;&#x9023;&#x7DDA;&#x7684;&#x52A0;&#x5BC6;&#x5F37;&#x5EA6;&#x4EE5;&#x78BA;&#x4FDD;&#x60A8;&#x7684;&#x96B1;&#x79C1;&#x3002;&#x5982;&#x679C;&#x6191;&#x8B49;&#x7121;&#x6CD5;&#x88AB;&#x9A57;&#x8B49;&#xFF0C;&#x6216;&#x9023;&#x7DDA;&#x4F7F;&#x7528;&#x4E86;&#x4E0D;&#x5920;&#x5F37;&#x7684;&#x52A0;&#x5BC6;&#x6F14;&#x7B97;&#x6CD5;&#xFF0C;Firefox &#x6703;&#x4E2D;&#x65B7;&#x8207;&#x7DB2;&#x7AD9;&#x7684;&#x9023;&#x7DDA;</p>
</blockquote>
<p>&#x60F3;&#x66B8;&#x89E3; HTTPS &#x66F4;&#x591A;&#x7684;&#x8A71;&#x53EF;&#x4EE5;&#x770B; <a href="https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%AE%89%E5%85%A8%E5%8D%8F%E8%AE%AE" target="_blank">&#x7DAD;&#x57FA;&#x767E;&#x79D1;</a> &#x548C; <a href="https://ithelp.ithome.com.tw/articles/10000019" target="_blank">&#x9019;&#x7BC7;</a>&#x3002;&#x7919;&#x65BC;&#x7BC7;&#x5E45;&#x5C31;&#x4E0D;&#x91CD;&#x8FF0;&#x3002;</p>
<h2>How&#xFF1F;</h2>
<p>Servo &#x5728;&#x7DB2;&#x8DEF;&#x9023;&#x7DDA;&#x4E0A;&#x7684;&#x5BE6;&#x73FE;&#x90FD;&#x5728; <a href="https://github.com/servo/servo/tree/master/components/net" target="_blank"><code>servo/components/net/</code></a>&#x3002;&#x88E1;&#x9762;&#x5305;&#x542B;&#x8655;&#x7406; http&#x3001;https &#x5354;&#x5B9A;&#x3001;headers&#x3001;cookies&#x3001;resources &#x7B49;&#x7B49;&#x3002;</p>
<p>&#x800C;&#x4ECA;&#x5929;&#x7684;&#x91CD;&#x9EDE;&#x662F;&#x700F;&#x89BD;&#x5668;&#x7684;&#x5B89;&#x5168;&#x6027;&#x9023;&#x7DDA;&#xFF0C;&#x90A3;&#x9EBC;&#x91CD;&#x9EDE;&#x7576;&#x7136;&#x5C31;&#x5728; HTTPS &#x548C; SSl &#x7684;&#x9023;&#x7DDA;&#x90E8;&#x5206;&#x56C9;&#xFF01;</p>
<p>&#x76F8;&#x95DC;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#x5728; <a href="https://github.com/servo/servo/blob/master/components/net/connector.rs" target="_blank">/components/net/connector.rs</a>&#xFF0C;&#x4E26;&#x4E0D;&#x6703;&#x5F88;&#x9577;&#xFF0C;&#x5927;&#x5BB6;&#x53EF;&#x4EE5;&#x9EDE;&#x9032;&#x53BB;&#x770B;&#x770B;&#x3002;&#xFF08;&#x4EE5;&#x4E0B;&#x7684;&#x7BC4;&#x4F8B;&#x78BC;&#x6211;&#x6709;&#x628A;&#x539F;&#x59CB;&#x78BC;&#x91CD;&#x65B0;&#x6392;&#x7248;&#x904E;&#xFF09;</p>
<p>&#x9019;&#x908A;&#x7A0B;&#x5F0F;&#x7684;&#x5BE6;&#x73FE;&#x662F;&#x8655;&#x7406;&#x300C;&#x9023;&#x7DDA;&#x300D;&#xFF0C;&#x540C;&#x6642;&#x53EF;&#x4EE5;&#x61C9;&#x4ED8; HTTP &#x548C; HTTPS&#x3002;&#x800C;&#x5982;&#x679C;&#x662F; HTTPS &#x7684;&#x9023;&#x7DDA;&#x5C31;&#x7528; SSL &#x7684; Client &#x53BB;&#x5305;&#x88DD;&#x3002;</p>
<p>&#x9019;&#x908A;&#x5148;&#x5B9A;&#x7FA9;&#x9023;&#x7DDA;&#x7684;&#x7269;&#x4EF6;</p>
<pre><code>pub struct HttpsConnector {
    ssl: OpensslClient,
}

impl HttpsConnector {
    fn new(ssl: OpensslClient) -&gt; HttpsConnector {
        HttpsConnector {
            ssl: ssl,
        }
    }
}
</code></pre>
<p>&#x9019;&#x908A;&#x662F;&#x5728;&#x9023;&#x7DDA;&#x6642;&#x6C7A;&#x5B9A;&#x8981;&#x63A1;&#x7528; HTTP &#x9084;&#x662F; HTTPS &#x5354;&#x8B70;</p>
<pre><code>impl NetworkConnector for HttpsConnector {
    type Stream = HttpsStream&lt;&lt;OpensslClient as SslClient&gt;::Stream&gt;;

    fn connect(&amp;self, host: &amp;str, port: u16, scheme: &amp;str) 
        -&gt; HyperResult&lt;Self::Stream&gt;
    {
        if scheme != &quot;http&quot; &amp;&amp; scheme != &quot;https&quot; {
            return Err(HyperError::Io(
                io::Error::new(io::ErrorKind::InvalidInput,
                               &quot;Invalid scheme for Http&quot;)));
        }

        // Perform host replacement when making the actual 
        // TCP connection.
        let addr = &amp;(&amp;*replace_host(host), port);
        let stream = HttpStream(TcpStream::connect(addr)?);

        if scheme == &quot;http&quot; {
            Ok(HttpsStream::Http(stream))
        } else {
            // Do not perform host replacement on the host that is
            // used for verifying any SSL certificate encountered.
            self.ssl.wrap_client(stream, host).map(HttpsStream::Https)
        }
    }
}
</code></pre>
<p>&#x5C0D;&#x9023;&#x7DDA;&#x65B9;&#x5F0F;&#x4E0D;&#x719F;&#x7684;&#x8A71;&#xFF0C;&#x5EFA;&#x8B70;&#x628A;&#x672C;&#x6587;&#x4E00;&#x958B;&#x59CB;&#x5EFA;&#x8B70;&#x95B1;&#x8B80;&#x8CC7;&#x6599;&#x770B;&#x5B8C;&#x3002;<br>
&#x4F7F;&#x7528; SSL &#x7684;&#x6642;&#x5019;&#x6703;&#x7528;&#x5230; TLS&#xFF0C;&#x6240;&#x4EE5;&#x9019;&#x908A;&#x6709; <code>SslMethod::tls()</code>&#xFF0C;&#x6B64;&#x5916;&#x9084;&#x8981;&#x6AA2;&#x67E5;&#x6191;&#x8B49;&#xFF08;CA&#xFF09;<br>
&#x90FD;&#x6C92;&#x554F;&#x984C;&#x5C31;&#x53EF;&#x4EE5;&#x9806;&#x5229;&#x7528; SSL &#x50B3;&#x8F38;&#x56C9;&#xFF01;</p>
<pre><code>pub type Connector = HttpsConnector;

pub fn create_ssl_client(ca_file: &amp;PathBuf) -&gt; OpensslClient {
    let mut ssl_connector_builder = 
        SslConnectorBuilder::new(SslMethod::tls()).unwrap();
    {
        let context = ssl_connector_builder.builder_mut();
        context.set_ca_file(ca_file).expect(&quot;could not set CA file&quot;);
        context.set_cipher_list(DEFAULT_CIPHERS)
            .expect(&quot;could not set ciphers&quot;);
        context.set_options(
            SSL_OP_NO_SSLV2 | SSL_OP_NO_SSLV3 | SSL_OP_NO_COMPRESSION);
    }
    let ssl_connector = ssl_connector_builder.build();
    OpensslClient::from(ssl_connector)
}

pub fn create_http_connector(ssl_client: OpensslClient) 
-&gt; Pool&lt;Connector&gt; {
    let https_connector = HttpsConnector::new(ssl_client);
    Pool::with_connector(Default::default(), https_connector)
}
</code></pre>
<hr>
<p>&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x6211;&#x5011;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
<hr>
<blockquote>
<h3><em><strong>&#x95DC;&#x65BC;&#x4F5C;&#x8005;</strong></em></h3>
<h2>&#x5289;&#x5B89;&#x9F4A;</h2>
<p>&#x8EDF;&#x9AD4;&#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x71B1;&#x611B;&#x5BEB;&#x7A0B;&#x5F0F;&#xFF0C;&#x66F4;&#x559C;&#x6B61;&#x63A8;&#x5EE3;&#x7A0B;&#x5F0F;&#x8B93;&#x66F4;&#x591A;&#x4EBA;&#x5B78;&#x6703;</p>
<ul>
<li>
<a href="https://tigercosmos.github.io" target="_blank">&#x500B;&#x4EBA;&#x7DB2;&#x7AD9;</a>
</li>
<li>
<a href="https://github.com/tigercosmos" target="_blank">Github</a>
</li>
<li>
<a href="https://www.facebook.com/CodingNeutrino/" target="_blank">FB&#x7C89;&#x5C08;--&#x5FAE;&#x4E2D;&#x5B50;</a>
</li>
</ul>
</blockquote>
 <br>
                                                    </div>
                    </div>
                
