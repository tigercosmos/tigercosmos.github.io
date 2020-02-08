---
title: JavaScript 平行化使用 Web Worker、SharedArrayBuffer、Atomics
date: 2020-02-07 15:01:00
tags: [JavaScript, web, Web Worker, SharedArrayBuffer]
---

JavaScript 是執行時只會用單執行緒，即便 JavaScript 大量使用並行（Concurrency）機制，像是各種 Event Handler，依舊還是只有一個執行緒，於是這樣大大限制計算的效能。解套辦法是在 JavaScript 上撰寫平行程式，使用 [Web Worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)、 [SharedArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer)和 [Atomics](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics)。

Web Worker 讓你這個網頁可以開啟其他執行緒來做事，但因為每個 Worker 彼此資料是獨立的，想要共用的話還需要搭配 `SharedArrayBuffer` 共享記憶體，並透過 `Atomics` 來確保資料正確。本文先介紹 Web Worker，然後分別介紹 `SharedArrayBuffer` 和 `Atomics`，最後演示如何結合使用。

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

Worker 和 Worker 之間是彼此不能溝通的，但我們可以使用 `MessageChannel` 來解套：

```js
const channel = new MessageChannel();
receivingWorker.postMessage({port: channel.port1}, [channel.port1]);
sendingWorker.postMessage({port: channel.port2}, [channel.port2]);
```

`MessageChannel` 的 `port1` 和 `port2` 皆為雙向管道，所以可以用 `onmessage` 和 `postMessage`，詳細範例可以參考「[Using channel messaging](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API/Using_channel_messaging)」。

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

## 2. SharedArrayBuffer

### 2.1 簡介

前面提到 Worker 的資料是獨立的，不管是透過深度拷貝或是轉移所有權，資料都不能和主程序或其他 Worker 共用。當然可以透過消息通知傳資料，但當資料很大時就顯的不切實際，因此當我們要寫平行程式時，共享資料成為必然。[SharedArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) 因應而生。

### 2.2 用法

以下為 `SharedArrayBuffer` 使用示例。

#### 2.2.1 Master 端

```js
// main.js

const worker = new Worker('worker.js');

// 要分享的 SharedArrayBuffer
const sharedBuffer = new SharedArrayBuffer( // (A)
    10 * Int32Array.BYTES_PER_ELEMENT); // 10 個 int

// 分享給 Worker
worker.postMessage(sharedBuffer); // (B)

// 本地端使用
const sharedArray = new Int32Array(sharedBuffer); // (C)
```

`(A)` 生成 `SharedArrayBuffer`，初始化要宣告要多大的 Buffer。

`(B)` 將 `sharedBuffer` 採用[結構複製（Structured Clone）](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm)給 Worker，意思是 Worker 也會生出一個新的 `SharedArrayBuffer` 物件，被底層機制會讓他們映射到同一塊記憶體區間，可以想成就是傳址。

`(C)` 將 Buffer 轉為 Array 建立 `sharedArray` 本地端變數，這樣我們才可以操作元素，元素變動會直接改到共享的記憶體。

#### 2.2.2 Worker 端

```js
// worker.js

addEventListener('message', function (event) {
  const sharedBuffer = event.data;
  const sharedArray = new Int32Array(sharedBuffer); // (D)
});
```

Worker 可以從 `(B)` 取得資料，於 `(D)` 將 Buffer 轉換成可操作的 Array。此時 `(C)` 和 `(D)` 都可以修改 `SharedArrayBuffer` 的記憶體。

## 3. Atomics

### 3.1 簡介

前面說到可以共用記憶體，但當主程序和 Worker 都可以存取同一塊記憶體時，就容易發生數據競爭（Data Racing），所以我們需要上鎖機制，而 `Atomics` 為 JavaScript 提供原子性操作，使用 `Atomics` 可以確保資料安全寫入，不會產生競爭，一些更高階的上鎖機制如 Mutex，也是基於 `Atomics` 來實現。`Atomics` 本身只提供 Static 方法，類似 `Math` 那樣。

### 3.2 用法

#### 3.2.1 資料同步

Busy Waiting 的範例：

```js
// main.js
console.log('notifying...');
Atomics.store(sharedArray, 0, 1);

// worker.js
while (Atomics.load(sharedArray, 0) !== 1) ;
console.log('notified');
```

### 3.2.2 等待通知

這邊介紹 `Atomics.wait()` 和 `Atomics.notify()` 用法。

```js
// main.js
const worker = new Worker('./worker.js');

const sab = new SharedArrayBuffer(1024);
worker.postMessage(sab); // `SharedArrayBuffer` 物件傳給 Worker。

const int32 = new Int32Array(sab);
console.log("master before notify", int32[0]); // 0;
Atomics.store(int32, 0, 123); // 改變共用元素
Atomics.notify(int32, 0, true); // (A)
```

`(A)` 這邊用 `Atomics.notify` 去告知 `int32` 的第 `0` 個元素值有變化，故傳 `true` 去通知。

```js
// worker.js

addEventListener('message', function (event) {
  const sharedBuffer = event.data;
  const int32 = new Int32Array(sharedBuffer);
 
  Atomics.wait(int32, 0, false); // (B)
  console.log("worker after waiting", int32[0]); // 123
});
```

`(B)` 這邊用 `Atomics.wait` 去監聽 `int32` 的第 `0` 個元素值有沒有變化，監聽方式是看 `notify` 傳進來的值有沒有和第三個數不一樣。因為第三個參數設為 `false`，故當 `notify` 傳 `true` 來時，`Atomics` 知道有變動了，於是繼續執行。

## 4. 平行程式

## 5. 參考資料

- [Web Worker 使用教程](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)
- [Using Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
- [ES proposal: Shared memory and atomics](https://2ality.com/2017/01/shared-array-buffer.html#sharing-data-other-than-integers)
- [Shared memory - a brief tutorial](https://github.com/tc39/ecmascript_sharedmem/blob/master/TUTORIAL.md)
- [Communicating between Web Workers via MessageChannel](https://2ality.com/2017/01/messagechannel.html)
- [MDN: SharedArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer)
- [MDN: Atomics](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics)
- [Shared memory parallel programming](https://apiacoa.org/teaching/big-data/smp.en.html)
