---
title: 瀏覽器開發進階實戰（三）捲動
date: 2017-12-28 23:21:25
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
今天繼續以[Servo](https://github.com/servo/servo) 專案來討論如何實作。

今天主題是 scroll，也就是捲動。當頁面大於視窗，或是元素內容大於元素本身，這時候我們常常會看到到「捲軸」出現。並且我們可以捲動視窗，這就是 scroll 做的事情了。不過今天討論的是使用 script 去做捲動。捲動牽扯到的東西太多，不可能把所有機制都講，所以今天挑一小部分來說明。

在實作之前，我們先來看看[文件](https://drafts.csswg.org/cssom-view/#scrolling-box)怎麼寫的。

> Elements and viewports have an associated scrolling box if has a scrolling mechanism or it overflows its content area and the used value of the overflow-x or overflow-y property is hidden.
An element body (which will be the HTML body element) is potentially scrollable if all of the following conditions are true:
> * body has an associated CSS layout box.
> * body’s parent element’s computed value of the overflow-x or overflow-y properties is not visible.
> * body’s computed value of the overflow-x or overflow-y properties is not visible.

這段文字告訴我們，如果元素是 scrolling box（捲動盒子）的話，他會有捲動的機制（例如捲軸）或是他的內容面積超過原本大小，並且超過的 overflow-x 或 overflow-y 被設定為隱藏。

這邊有幾個關鍵，基本上要能捲動就他就必須是捲動盒子。此外如果元素超過的部分沒有被隱藏，而是設定為顯示，那超出的地方已經顯示了，自然不會有捲動的問題。

然後他又說如果元素的本體是有捲動的「潛力」，則會滿足：
* 是 layout box
* 元素的父元素不是設定 overflow 為顯示（不然子元素也會套用顯示）
* 元素的 computed value 的 overflow-x 和 overflow-y 不是設為顯示 （computed value 先前[文章](https://ithelp.ithome.com.tw/articles/10191967)有解釋過）

再來要解釋一下，什麼是「有 overflow」？
簡單來說就是「視窗大小」小於「內容大小」。

---
接著我們來認識幾個 script 的用法：
```
//假設有個 box 元素已經指定好了
box.scroll(50, 60);  // 捲動到 (x: 50, y: 60)
console.log(box.scrollLeft); // 50
console.log(box.scrollTop); // 60
```
第一行是設定捲到哪裡，所以是 setter
第二、第三行是取得捲到哪裡了，所以是 getter

---
好了，該知道的都知道了。我們上工！

現在我們想完成 `scroll` setter 的一部分，文件在[這邊](https://drafts.csswg.org/cssom-view/#dom-element-scroll)，事實上 `scroll`、`scrollTop`、`scrollLeft` 在 setter 的定義都很接近。
我們今天想完成 `scroll` setter 的第十步驟。

其他步驟大家可以自行點進去看，這邊就不附上了。第十步是說：
> If the element does not have any associated CSS layout box, the element has no associated scrolling box, or the element has no overflow, terminate these steps.

意思是說假設元素：
1. 不是 CSS layout box
2. 不是 scrolling box
3. 元素沒有 overflow

滿足以上三點的任一個，`scroll` 就會被終止，意思是即使 script 叫你卷動，也不會實際去執行，因為不滿足可以捲動的定義。而這三點特性，在文章一開始我們便解釋過了。

---
接著就可以實作了：

第十步其實就是：
```
// Step 10
if !self.has_css_layout_box() ||
   !self.has_scrolling_box() ||
   !self.has_overflow()
{
    return;
}
```

還有文章一開始定義的幾個特性：
```
// https://drafts.csswg.org/cssom-view/#scrolling-box
fn has_scrolling_box(&self) -> bool {
    // TODO: scrolling mechanism, such as scrollbar (We don't have scrollbar yet)
    //       self.has_scrolling_mechanism()
    self.overflow_x_is_hidden() ||
    self.overflow_y_is_hidden()
}

fn has_overflow(&self) -> bool {
    self.ScrollHeight() > self.ClientHeight() ||
    self.ScrollWidth() > self.ClientWidth()
}
```

這其實是一次 [commit](https://github.com/servo/servo/commit/9965f7e2cc0f722acfee5f0710b74a84d1112b54) 所完成的事情，大家有興趣可以點進去看那次貢獻總共做了哪些事情。

---

希望有幫到大家，大家明天見！

