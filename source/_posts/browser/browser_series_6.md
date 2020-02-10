---
title: 瀏覽器引擎處理 CSS 的簡易版（二）
date: 2017-12-17 21:15:08
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


處理 CSS 又分兩個步驟，有 Parser 和 style，前者是解析原始 CSS，後者則是讓 DOM 有 style。
昨天討論過 CSS parser 了，而今天就來談談 style。

---
## Style
在開始講解實作之前，先來談談 style 幾個性質。

* Cascading
* Specified, computed, and actual values
* Inheritance
* Attribute

### Cascade
可以先看一下 [mozilla](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) 的文件。
簡單來說就是 style 有分好幾個等級，使用者定義高過瀏覽器預設，有加上 `!important` 的等級比沒加的高。當使用者沒有定義 style 的時候，瀏覽器就會使用自己預設的。所以你會發現 `<h1>` 比 `<h2>` 字體要大，明明自己的 CSS 沒有定義，這就是因為瀏覽器有預設的 style 了。

### Specified, computed, and actual values
這部分可以看 [W3C](https://www.w3.org/TR/CSS2/cascade.html#computed-value) 的文件。
主要是說當瀏覽器開始解析並構建 DOM 樹，那麼就必須為 DOM 樹中的每個元素的每個屬性賦予一個值。

然而每個屬性的最終值最終值是通過四步計算得來的：
1. 通過每個屬性的規範說明的默認值或者是用戶顯示通過 CSS 規則指定的一個值，稱為指定值。
1. 指定值被解析為 DOM 樹繼承時使用的值，稱為計算值。
1. 計算值在必要時會被轉換為一個絕對值，稱為使用的值。
1. 最後使用的值會由於本地環境的限制再做一次近似轉化，比如使用的值是1.5px，但是某些瀏覽器不支持.5px會做一次近似取值，最終的值是2px，稱為實際價值。

### Inheritance
繼承是指延續父節點的屬性，直接繼續套用。我們可以讓子節點進行繼承父節點的屬性，例如字體和顏色，如下：
```html
<div style="color: red;">
    <p> 這邊的文字就會是紅色 </p>
</div>
```
因為有繼承，我們不用每個元素都特地設定字體、顏色等等屬性，他們自己就會遵循父節點的設定，要是每個節點都要特地設定，那該有多麻煩！

然而像是 margin、padding、border、background-image 這些就不會被繼承。這些攸關於版面輸出，要是他們也被繼承，那畫面根本就會是一團亂了！

### Attribute
CSS 我們通常定義在 `.css` ，並被 `.html` 引入，或是在 html 中使用 `<style>` 標籤來著名是 CSS 的定義區塊。但我們也可以在寫 HTML DOM 的時候，直接賦予它 CSS，這就叫做 attribute。所以瀏覽器除了從 CSS 中解析之外，在處理 DOM 的時候也要留意有沒有 CSS 並把它插入 CSS 的樹當中。
例如原本應該是：
```
<style>
    div {
        padding: 10px;
        color: red;
    }
</style>
<div></div>
```
可以寫成：
```html
<div style="padding:10px; color: red;"></div>
```

---
明天再來討論如何實作，一樣會使用 robinson 這個「玩具」專案。robinson 將 CSS 拆成兩個模組，在 [robinson/src/css.rs](https://github.com/mbrubeck/robinson/blob/master/src/css.rs) 和 [robinson/src/style.rs](https://github.com/mbrubeck/robinson/blob/master/src/style.rs)。再提一次，Servo 的 CSS 部分在 [servo/components/style](https://github.com/servo/servo/tree/master/components/style)，對照著看對之後我們學習 Servo 會有幫助。

希望對大家有幫助，大家明天見！

