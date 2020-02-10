---
title: 瀏覽器引擎處理 HTML 的簡易版
date: 2017-12-15 22:43:03
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


這篇一樣使用 [robinson](https://github.com/mbrubeck/robinson) 這個「玩具」來進行講解，還記得我們第二篇文章中提到解析的部分嗎？分為 HTML 和 CSS 解析。忘記的話、或是之前偷懶沒看的話，可以回去看一下，那篇解釋瀏覽器如何進行解析，「How browser work」一篇文章更是對原理講得非常仔細，讀懂原理才能知道這篇在做什麼。

我們知道如何處理一個 DOM 了，接下來我們要來解析 HTML 本身了！解析好的 HTML 便可以使用我們昨天寫好的 DOM 模組來組裝。這樣一來就完成 DOM Tree 的部分了！

robinson 關於 html 的部分在 [robinson/src/html.rs](https://github.com/mbrubeck/robinson/blob/master/src/html.rs)。程式碼也不算太長，比昨天稍微朝一點點而已。

玩具當然無法滿足我們，我們最終的目標是要去挑戰 Servo 專案，這邊先告訴大家，Servo 的 html parser 是 [html5ever](https://github.com/servo/html5ever)，其實做原理也是照著 SPEC 來完成的，被獨立出來作為一個模組。意思是他不是包含在 Servo 裡面，假設你也用 Rust 語言寫一個「玩具瀏覽器」，你可以完全使用這個套件來完成 html 的解析。把時間花在更想實作練習的項目上！

## 實作

以下為我直接複製 [`html.rs`](https://github.com/mbrubeck/robinson/blob/master/src/html.rs) 過來，並拆解成片段來解釋在做什麼。
建議先去看原始碼，大概意會一下原始程式碼的想法。再來看我的解說。
程式的作者也有寫[文章](https://limpet.net/mbrubeck/2014/08/11/toy-layout-engine-2.html)解釋，但我的絕對比他的更詳細，當然還是中文的 X)
原始程式碼的註解和一些我覺得不用特別解說的部分這邊有拿掉。這邊只挑出關鍵的邏輯部分。
這段程式碼有一些使用 Rust 語言的特性，不影響邏輯理解，但是如果想完全瞭解程式碼的運作過程，最好還是去了解一下 Rust 的使用方式。

好啦！我們上路！

---
```
// 昨天我們實作的 DOM 這邊就拿來使用
use dom;
// 用來儲存資料
use std::collections::HashMap;
```

用我們寫好的 Parser 來進行解析，其中 `dom::elem()` 是我們昨天定義的函示，解析完 HTML 就可以建立一個新的 DOM。Parser 的實作在下面。
```
pub fn parse(source: String) -> dom::Node {
    let mut nodes = Parser { pos: 0, input: source }.parse_nodes();

    // 如果節點只有一個，也就是根節點，就返回
    if nodes.len() == 1 {
        nodes.swap_remove(0)
    // 不然就建立節點
    } else {
        dom::elem("html".to_string(), HashMap::new(), nodes)
    }
}
```

建立一個 Class 叫做 Parser，你可以完全不要這樣寫，這邊只是一種可行的方式
```
struct Parser {
    pos: usize,
    input: String,
}
```

Parser 的 method
```
impl Parser {
    ...
    ...
}
```

---
***以下是 Parser 的 Methods***

這邊把所有子節點都解析進來
```
    /// Parse a sequence of sibling nodes.
    fn parse_nodes(&mut self) -> Vec<dom::Node> {
        let mut nodes = vec!();
        loop {
            self.consume_whitespace();
            if self.eof() || self.starts_with("</") {
                break;
            }
            nodes.push(self.parse_node());
        }
        nodes
    }
```


判斷解析的節點是元素還是文字節點。如果是文字節點就會者的像是，`<h1>Tiltle</h1>`，可以看到裡面只有文字，所以這邊用`<`來判斷是什麼節點。當然因為這邊假設只有兩種節點型態才能這樣做。
```
    /// Parse a single node.
    fn parse_node(&mut self) -> dom::Node {
        match self.next_char() {
            '<' => self.parse_element(),
            // 在 Rust 中，_ 代表其餘狀況，或是設定值為空
            _   => self.parse_text()
        }
    }
```

解析一個元素，這邊把檢查一起寫進來了，正式的產品不建議這樣做，最好是能夠把測試分離。
一個元素大概長這樣:
```html
<div>
    <p> Hello </p>
</div>
```
然後你再看一下這邊解析元素作的部分，就能明白為啥要有三個步驟。
```
    /// Parse a single element, including its open tag, contents, and closing tag.
    fn parse_element(&mut self) -> dom::Node {
        // Opening tag.
        assert_eq!(self.consume_char(), '<');
        let tag_name = self.parse_tag_name();
        let attrs = self.parse_attributes();
        assert_eq!(self.consume_char(), '>');

        // Contents.
        let children = self.parse_nodes();

        // Closing tag.
        assert_eq!(self.consume_char(), '<');
        assert_eq!(self.consume_char(), '/');
        assert_eq!(self.parse_tag_name(), tag_name);
        assert_eq!(self.consume_char(), '>');

        dom::elem(tag_name, attrs, children)
    }
```

這邊認定 `tag` 的名稱只會有英文和數字
```
    /// Parse a tag or attribute name.
    fn parse_tag_name(&mut self) -> String {
        self.consume_while(|c| match c {
            'a'...'z' | 'A'...'Z' | '0'...'9' => true,
            _ => false
        })
    }
```

Attibutes 就像是 `class="btn red box"`，會用空白隔開，所以這邊解析屬性時，將屬性內容用空白切開，跑回圈來記錄。
```
    /// Parse a list of name="value" pairs, separated by whitespace.
    fn parse_attributes(&mut self) -> dom::AttrMap {
        let mut attributes = HashMap::new();
        loop {
            self.consume_whitespace();
            if self.next_char() == '>' {
                break;
            }
            let (name, value) = self.parse_attr();
            attributes.insert(name, value);
        }
        attributes
    }
```

只處理元素的 `name`，像是 `<input name="upload">` 這種。
```
    /// Parse a single name="value" pair.
    fn parse_attr(&mut self) -> (String, String) {
        let name = self.parse_tag_name();
        assert_eq!(self.consume_char(), '=');
        let value = self.parse_attr_value();
        (name, value)
    }
```

解析文字節點，上面有提過，節點內不該有`<`存在
```
    /// Parse a text node.
    fn parse_text(&mut self) -> dom::Node {
        dom::text(self.consume_while(|c| c != '<'))
    }
```

一般瀏覽器對於多餘的空白都會直接忽視，所以這邊有特別處理一下，其實不是很重要啦
```
    /// Consume and discard zero or more whitespace characters.
    fn consume_whitespace(&mut self) {
        self.consume_while(char::is_whitespace);
    }
```

這邊實現的解析器，是從左到右，一個字元一個字元向右判斷，然後把輸入的字串跑完來做解析
```
    /// Return the current character, and advance self.pos to the next character.
    fn consume_char(&mut self) -> char {
        let mut iter = self.input[self.pos..].char_indices();
        let (_, cur_char) = iter.next().unwrap();
        let (next_pos, _) = iter.next().unwrap_or((1, ' '));
        self.pos += next_pos;
        cur_char
    }
```

---
以上就是簡單的 HTML 解析器，基本功能都有了，當然很多缺陷，不僅一堆特殊狀況無法處理，很多的標準 HTML 寫法也不支援。不過我們也大概了解 Parser 的作用和做法了，可以以此改進，或是有興趣的話就去貢獻一下到 html5ever 吧！

明天討論 CSS，大家再見！

