---
title: 瀏覽器引擎輸出畫面的簡易版
date: 2017-12-24 23:33:56
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
在簡易瀏覽器中，我們將流程制定成：
```sh
DOM tree \
           --> style tree --> layout --> painting
CSS tree /
```
前面文章已經將 painting 之前的步驟解說過了，所以我們差最後一個步驟，也就是將處理好的版面繪畫在螢幕上。
這算是最簡單的處理方式，因為就是將靜態的文件處理後輸出成一個影像，可以想成 html 轉圖片的概念，事實上瀏覽器看到的畫面不過是文字可以框選，本質上跟一張有文字、排版的圖片沒太大差異。
而在 roobinson 這個專案中，就是將網頁輸出成影像檔。繪出的模組在 [painting.rs](https://github.com/mbrubeck/robinson/blob/master/src/painting.rs) 裡面。
如果是更真實一點的瀏覽器的話，流程應該會長得像以下：
```sh
DOM tree \
           --> style tree --> layout --> painting
CSS tree /  └─----- rendering <--------┘
```
因為通常網站還會透過 js 渲染，簡單來說就是畫面是動態的，會一直變化。

---
程式邏輯滿簡單的，這邊只講部分 code，有興趣可以上去 [painting.rs](https://github.com/mbrubeck/robinson/blob/master/src/painting.rs) 看他如何實作。

因為我們目的是輸出成一個「畫面」，這邊畫面我們直接輸出成圖像。
因此我們首先建立一個畫布，用來把各種元素畫在裡面。
目前只能畫出各種矩形。包含 box 的內部和邊框。
```
struct Canvas {
    pixels: Vec<Color>,
    width: usize,
    height: usize,
}

impl Canvas {
    // Create a blank canvas
    fn new(width: usize, height: usize) -> Canvas {
        let white = Color { r: 255, g: 255, b: 255, a: 255 };
        return Canvas {
            pixels: repeat(white).take(width * height).collect(),
            width: width,
            height: height,
        }
    }
    // ...
}
```
用 layout tree 建立一個 display tree，包含每個 node 的畫素資訊
```
fn build_display_list(layout_root: &LayoutBox) -> DisplayList {
    let mut list = Vec::new();
    render_layout_box(&mut list, layout_root);
    return list;
}

fn render_layout_box(list: &mut DisplayList, layout_box: &LayoutBox) {
    render_background(list, layout_box);
    render_borders(list, layout_box);
    // TODO: render text
    // 作者還沒有將顯示文字寫進去

    for child in &layout_box.children {
        render_layout_box(list, child);
    }
}
```

把目前的 box 所在的位置的所有畫素的顏色設定好。
```
fn paint_item(&mut self, item: &DisplayCommand) {
    match item {
        &DisplayCommand::SolidColor(color, rect) => {
            // Clip the rectangle to the canvas boundaries.
            let x0 = rect.x.clamp(0.0, self.width as f32) as usize;
            let y0 = rect.y.clamp(0.0, self.height as f32) as usize;
            let x1 = (rect.x + rect.width).clamp(0.0, self.width as f32) as usize;
            let y1 = (rect.y + rect.height).clamp(0.0, self.height as f32) as usize;

            for y in (y0 .. y1) {
                for x in (x0 .. x1) {
                    // TODO: alpha compositing with existing pixel
                    self.pixels[x + y * self.width] = color;
                }
            }
        }
    }
}
```

從 display tree 讀出所有 box 的位置、顏色資訊，然後畫在畫布上。
```
fn paint(layout_root: &LayoutBox, bounds: Rect) -> Canvas {
    let display_list = build_display_list(layout_root);
    let mut canvas = Canvas::new(bounds.width as usize, bounds.height as usize);
    for item in display_list {
        canvas.paint_item(&item);
    }
    return canvas;
}
```

最後就可以透過 [Rust Image](https://github.com/PistonDevelopers/image/) 之類的函式庫，把圖像輸出。
```
// Save an image:
let (w, h) = (canvas.width as u32, canvas.height as u32);
let buffer: Vec<image::Rgba<u8>> = unsafe { std::mem::transmute(canvas.pixels) };
let img = image::ImageBuffer::from_fn(w, h, Box::new(|&: x: u32, y: u32| buffer[(y * w + x) as usize]));
let result = image::ImageRgba8(img).save(file, image::PNG);
```

---
假設你寫成視窗程式，將網頁以圖像呈現，就是最陽春的瀏覽器了！
如此一來，實作簡易版瀏覽器的系列也告一段落！

