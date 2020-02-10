---
title: 瀏覽器引擎處理 CSS 的簡易版（三）
date: 2017-12-18 22:46:13
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


明天一樣討論 robinson 這個「玩具」專案。讓我們來直接看 [robinson/src/style.rs](https://github.com/mbrubeck/robinson/blob/master/src/style.rs) 這邊如何實作 style。如果你還沒看過 CSS 系列的前兩部分，建議你先看一下。如果是系列的新讀者，建議你從第一篇開始讀。

這邊要注意一下，我們昨天提到的四個特性，在這邊都沒有實作，這邊做的部分只是最簡單的，把 CSS 綁定 DOM。也就是讓 DOM 能有顏色、大小之類的樣子。

## 程式

這邊我們定義一個 `StyledNode` 作為 style tree 的節點。還記得 DOM tree + CSS tree = style tree 嗎？

```
pub fn style_tree<'a>(root: &'a Node, stylesheet: &'a Stylesheet) 
-> StyledNode<'a> {

    StyledNode {
        node: root,
        specified_values: match root.node_type {
            NodeType::Element(ref elem) => 
                specified_values(elem, stylesheet),
            NodeType::Text(_) => HashMap::new()
        },
        children: root.children
                      .iter()
                      .map(|child| style_tree(child, stylesheet))
                      .collect(),
    }
    
}
```
每個節點對應的 DOM 和 style 的屬性

```
/// A node with associated style data.

pub struct StyledNode<'a> {
    pub node: &'a Node,
    pub specified_values: PropertyMap,
    pub children: Vec<StyledNode<'a>>,
}
```

---
接著從 CSS tree 中，遍佈的尋找對應的 DOM，為什麼從 CSS tree 而不是 DOM tree 呢？因為 CSS 一定會有對應的 DOM （除非是無效 CSS），而 DOM 不一定會有對應的 CSS，所以從 CSS 找 DOM 效率比較高。

還記得我們 CSS 模組做過的事情嗎？ Stylesheet 裡面有很多 rules，每個 rules 裡面又有很多 selectors，對應各自的值。

所以這邊直接遍佈 Stylesheet，這時候每檢查一個 rule 會呼叫 `match_rule`，每次 `match_rule` 會再檢查 selectors。
```
// Find all CSS rules that match the given element.

fn matching_rules<'a>(elem: &ElementData, stylesheet: &'a Stylesheet) -> Vec<MatchedRule<'a>> {
    stylesheet.rules.iter()
              .filter_map(|rule| match_rule(elem, rule))
              .collect()
}
```
```
// If `rule` matches `elem`, return a `MatchedRule`. 
// Otherwise return `None`.

fn match_rule<'a>(elem: &ElementData, rule: &'a Rule) 
-> Option<MatchedRule<'a>> {
    rule.selectors.iter()
        .find(|selector| matches(elem, *selector))
        .map(|selector| (selector.specificity(), rule))
}
```

--- 
藉由之前在 DOM 模組做的，這邊可以輕鬆取得 DOM 的 CSS 是什麼。
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
再藉由 `matches` 由 selector 去對應 DOM 的 CSS，如果有匹配就回傳
```
/// Selector matching:
fn matches(elem: &ElementData, selector: &Selector) -> bool {
    match *selector {
        Selector::Simple(ref simple_selector) => 
            matches_simple_selector(elem, simple_selector)
    }
}

fn matches_simple_selector(elem: &ElementData, selector: &SimpleSelector) -> bool {
    // Check type selector
    if selector.tag_name.iter().any(|name| elem.tag_name != *name) {
        return false
    }

    // Check ID selector
    if selector.id.iter().any(|id| elem.id() != Some(id)) {
        return false;
    }

    // Check class selectors
    let elem_classes = elem.classes();
    if selector.class.iter().any(|class| !elem_classes.contains(&**class)) {
        return false;
    }

    // We didn't find any non-matching selector components.
    true
}
```

---

最後我們就讓本文一開始提到的 `style_tree`  藉由執行 `specified_values` 取得樹裡面的數值，取得方式是靠上面提到的 `matching_rules`。

```
/// Apply styles to a single element, returning the specified styles.
fn specified_values(elem: &ElementData, stylesheet: &Stylesheet) -> PropertyMap {
    let mut values = HashMap::new();
    let mut rules = matching_rules(elem, stylesheet);

    // Go through the rules from lowest to highest specificity.
    rules.sort_by(|&(a, _), &(b, _)| a.cmp(&b));
    for (_, rule) in rules {
        for declaration in &rule.declarations {
            values.insert(declaration.name.clone(), declaration.value.clone());
        }
    }
    values
}
```

---

以上就是簡單的 style tree 實作方式，其實眼尖的話就可以發現沒什麼技術，等於就是好幾個迴圈去做匹配，只是寫法比較好看而已。這種寫法是完全線性，非常沒效率，最新的 Servo 的 Stylo 就針對這部份做高效能的優化，其中一項就是平行化處理樹。

希望有幫到大家，大家明天見！

