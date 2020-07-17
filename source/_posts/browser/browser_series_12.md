---
title: 瀏覽器引擎處理版面佈局的簡易版（三）
date: 2017-12-23 23:31:29
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
接續昨天討論 [robinson/src/layout.rs](https://github.com/mbrubeck/robinson/blob/master/src/layout.rs) 這個 layout 模組。

一般來說，box 是從上到下堆起來的，如果有定義是 inline 的話，則是從左到右。不過這是在 Normal flow 的情況下，也就是沒有定義「[位置](https://www.w3.org/TR/CSS2/visuren.html#positioning-scheme)」，不然你也可以讓某個 box 固定在那邊，也就是不會受任何東西影響他的位置，或是讓某個 box 從右邊對齊。

---
LayoutBox 算出 layout 的初始函數，針對自己是那種型別來開始，這個專案中目前只實作 block。
所以以下都是針對 block 的算法做解釋。
```
// implimpl<'a> LayoutBox<'a>

    /// Lay out a box and its descendants.
    fn layout(&mut self, containing_block: Dimensions) {
        match self.box_type {
            BlockNode(_) => self.layout_block(containing_block),
            InlineNode(_) | AnonymousBlock => {} // TODO
        }
    }
```

---
一個 box 實際大小高度會受子影響，而自己的寬度會限制子的排列。

簡單來說解釋：
```
<A height = 100>
    <a heught = 200>
</A>
```
這樣的話 `A` 的實際高度會是 200，當然如果有設定其他的屬性的話，例如設定 `A` 只顯示定義的高度，那麼 `a` 就會有一半不會顯示出來。


```
<B width = 100>
    <b width = 70>
    <c width = 40>
</B>
```
`B` 的的寬度是 100，雖然 `b` 和 `c` 加起來超過了，但他的寬度依舊是 100。

了解了上面的概念後之後我們開始實作

---
這邊排版一個 block box 的做法：
```
fn layout_block(&mut self, containing_block: Dimensions) {
    // 子受父的寬度影響
    self.calculate_block_width(containing_block);

    // 決定這個 box 的位置
    self.calculate_block_position(containing_block);

    // 把底下的子算一下
    self.layout_block_children();

    // 父的高度受子影響，所以要等子算完才得到父
    self.calculate_block_height();
}
```


如果子內容超過父，是為 overflow。反之子內容比父內容少，是為 underflow。
在 auto 模式下， normal flow 處理 block 的時候，有一套[演算法](https://www.w3.org/TR/CSS2/visudet.html#blockwidth)來想辦法盡量讓子元素符合父。
也就是藉由調整大家的 margin 來達到目的。
例如子元素超過父元素，但是如果把子元素的 margin 拿掉，就吻合了。
或著是子元素填不滿父元素，這時候就把子元素的 margin 加長。
```
// Calculate the width of a block-level non-replaced element in normal flow.
// Sets the horizontal margin/padding/border dimensions, and the `width`.
fn calculate_block_width(&mut self, containing_block: Dimensions) {
    ...
}
```


將子元素和自己本身的內容區域進行排版
```
fn layout_block_children(&mut self) {
    // 將 `self.dimensions.height` 設為全部內容加起來的總高度
    let d = &mut self.dimensions;
    for child in &mut self.children {
        child.layout(*d);
        // 把所有子元素的高度相加
        d.content.height = d.content.height + child.dimensions.margin_box().height;
    }
}
```

這邊概念滿簡單的，如果高度有定義，他就是那麼高，不然就由內容高度決定
```
    /// Height of a block-level non-replaced element in normal flow with overflow visible.
    fn calculate_block_height(&mut self) {
        // If the height is set to an explicit length, use that exact length.
        // Otherwise, just keep the value set by `layout_block_children`.
        if let Some(Length(h, Px)) = self.get_style_node().value("height") {
            self.dimensions.content.height = h;
        }
}
```

如何算出位置呢？簡單來說就是取得先前 box 的位置，在針對自己的 margin、padding 作處理，因為我們的位置是針對最裡面的 comtent area 來訂。（意思就是邊邊雖然雖然佔面積，但元素的原點是在 cotent area）
```
    fn calculate_block_position(&mut self, containing_block: Dimensions) {
        let style = self.get_style_node();
        let d = &mut self.dimensions;

        // margin, border, and padding have initial value 0.
        let zero = Length(0.0, Px);

        // If margin-top or margin-bottom is `auto`, the used value is zero.
        d.margin.top = style.lookup("margin-top", "margin", &zero).to_px();
        d.margin.bottom = style.lookup("margin-bottom", "margin", &zero).to_px();

        d.border.top = style.lookup("border-top-width", "border-width", &zero).to_px();
        d.border.bottom = style.lookup("border-bottom-width", "border-width", &zero).to_px();

        d.padding.top = style.lookup("padding-top", "padding", &zero).to_px();
        d.padding.bottom = style.lookup("padding-bottom", "padding", &zero).to_px();

        d.content.x = containing_block.content.x +
                      d.margin.left + d.border.left + d.padding.left;

        // Position the box below all the previous boxes in the container.
        d.content.y = containing_block.content.height + containing_block.content.y +
                      d.margin.top + d.border.top + d.padding.top;
}
```

---
就由以上的程式，就可以把一個一個的 box 堆疊起來。
而網頁本身就是一堆的 box 堆來堆去。現在你知道如何做了！
希望對大家有幫助，大家明天見！

