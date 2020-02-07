---
title: JavaScript 平行化使用 Web Worker 和 SharedArrayBuffer
date: 2020-02-07 15:01:00
tags: [JavaScript, web, Web Worker, SharedArrayBuffer]
---

JavaScript 是執行時只會用單執行緒，即便 JavaScript 大量使用並行（Concurrency）機制，像是各種 Event Handler，依舊還是只有一個執行緒，於是這樣大大限制計算的效能。解套辦法是在 JavaScript 上撰寫平行程式，使用 [Web Worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 和 [SharedArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer)。

Web Worker 讓你這個網頁可以開啟其他執行緒來做事，但因為每個 Worker 彼此資料是獨立的，想要共用的話還需要搭配 SharedArrayBuffer 共享記憶體。本文先介紹 Web Worker，然後介紹 SharedArrayBuffer，最後演示如何結合兩者使用。

## 1. Web Worker

### 1.1 簡介
簡單來說，呼叫一個 Worker 就是多開一條執行緒，但 Worker 有以下特性：

1. 同源限制
  Worker 使用腳本不可以是其他網站的，也不可以開啟本地端文件。
2. 作用域（Scope）限制
  每個 Worker 有屬於自己的 `window`，與 parent 彼此獨立。
3. 進程間通訊（IPC）
  Worker 採用 share-nothing 模型，必須使用 `postMessage` 和 `onmessage` 來溝通
4. 腳本限制
  不可修改 `DOM`、`document`。不可呼叫 `alert`、`confirm`。詳細規定要看 [Functions and classes available to Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Functions_and_classes_available_to_workers)。

### 1.2 用法

#### 1.2.1 主程序

Worker 是主從式（master/slave），由主程序建立 Worker：

```js
const worker = new Worker('myworker.js');
```

`myworker.js` 就是要執行的 worker 的程式碼，記住檔案必須是同源，如果取得檔案失敗（404），worker 就會默認失敗。

主程序發送消息給 Worker 的語法是：

```js
worker.postMessage(message, [transfer]);
```

其中 `message` 是要通知的訊息，可以用來區分監聽的任務，也可以用來傳物件，但是物件會是「完全拷貝」而非傳址；而 `transfer` 則是指定 `message` 中哪些物件是要直接轉移所有權（Ownership），將「[具可轉性（Transferable）](https://developer.mozilla.org/en-US/docs/Web/API/Transferable)」的物件，物件所有權從主程序變成 Worker。

例如：

```js
worker.postMessage(
  { msg: 'do_thing', buf: arrBuf }, // buf 這邊放入 arrBuf
  [ arrBuf ] // 指明 arrBuf 要轉移
);
```

主程序透過 `onmessage` 函數來接收從 Worker 傳回來的訊息：

```js
worker.onmessage = function (event) {
  console.log('Received message ' + event.data);
}
```

當 Worker 執行完畢，主程式可以將其關閉

```js
worker.terminate();
```

#### 1.2.2 Worker 緒

Worker 有兩幾種方式來監聽訊息，一種是透過 `onmessage` 方法，另一種是使用 `addEventListener` 去監聽 Event 物件，其物件的 `data` 屬性為傳過來的 `message` 內容：

```js
// myworker.js

// 法 1
onmessage = function(e) {
  postMessage('You said: ' + e.data);
}

// 法 2
addEventListener('message', function (e) {
  postMessage('You said: ' + e.data);
}, false);
```

這邊的 `e.data` 就是從主程序傳過來的 `message`。

根據主程序傳過來的數據，Worker 可以選擇要做甚麼事情，例如：

```js
addEventListener('message', function (e) {
  const cmd = e.data.cmd;
  switch (cmd) {
    case 'run':
      postMessage('WORKER RAN: ' + data.msg);
      break;
    case 'stop':
      postMessage('WORKER STOPPED: ' + data.msg);
      close(); // 關閉 worker
      break;
    default:
      postMessage('Unknown command: ' + data.msg);
  };
}, false);
```

Worker 可以透過 `close()` 來關閉自己。

Worker 可以引入其他腳本：

```js
importScripts('script1.js', 'script2.js');
```

#### 1.2.3 錯誤處理

主程式可以監聽 Worker 是否有錯，Worker 自己也可以監聽自己，語法相同：

```js
worker.onerror(function (event) {
  console.log(e.lineno, e.filename, e.message); // 行數、檔名、錯誤訊息
});

// 或者
worker.addEventListener('error', function (event) { /* */ });
```

### 1.3 進程間通訊 (IPC)

前面提到 Worker 之間通訊可以靠 message，除了物件以外還可以送各種 Binary 資料如 File、Blob、ArrayBuffer，不過都會是深度拷貝。避免拷貝可以指名哪些具可轉性物件要做所有權轉移。瀏覽器內部機制將傳送的內容序列化（Serialization），Worker 接收後再反序列化。

深度拷貝範例：

```js
// 主程序
const uInt8Array = new Uint8Array(new ArrayBuffer(10));
for (let i = 0; i < uInt8Array.length; ++i) {
  uInt8Array[i] = i * 2; // [0, 2, 4, 6, 8,...]
}
worker.postMessage(uInt8Array);

// Worker 程序
onmessage = function (e) {
  const uInt8Array = e.data; // 完全複製的 uInt8Array
};
```

深度拷貝會造成效瓶頸，轉移所有權是個好方法，通常用在影像、聲音、矩陣運算等上。Transferable 的物件有：` ArrayBuffer`、`MessagePort`、`ImageBitmap`、`OffscreenCanvas`。

轉移物件範例：

```js
var ab = new ArrayBuffer(1);
worker.postMessage(ab, [ab]);
```

### 1.4 其他

#### 1.4.1 Web worker 也可以和主程序在同一個檔案中

作法滿偷吃步：

```html
<!DOCTYPE html>
  <body>
    <script>
      // 主程序
    </script>

    <script id="worker" type="app/worker">
      addEventListener('message', function () {
        postMessage('some message');
      }, false);
    </script>
  </body>
</html>
```

注意是 Worker 的部分一定要有 `type = "app/worker"`。

主程序這樣去呼叫：

```js
const blob = new Blob([document.querySelector('#worker').textContent]); // 取得內容
const url = window.URL.createObjectURL(blob); // 假裝是從 URL 來的
const worker = new Worker(url);

worker.onmessage = function (e) { /* */ };
```

#### 1.4.2 Worker 也可以產生 Worker

Worker 也可以是其他 Worker 的 Master，關係大概就像 `fork` 的 child 也可以去做 `fork`。Worker 和他產生的 Worker，互動方式就和原本主程式之於 Worker 一樣。


## 參考資料

- [Web Worker 使用教程](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)
- [Using Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
- [Shared memory - a brief tutorial](https://github.com/tc39/ecmascript_sharedmem/blob/master/TUTORIAL.md)


https://apiacoa.org/teaching/big-data/smp.en.html
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer
https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers
ruanyifeng.com/blog/2018/07/web-worker.html
https://github.com/tc39/ecmascript_sharedmem/blob/master/TUTORIAL.md
https://2ality.com/2017/01/messagechannel.html
https://2ality.com/2017/01/shared-array-buffer.html#sharing-data-other-than-integers
https://lucasfcosta.com/2017/04/30/JavaScript-From-Workers-to-Shared-Memory.html
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics