---
title: 瀏覽器引擎處理 CSS 的簡易版（一）
date: 2017-12-16 15:52:02
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)

今天繼續使用 [robinson](https://github.com/mbrubeck/robinson) 這個「玩具」來進行講解，第二篇文章講到解析，目前我們已經會處理 DOM 和 HTML 了，接下來就是處理 CSS 的部分。在開始之前，不知道你對 CSS 了解多少，平常有在開發網頁的話應該還算是懂吧，不過我想並沒有真正完全去理解它，因為其實只是開發網頁的話，也不需要懂。

但是既然我們現在要處理 CSS 的部分，有完整的了解當然最好，可以參考 [Mozilla 文件](https://developer.mozilla.org/zh-TW/docs/Web/CSS) 或是 [W3C 文件](https://www.w3.org/Style/CSS/specs.en.html)。

處理 CSS 又分兩個步驟，有 Parser 和 style，前者是解析原始 CSS，後者則是讓 DOM 有 style。

robinson 這個專案中，CSS 拆成兩個模組，在 [robinson/src/css.rs](https://github.com/mbrubeck/robinson/blob/master/src/css.rs) 和 [robinson/src/style.rs](https://github.com/mbrubeck/robinson/blob/master/src/style.rs)。有一點點小長了，因為 CSS 本來就蠻複雜的。對照一下，Servo 的 CSS 部分在 [servo/components/style](https://github.com/servo/servo/tree/master/components/style)，點進去就會發現它很複雜。CSS 部分已經被拿去在 Firefox 上使用，算是滿完整的，正式的名稱叫做 [Stylo](https://wiki.mozilla.org/Quantum/Stylo)，現在只是稍微提一下，之後會再細講。

---
## Parser

今天先針對 parser 來解說， 也就是 [`css.rs`](https://github.com/mbrubeck/robinson/blob/master/src/css.rs) 的部分。（解說都是在程式碼區塊的上方）

定義 css 的規則，所以是規則的向量
```
pub struct Stylesheet {
    pub rules: Vec<Rule>,
}
```

一條一條的規則，包含選擇子和宣告
```
struct Rule {
    selectors: Vec<Selector>,
    declarations: Vec<Declaration>,
}
```

這邊的 `SimpleSelector` 只支援單一邏輯，事實上應該還有[組合子邏輯](https://www.w3schools.com/css/css_combinators.asp)，只是在這邊的範例碼中並沒有實現。
舉例來說多重選擇就是像 `div > p` 或 `div + p` 這樣。

`tag` 就是 `div` 、 `p` 、 `h1` 之類的， `id` 則是 `#` 開頭，而 `class` 就是 `.` 開頭
```
pub struct SimpleSelector {
    pub tag_name: Option<String>,
    pub id: Option<String>,
    pub class: Vec<String>,
}
```
選擇器選到東西之後，會看裡面的內容，也就是宣告了。
例如 `padding: 10px`，`padding` 是名稱，`10px` 則是他的值。
```
struct Declaration {
    name: String,
    value: Value,
}
```
而宣告的值，單位項目都不一樣，必須要有東西來讀他們。例如長度就有可能是 `px` 、 `em`，顏色可以用 `white` 或是 `#000` 來表示。這邊就是定義他們。
```
enum Value {..}
enum Unit {..}
struct Color {..}
```

簡單的 CSS 選擇器，從左到右讀進去，然後存進 `SimpleSelector`，這邊並不嚴謹，很多錯誤的輸入會被當成正確的，就像是 `*ABC*`，但事實上 `*` 當然不會接在尾巴。一般正式的瀏覽器在解析碰到錯誤的時候，會直接忽視那個錯誤的 CSS，一些奇怪的輸入也會被忽視。所以像是輸入 `padding: red` 這種完全錯誤的，瀏覽器就不會把他列入 CSS tree 中。
```
    fn parse_simple_selector(&mut self) -> SimpleSelector {
        let mut selector = SimpleSelector { tag_name: None, id: None, class: Vec::new() };
        while !self.eof() {
            match self.next_char() {
                '#' => {
                    self.consume_char();
                    selector.id = Some(self.parse_identifier());
                }
                '.' => {
                    self.consume_char();
                    selector.class.push(self.parse_identifier());
                }
                '*' => {
                    // universal selector
                    self.consume_char();
                }
                c if valid_identifier_char(c) => {
                    selector.tag_name = Some(self.parse_identifier());
                }
                _ => break
            }
        }
        selector
}
```

Parser 的細節部分跟昨天的 HTML 都非常接近，像是 `parse_declarations` 就是抓兩個大括弧中的內容，然後再針對內容有更近一步的拆解，這部分看原始碼就非常好理解了，就不在一一說明。
```
    /// Parse a list of declarations enclosed in `{ ... }`.
    fn parse_declarations(&mut self) -> Vec<Declaration> {
        assert_eq!(self.consume_char(), '{');
        let mut declarations = Vec::new();
        loop {
            self.consume_whitespace();
            if self.next_char() == '}' {
                self.consume_char();
                break;
            }
            declarations.push(self.parse_declaration());
        }
        declarations
}
```

最後比較重要的部分是，[權重分配](https://www.w3.org/TR/selectors/#specificity)。同一個 DOM 可能同時有很多 CSS 定義它，那究竟要選擇哪個當作最後呈現的，這時候就看他們的重要程度啦。一般而言 id > class > tag，所以就可以定義，比方說 id 加權 3，tag 只有加權 1 之類的，最後哪個 CSS 針對這個 DOM 數值最高，就使用它。
```
impl Selector {
    pub fn specificity(&self) -> Specificity {
        // http://www.w3.org/TR/selectors/#specificity
        let Selector::Simple(ref simple) = *self;
        let a = simple.id.iter().count();
        let b = simple.class.len();
        let c = simple.tag_name.iter().count();
        (a, b, c)
    }
}
```

---
希望對大家有幫助，大家明天見！

