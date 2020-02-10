---
title: 瀏覽器引擎處理版面佈局的簡易版（一）
date: 2017-12-21 23:31:34
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
經過幾天身心調養後，我們再回來討論 robinson 這個「玩具」專案。接著我們來看 [robinson/src/layout.rs](https://github.com/mbrubeck/robinson/blob/master/src/layout.rs) 這個模組。如果你還沒看過本系列的前面部分，建議你先看一下。如果是系列的新讀者，建議你從第一篇開始讀。

還記得瀏覽器的簡易步驟嗎？
```sh
DOM tree \
           --> style tree --> layout --> painting
CSS tree /
```

前幾個步驟我們之前已經講過了。所以接下來要介紹 layout。而這個模組就在實現 layout 的部分。

layout（版面佈局）就是一堆的 box（盒子）。一個盒子是一個網頁的矩形部分。盒子具有寬度、高度和頁面上的位置，形成一個矩形。 這個矩形被稱為內容區，因為內容會呈現在區塊內。內容可以是文字、圖像、影片或其他小盒子。

這張圖片大家應該很熟悉：
![box](https://www.w3.org/TR/CSS2/images/boxdim.png)
或是有顏色的可能更熟悉：
![box](https://i.imgur.com/crDJAoT.png)
沒錯，就是你按 F12，在開發者工具中看到的畫面！

box 的周圍也可能會有 padding、borders、margins 等屬性。就像上面兩張圖所顯示的。
[W3C](https://www.w3.org/TR/CSS2/box.html)也有完整的文件定義。

這邊需要大家對 [padding](https://developer.mozilla.org/zh-TW/docs/Web/CSS/padding)、[margin](https://developer.mozilla.org/zh-TW/docs/Web/CSS/margin) 有更多了解。雖然我們在實作簡單版的 layout 時不會去處理這些性質，但在真實的瀏覽器中確是至關重要，真正的瀏覽器一點偏差都不能有，能不能將所有 box 處理好，影響最終的結果。

此外像是 scroll、client 等等的功能都會需要好的 box。不然就會發生畫面捲動的位子就會是錯的，瀏覽器本身的視窗大小也不是對的。

以上的幾個連結希望大家能點進去更近一步了解，明天我們來看如何實作。

大家明天見！

