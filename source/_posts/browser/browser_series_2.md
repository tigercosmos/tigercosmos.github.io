---
title: 深入探討瀏覽器引擎如何進行解析
date: 2017-12-13 23:08:30
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)

暖身完畢！本文開始進入本系列重點。
接下來要深入探討渲染引擎的運作原理以及實作方式。

## 目前普及的瀏覽器引擎
最常聽到的莫過於 Mozilla 的 Gecko，最主要被用在 Firefox 上，也是第一款被設計為可作為單一模組存在的瀏覽器引擎。另外就是 WebKit，起初用在 Linux 平台，後來經由 Apple 公司進行修改後，Windows 和 macOS 也支援，主要用在 Chrome 和 Safari。這兩款都是開源專案。

關於兩者的工作流程，可以參考 [how browser work](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/) 這篇文章的示意圖。
Webkit 長這樣：
![](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/webkitflow.png)
Gecko 長這樣：
![](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/image008.jpg)

可以看到雖然兩者採用的術語不同，但概念其實是很像的。當然，更深入的實作方式就完全不同了，各種小細節造就一個引擎的厲害程度，也是各家比拼的重點！

## 解析
在上面兩張圖中，我們都可以看到 HTML Parser，功用就是把 HTML 的原始碼解析成 DOM tree。HTML 在解析的時候不能用一般的解析方式，因為 HTML 本身可以容錯，例如說原本應該是 `<div></div>`，但如果我們不小心漏掉 `</div>`，依舊可以看到正確地顯示。雖然說容錯對於使用者來說很方便，但也就使得解析的方式比較特別了。事實上，[W3C](https://www.w3.org/TR/html5/syntax.html#html-parser) 有完整定義如何去做這個步驟，通常我們在開發引擎核心時，就是直接照著 SPEC 來做。

同理， CSS Parser，功用就是把 CSS 的原始碼解析成 CSS tree。而一樣 [W3C](https://www.w3.org/TR/CSS2/grammar.html) 也定義好規範了。CSS 因為不像 HTML 有上下關係（有`<div>`就會有`</div>`），所以可以使用一般常見解析的解析方式。例如：
> WebKit 使用了兩種非常有名的解析器生成器：用於創建詞法分析器的 Flex 以及用於創建解析器的 Bison（您也可能遇到 Lex和 Yacc這樣的別名）。Flex 的輸入是包含標記的正則表達式定義的檔案。Bison 的輸入是採用 BNF 格式的語言語法規則。 

關於瀏覽器引擎的處理方式，[how browser work](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/) 這篇經典文章講的太清楚了，我認為這篇已經非常精簡也很清楚，因此不打算重複闡述原理。如果大家在閱讀這篇上有遇到問題，歡迎和我討論！

## 開發
當我們在設計一個瀏覽器的時候，寫處理 HTML 和 CSS 的部分是相對容易的（這邊不探討 JS，那又是另一個引擎了），因為 W3C 都有明確規範，例如我們常聽到的 HTML5、CSS3，因為要讓各家品牌做出來的東西可以呈現一樣，才不會發生同一份原始碼，在 Chrome 上跟在 Firefox 上差非常多，這樣開發者大概會瘋掉吧！所以 W3C 才都有完整的定義，甚至除了規則以外，連實作的細項步驟都寫得一清二楚。閒來無事的話可以點開看看 https://html.spec.whatwg.org 。

例如擷取 [Servo](https://github.com/servo/servo) 專案 [`components/script/dom/document.rs`](https://github.com/servo/servo/blob/master/components/script/dom/document.rs) 的其中一段，可以看到這目前這個函式，就是根據註解起來的 SPEC 文件中的 `current-document-readiness` 來寫的。

```

// https://html.spec.whatwg.org/multipage/#current-document-readiness
pub fn set_ready_state(&self, state: DocumentReadyState) {
    match state {
        DocumentReadyState::Loading => {
            // https://developer.mozilla.org/en-US/docs/Web/Events/mozbrowserconnected
            self.trigger_mozbrowser_event(MozBrowserEvent::Connected);
            update_with_current_time_ms(&self.dom_loading);
        },
        DocumentReadyState::Complete => {
            // https://developer.mozilla.org/en-US/docs/Web/Events/mozbrowserloadend
            self.trigger_mozbrowser_event(MozBrowserEvent::LoadEnd);
            update_with_current_time_ms(&self.dom_complete);
        },
        DocumentReadyState::Interactive => update_with_current_time_ms(&self.dom_interactive),
    };

    self.ready_state.set(state);

    self.upcast::<EventTarget>().fire_event(atom!("readystatechange"));
}
```

