---
title: 為什麼手機上網速度比較慢呢？
date: 2017-12-29 23:25:55
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


## 問題：為什麼手機上網速度比較慢？
今天來點輕鬆的主題。
你有沒有想過，為什麼手機上網速度比較慢？
1. 手機處理器不夠強
2. 手機記憶體不夠大
3. 網路速度影響的

百萬小學堂，請回答！

---
這問題真的滿有趣的，給我回答的話我會回答 1，直覺告訴我處理器越強開網頁越快。可惜直覺是錯的。
關於這個問題就有一篇 Paper([Why are Web BrowsersSlowon Smartphones?](http://www.ruf.rice.edu/~mobile/publications/wang11hotmobile.pdf))在討論。本篇截取重點告訴大家這題的答案。

---
## 解答

首先來看圖一
![](https://user-images.githubusercontent.com/18013815/34439654-6622f5a2-ecea-11e7-9255-b948aea96581.png)

IR(Internal representation) 代表 build 的過程，先前提到過解析渲染的過程。此外過程中會由 `index.html` 延伸把所有要的資料都抓回來。
這邊顯示的是簡易的網頁處理流程，我們也看過不少次了。

---
再來看圖三
![](https://user-images.githubusercontent.com/18013815/34439739-08630a8c-eceb-11e7-9354-3b05259528a4.png)
這張圖顯示一般手機載入網頁每個步驟所需的時間。這邊注意到 inter-group dependency 所花的時間有點長。

---
圖四顯示連接不同網路，所帶來的差異
![](https://user-images.githubusercontent.com/18013815/34439787-7060d574-eceb-11e7-98cd-0ee3a6270d09.png)
乙太網路這邊下載速度是 1GB， 3G 網路下載速度大約 40 MB，Adverse 設定情況為檔案連結花 400 ms 下載速度 500 KB。
N1、G1 個代表不同款手機，這邊可以不用管，主要是看網路造成差異，發現都是超好幾秒，相當於 20、30%

---
再來看如果將計算效能加快會怎麼樣
![](https://user-images.githubusercontent.com/18013815/34439788-72df191e-eceb-11e7-8075-66447d797363.png)
這邊列出桌面版、行動版網站的數據，但不論哪一種，在哪一個模組（版面、渲染、style）將他速度加到 32 倍，對整體時間的影響微乎其微，最多就 4％。事實上，手機計算效能差異最多也才2、3倍而已。所以這邊證明 IR 對於網路瀏覽速度幾乎沒影響。

---
看到這邊有沒有有點 sense 了？

最後來看網路頻寬和網路來回通訊延遲(Round-trip time, RTT)的影響
![](https://user-images.githubusercontent.com/18013815/34440036-6436dd0a-eced-11e7-9c36-b519eb420c80.png)
直接發現 RTT 影響比寬頻更大。答案呼之欲出了！

---
## 結論
實際研究發現，大多數時間都花在 RTT 上面了，其次是網路速度。其實這也滿合理的，手機是連基地台，網路延遲程度比乙太網路嚴重很正常，更不要說 3G（甚至 4G）寬頻想要贏過光纖網路。並且當 RTT 與網路速度兩者加起來時，效果更明顯，你會有「感覺」到怎麼好「卡」？所以，假設你想要上網快一點，其實手機好不好關係其實不是很大。（不過如果想要玩 WebVR 的話，手機還是要很好啦～）

你答對了嗎？想當年我也有看百萬小學堂，也只記得小西瓜這號人物而已了。 Orz

最後這篇論文結論有提出一些觀點，我就不翻譯了，附給大家參考：
> The loading of multiple resources can be batched in various ways to hide the resource loading time. For example, Google normally batches multiplepictures into one and send itto the browserdirectly. This eliminates  multiple  RTTs needed to get several pictures. Furthermore, the batched loading can be supported by a proxy in the  cloud  in  order to suppress the long  RTT  of the wireless first hop. Finally, it can be supported by new ways of specifying webpage resourcesso that the browser can load  resources as soon as possible, such as Data URI scheme 

如果還有興趣的話，可以看這個提問的[回答](https://serverfault.com/questions/387627/why-do-mobile-networks-have-high-latencies-how-can-they-be-reduced)(why-do-mobile-networks-have-high-latencies-how-can-they-be-reduced)

回答中有個表格是，一個 HTTP 要求所經過的各項延遲

RTT Things | 3G     | 4G
---|---|---
Control plane          | 200–2,500 ms | 50–100 ms
DNS lookup             | 200 ms       | 100 ms
TCP handshake          | 200 ms       | 100 ms
TLS handshake          | 200–400 ms   | 100–200 ms
HTTP request           | 200 ms       | 100 ms
Total latency overhead | 200–3500 ms  | 100–600 ms

5G 好像也要出來了喔！
