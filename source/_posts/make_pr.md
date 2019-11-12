---
title: 我都怎麼發 PR？
date: 2017-11-11 00:00:00
tags: [Chinese Posts,English Posts,Open Source,開源,Servo,Chinese,]
---


## 我都怎麼發 PR？

開源專案中，如何找出問題，並解決他？

<img class="dz t u gw ak" src="https://miro.medium.com/max/1920/0*1MIgNKX6H7wFYTGp.jpg" role="presentation"><br/>

開源專案的流程很簡單，看 issue 有甚麼，然後改 code，接著發 pull request，順利的話就會被 merge，成為一個 commit。開源，就是一直重複這些步驟。

發 issue 很簡單，你哪邊看不爽，不管是 bug、feature、doc、style，就可以發個 issue。當然發 PR 也很簡單，但能被 merge 的 PR 就不簡單。所以如何寫點新東西或是修正 bug，然後發 PR 最後被 merge 進去？

<!-- more --> 

參加開源專案最困難的地方，便是一開始不知道整個架構，不熟悉自然也就難。但經過初期的陣痛期，大概對一個專案的內容也 87% 了解了。例如某個模組和某個模組是相輔相成，某個單元測是要參考哪個公定標準，這些都是經驗。這些新手一定不了解，所以要勇敢問。

懂了之後，要發 PR 也不是那麼難，尤其大專案更是容易。撇除大專案本身有一堆 issues 可以去解決，其實開發過程或是隨便瀏覽 code 都可以看到一些問題，就可以自己提出問題然後解決他。以下談的是我個人一些經驗，有些會先發 issue 和別人討論，有些比較有把握的就會直接發 PR。

以 <a href="https://github.com/servo/servo" class="dj by hl hm hn ho" target="_blank" rel="noopener nofollow">Servo</a> 為例，編譯前的事先準備工作就不少，如果漏掉或弄錯一些步驟，就會編譯不成功，常常我建置一個新環境就會搞錯，甚至如果一個新手新加進來，一定會有很大機會出錯，所以自動化流程的除錯友善程度，就是一個可以改進的點。Servo 是一個跨平台的平行化瀏覽器引擎，我一開始是改善 Windows 編譯，後來也讓 Android 的編譯都有讓偵錯變得更好。有時候就是一念之差吧，我猜很多人也有被雷到過，但就沒有想要發 PR 讓他變更完整。

此外在大專案中，搜尋所有程式碼中的 <code class="ha hp hq hr hs b">TODO</code> ，基本上可以看到一堆，因為專案本身很大，很多功能都只先完成部分就先上線，但日後勢必要把它完成的。這種未完成的部分，有時候會被別人當作 issue 提出來，但數量太多了，可能就擺著。我會看看哪寫是我感興趣的，然後這時候會自己發個 issue，算是聲明自己要開始做這個，然後把 <code class="ha hp hq hr hs b">TODO</code> 完成掉，再發 PR。也可以先弄個部分，先發 PR，然後標題註明 WIP ( work in process)，這樣就不用發 issue，不過通常大家會直接搜尋 issue，有一定風險(要賭你的PR比較快被 merge )。但通常要解決的東西太多，自己想到的東西，幾乎不會跟別人撞到。

還有一種是漫無目的的瀏覽 code，我不知道一般人會不會這樣，但我為了更熟悉整個專案，就會仔細看 code 的內容。通常會被我發現一些邏輯問題或是多餘的程式碼。例如，某個模組是處理 Linux 平台，裡面卻有些 Windows 平台的東西，大概就是移植的時候沒有處理好，不小心遺留之類的，就可以把那些程式碼拿掉。

或是像是：

<pre><span id="4be7" class="hv hw em at hs b fd hx hy r hz">fn overflow_x_is_visible(&amp;self) -&gt; bool {<br>  ....<br>  overflow_pair.x == overflow_x::computed_value::T::visible<br>}</span><span id="f74f" class="hv hw em at hs b fd ia ib ic id ie hy r hz">fn overflow_y_is_visible(&amp;self) -&gt; bool {<br>  ....<br>  overflow_pair.y != overflow_y::computed_value::T::visible<br>}</span></pre>

x 和 y 是一組，所以一般而言應該要邏輯一樣。就可以很清楚察覺，x 和 y 的邏輯不一樣是錯的。

總之，在看 code 的時候多想一下她在幹嘛，順著 code 的思維走，如果 code 有問題的話，應該會馬上覺得怪怪的，那大概就是一個 bug！簡單來說，大概可以算是在練習找碴能力吧。

除了以上的方式，還可以修正文件檔案，當然也可以自己寫新的功能、模組。參加開源的過程，就是在練習自己的邏輯能力，同時藉由別人的足跡增進自己的程式技巧，並且也可以訓練溝通能力。學會如何找問題，發 PR 就是信手拈來，要成為核心貢獻者指日可待！