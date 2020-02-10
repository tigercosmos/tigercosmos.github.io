---
title: 瀏覽器引擎處理 DOM 的簡易版
date: 2017-12-14 23:47:47
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


## 玩具？
接下來開始會實戰解說瀏覽器引擎，由於我沒有接觸過 Gecko 或是 WebKit，所以會由 Servo 來切入，這幾個都是瀏覽器引擎，之前文章有提到過。Gecko 那些已經是龐然大物，但 Servo 也已經不小了，直接切入有點太困難，所以我們先從「玩具」瀏覽器開始解說，之後再進階成真正的。所謂玩具的意思是，功能非常簡陋，存粹煉功用的，就像是大學修資料庫、編譯程式這類的課程，也都會實做一個玩具當作專題。玩具本身當然不能跟真正的產品相比，但概念是一致的，可以藉由玩具來了解產品。

以下這幾個都是比較小型的引擎專案：
* [CSSBox (Java)](https://github.com/philborlin/CSSBox)
* [Cocktail (Haxe)](https://github.com/silexlabs/Cocktail)
* [gngr (Java)](https://gngr.info/)
* [litehtml (C++)](https://github.com/tordex/litehtml)
* [LURE (Lua)](https://github.com/admin36/LURE)
* [NetSurf (C)](http://www.netsurf-browser.org/)
* [Simple San Simon (Haskell)](http://hsbrowser.wordpress.com/3s-functional-web-browser/)
* [WeasyPrint (Python)](https://github.com/Kozea/WeasyPrint)
* [WebWhirr (C++)](https://github.com/reesmichael1/WebWhirr)

因為是小型的，所以很適合拿來初步學習，看看怎樣制定架構、實作功能等等。大家可以每個專案點進去看看他們的架構、邏輯、寫法，稍微有個概念，也可以順便比較看看大家的差異。同樣一件事本來就有很多種做法 ＸＤ

本文採用 [@mbrubeck](https://github.com/mbrubeck/) 的作品 [robinson](https://github.com/mbrubeck/robinson) 來解說，原因是這個人也是 Servo 的開發團隊者之一，寫法算是簡易型的 Servo，對我們之後探討 Servo 會有幫助。此外這個專案是用 Rust 語言寫的。

## DOM
先來看看簡易版的的 DOM 長怎樣吧！
實作 DOM 的程式碼在 [robinson/src/dom.rs](https://github.com/mbrubeck/robinson/blob/master/src/dom.rs)，可以點進去看一下，其實非常短。這邊可以對照一下 Servo 的部分，是在 [servo/components/script/dom/](https://github.com/servo/servo/tree/master/components/script/dom) 點進去你就會嚇到了！

來解釋一下 robinson 的 dom 在做什麼。

### 定義節點
HTML 是由一堆的節點組成的。也就是我們平常看到的 `<body>` 、 `<div>` 、 `<p>` 之類的標籤，而這些標籤彼此有上下關係，也就形成了節點。
所以這邊先定義什麼是節點，節點包含他的「子」節點，另外節點也有分種類，例如元素、圖片、文字，因為這邊是最陽春的那種，所以只有定義兩種。
```
#[derive(Debug)]
pub struct Node {
    // data common to all nodes:
    pub children: Vec<Node>,

    // data specific to each node type:
    pub node_type: NodeType,
}

#[derive(Debug)]
pub enum NodeType {
    Element(ElementData),
    Text(String),
}
```

### 屬性
這邊實作元素的屬性，也就是平常看到的 `class` 、 `name` 、 `id`，當然這邊也是簡單地呈現而已。
```
pub type AttrMap = HashMap<String, String>;
```
```
#[derive(Debug)]
pub struct ElementData {
    pub tag_name: String,
    pub attributes: AttrMap,
}
```

### 建構子
所謂建構子就是初始化建立一個物件，這邊也是一樣的概念，讓我們可以輕鬆建立一個元素物件。
由於作者只寫了兩種節點，所以建構子也就只有兩種，仔細看的話應該不難理解，像是 `elem` 就是建立元素，他連子元素和屬性一起建立起來。
```
pub fn text(data: String) -> Node {
    Node { children: vec![], node_type: NodeType::Text(data) }
}

pub fn elem(name: String, attrs: AttrMap, children: Vec<Node>) -> Node {
    Node {
        children: children,
        node_type: NodeType::Element(ElementData {
            tag_name: name,
            attributes: attrs,
        })
    }
}
```

### 屬性綁定
元素歸元素，屬性歸屬性，要讓元素有屬性，當然還要做點事，這邊就是把屬性綁定元素的實現，這邊只是簡單的取得這個元素的 `id` 和 `class`。事實上實際情況複查得多，例如還要檢查屬性的正確性，還要跟 JS 做連結，有些屬性還會有邏輯，例如 `<input>` 的 `type` 就好幾種，如 `month` 、 `date` 、 `color`，每種邏輯都有各自的演算法。
```
impl ElementData {
    pub fn id(&self) -> Option<&String> {
        self.attributes.get("id")
    }

    pub fn classes(&self) -> HashSet<&str> {
        match self.attributes.get("class") {
            Some(classlist) => classlist.split(' ').collect(),
            None => HashSet::new()
        }
    }
}
```

---

今天看了簡單的 DOM 實作方式，真實的瀏覽器絕對更複雜，萬事起頭難，千萬別灰心！我們先從簡單的學起，之後再繼續挑戰更複雜的真實版本。這幾天都會是簡單版的講解，大家明天見！


