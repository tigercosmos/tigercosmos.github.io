---
title: 簡明 CGI 原理與實作
date: 2020-01-24 15:01:00
tags: [CGI, web, Boost, socket]
---

## CGI 介紹

Common Gateway Interface, CGI 讓伺服器(Server)將路由(Route)轉給轉外部程式(CGI 程式)，使外部程式可以直接和客戶端(通常為瀏覽器) 互動。在 WEB 剛興起的時候，主要還是處於靜態伺服階段，單純傳送檔案或文字資訊而已。如果想要有表單之類的互動，也就是動態網站的話，就要靠呼叫外部程式來幫忙。隨著網路科技的發達，CGI 至今仁廣泛使用，像是 PHP 搭配 Apache。不過同時也有其他架構興起，例如以 Python、NodeJS、PHP、Java 等語言為基礎的網頁框架，像是 Flask 或 Express，抑或著實現前後端分離的 RESTful API 架構。

<!-- more --> 
CGI 基本原理是，瀏覽器傳送請求(Request)給伺服器，伺服器以環境變數的方式將使用者傳送的資料傳給「外部可執行程式」，讓外部程式根據這些資訊來執行，並將結果傳回給伺服器，伺服器再將結果傳回給瀏覽器。也就是說，伺服器將工作打包給外部程式做，做完之後得到結果送回給客戶端，所以才叫做 Gateway，因為伺服器只負責指派任務。其中外部程式會以 STDIN 和 STDOUT 的方式接收資料和回傳資料給伺服器。

架構圖如下：

<pre><code>
 +--------+    HTTP        +--------+     ENV        +---------+
 |        |    Request     |        |     STDIN      |         |
 |        | +------------> |        | +------------> |         |
 |        |                |        |                | CGI     |
 | Client |                | Server |                | Program |
 |        |                |        |                |         |
 |        | <------------+ |        | <------------+ |         |
 |        |    HTTP        |        |     STDOUT     |         |
 +--------+    Response    +--------+                +---------+
</pre></code> 

詳細的規範定義在 [RFC 3875: The Common Gateway Interface (CGI) Version 1.1](https://tools.ietf.org/html/rfc3875)，有興趣的人可以翻來看看。

## 示例

接著我們要來實現簡單的 CGI 程式。本文的範例程式碼放在 Github 上[(連結)](https://github.com/tigercosmos/cgi_demo)，請 clone 下來玩玩看。

操作這個 DEMO 首先要 clone 專案，然後編譯它：

<pre><code class="shell">$ git clone https://github.com/tigercosmos/cgi_demo
$ cd cgi_demo
$ make
$ ./server 8880
</pre></code>

接著用瀏覽器打開 http://localhost:8880/print_env.cgi?a=1

![CGI 視窗](https://user-images.githubusercontent.com/18013815/73074976-c4547380-3ef5-11ea-9ae9-c3d4514579fe.png)

## 說明

首先，我們要建立 Web 伺服器，原則上你可以用任何語言來實現。這邊我用 Boost Asio 實現簡單的 TCP Server，你可能需要看一下 Boost 教學來搞懂在幹嘛，但如果你之前寫過其他語言的伺服器，其實本質是很像的。

其中 `server.cpp` 的 34-43 行，其實就是接受 HTTP request：

<pre><code class="c++">// server.cpp line 34

socket_.async_read_some(
    boost::asio::buffer(data_, max_length),
    [this, self](boost::system::error_code ec, std::size_t length) {
      sscanf(data_, "%s %s %s %s %s", REQUEST_METHOD, REQUEST_URI,
              SERVER_PROTOCOL, blackhole, HTTP_HOST);

      if (!ec) {
        do_write(length);
      }
    });
</pre></code>

當你用瀏覽器連上 `localhost:8880/print_env.cgi?a=1` 的時候，會看到 `data_` 印出這樣的訊息：

<pre><code class="log">GET /print_env.cgi?a=1 HTTP/1.1
Host: 140.113.193.198:8880
Connection: keep-alive
Cache-Control: max-age=0
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-TW,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-CN;q=0.6
</pre></code>

這是 HTTP 協定的標頭檔，我們需要取出裡面資訊，然後設成環境變數給外部程式。

其中第一行的 `GET` 是 HTTP method，`/print_env.cgi?a=1` 是 URI，`HTTP/1.1` 是協定。下面掠過不介紹，總之就是 HTTP 請求的各種參數。

我們為了實現簡單 CGI 程式，需要解析 URI 並設成環境變數給外部程式。現在我們知道那麼 URI 是 `/printenv.cgi?a=1`。我們可以進一步去拆解，得知我們的外部程式是 `printenv.cgi`，並且 Query 是 `a=1`。Query 是外部程式可能要用到的參數，為了讓外部成是可以吃到，我們可以設環境變數 `setenv("QUERY_STRING", "a=1", 1)`，並在外部程式中 `getenv("QUERY_STRING")` 來取得所需要的參數。

接著可以看到 `server.cpp` 的 94-109 行，將 socket 取代成外部程式(`EXEC_FILE`)的 `stdin`、`stdout` 和 `stderr`。也就是說，外部程式會直接吃 socket 的 input 和直接輸出給 socket。

<pre><code class="c++">// server.cpp line 94

global_io_service.notify_fork(io_service::fork_prepare);
if (fork() != 0) {
  global_io_service.notify_fork(io_service::fork_parent);
  socket_.close();
} else {
  global_io_service.notify_fork(io_service::fork_child);
  int sock = socket_.native_handle();
  dup2(sock, STDERR_FILENO);
  dup2(sock, STDIN_FILENO);
  dup2(sock, STDOUT_FILENO);
  socket_.close();

  if (execlp(EXEC_FILE, EXEC_FILE, NULL) < 0) {
    std::cout << "Content-type:text/html\r\n\r\n FAIL";
  }
}
</pre></code>

這邊我們假設 `EXEC_FILE` 必定是 CGI 程式，並沒有去特別處理，但如果是一個完整的伺服器，例如 Apache，就會去檢查程式是否有符合 CGI Spec 以及 URI 是否為 `.cgi` 結尾等等。

這時當瀏覽器打開 http://localhost:8880/print_env.cgi?a=1 的時候，伺服器取得 HTTP 請求，於是 `fork()` 出新的 porcess 並 `exec()` 執行 `./print_env.cgi`，同時 Query `a=1` 也會經由環境變數傳給 `./print_env.cgi`。

在 `print_env.cgi.cpp` 檔案中，`int main(int, char* const[], char* const envp[])` 中的 `envp[]` 取得環境變數，並經由 `for (int i = 0; envp[i]; ++i) { cout << envp[i] << endl; }` 印出。

當然，這只是示範，真實應用場景，可能是一個 form action，所有欄位都存在 Query 中傳給伺服器，CGI 程式由環境變數取得表單資料，然後操作資料庫，然後呈現處理後的數據。
