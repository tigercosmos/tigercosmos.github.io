---
title: 瀏覽器引擎輸出畫面的簡易版
date: 2017-12-24 23:33:56
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x5728;&#x7C21;&#x6613;&#x700F;&#x89BD;&#x5668;&#x4E2D;&#xFF0C;&#x6211;&#x5011;&#x5C07;&#x6D41;&#x7A0B;&#x5236;&#x5B9A;&#x6210;&#xFF1A;</p>
<pre><code class="language-sh">DOM tree \
           --&gt; style tree --&gt; layout --&gt; painting
CSS tree /
</code></pre>
<p>&#x524D;&#x9762;&#x6587;&#x7AE0;&#x5DF2;&#x7D93;&#x5C07; painting &#x4E4B;&#x524D;&#x7684;&#x6B65;&#x9A5F;&#x89E3;&#x8AAA;&#x904E;&#x4E86;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x5DEE;&#x6700;&#x5F8C;&#x4E00;&#x500B;&#x6B65;&#x9A5F;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5C07;&#x8655;&#x7406;&#x597D;&#x7684;&#x7248;&#x9762;&#x7E6A;&#x756B;&#x5728;&#x87A2;&#x5E55;&#x4E0A;&#x3002;<br>
&#x9019;&#x7B97;&#x662F;&#x6700;&#x7C21;&#x55AE;&#x7684;&#x8655;&#x7406;&#x65B9;&#x5F0F;&#xFF0C;&#x56E0;&#x70BA;&#x5C31;&#x662F;&#x5C07;&#x975C;&#x614B;&#x7684;&#x6587;&#x4EF6;&#x8655;&#x7406;&#x5F8C;&#x8F38;&#x51FA;&#x6210;&#x4E00;&#x500B;&#x5F71;&#x50CF;&#xFF0C;&#x53EF;&#x4EE5;&#x60F3;&#x6210; html &#x8F49;&#x5716;&#x7247;&#x7684;&#x6982;&#x5FF5;&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A;&#x700F;&#x89BD;&#x5668;&#x770B;&#x5230;&#x7684;&#x756B;&#x9762;&#x4E0D;&#x904E;&#x662F;&#x6587;&#x5B57;&#x53EF;&#x4EE5;&#x6846;&#x9078;&#xFF0C;&#x672C;&#x8CEA;&#x4E0A;&#x8DDF;&#x4E00;&#x5F35;&#x6709;&#x6587;&#x5B57;&#x3001;&#x6392;&#x7248;&#x7684;&#x5716;&#x7247;&#x6C92;&#x592A;&#x5927;&#x5DEE;&#x7570;&#x3002;<br>
&#x800C;&#x5728; roobinson &#x9019;&#x500B;&#x5C08;&#x6848;&#x4E2D;&#xFF0C;&#x5C31;&#x662F;&#x5C07;&#x7DB2;&#x9801;&#x8F38;&#x51FA;&#x6210;&#x5F71;&#x50CF;&#x6A94;&#x3002;&#x7E6A;&#x51FA;&#x7684;&#x6A21;&#x7D44;&#x5728; <a href="https://github.com/mbrubeck/robinson/blob/master/src/painting.rs" target="_blank">painting.rs</a> &#x88E1;&#x9762;&#x3002;<br>
&#x5982;&#x679C;&#x662F;&#x66F4;&#x771F;&#x5BE6;&#x4E00;&#x9EDE;&#x7684;&#x700F;&#x89BD;&#x5668;&#x7684;&#x8A71;&#xFF0C;&#x6D41;&#x7A0B;&#x61C9;&#x8A72;&#x6703;&#x9577;&#x5F97;&#x50CF;&#x4EE5;&#x4E0B;&#xFF1A;</p>
<pre><code class="language-sh">DOM tree \
           --&gt; style tree --&gt; layout --&gt; painting
CSS tree /  &#x2514;&#x2500;----- rendering &lt;--------&#x2518;
</code></pre>
<p>&#x56E0;&#x70BA;&#x901A;&#x5E38;&#x7DB2;&#x7AD9;&#x9084;&#x6703;&#x900F;&#x904E; js &#x6E32;&#x67D3;&#xFF0C;&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F;&#x756B;&#x9762;&#x662F;&#x52D5;&#x614B;&#x7684;&#xFF0C;&#x6703;&#x4E00;&#x76F4;&#x8B8A;&#x5316;&#x3002;</p>
<hr>
<p>&#x7A0B;&#x5F0F;&#x908F;&#x8F2F;&#x6EFF;&#x7C21;&#x55AE;&#x7684;&#xFF0C;&#x9019;&#x908A;&#x53EA;&#x8B1B;&#x90E8;&#x5206; code&#xFF0C;&#x6709;&#x8208;&#x8DA3;&#x53EF;&#x4EE5;&#x4E0A;&#x53BB; <a href="https://github.com/mbrubeck/robinson/blob/master/src/painting.rs" target="_blank">painting.rs</a> &#x770B;&#x4ED6;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#x3002;</p>
<p>&#x56E0;&#x70BA;&#x6211;&#x5011;&#x76EE;&#x7684;&#x662F;&#x8F38;&#x51FA;&#x6210;&#x4E00;&#x500B;&#x300C;&#x756B;&#x9762;&#x300D;&#xFF0C;&#x9019;&#x908A;&#x756B;&#x9762;&#x6211;&#x5011;&#x76F4;&#x63A5;&#x8F38;&#x51FA;&#x6210;&#x5716;&#x50CF;&#x3002;<br>
&#x56E0;&#x6B64;&#x6211;&#x5011;&#x9996;&#x5148;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x756B;&#x5E03;&#xFF0C;&#x7528;&#x4F86;&#x628A;&#x5404;&#x7A2E;&#x5143;&#x7D20;&#x756B;&#x5728;&#x88E1;&#x9762;&#x3002;<br>
&#x76EE;&#x524D;&#x53EA;&#x80FD;&#x756B;&#x51FA;&#x5404;&#x7A2E;&#x77E9;&#x5F62;&#x3002;&#x5305;&#x542B; box &#x7684;&#x5167;&#x90E8;&#x548C;&#x908A;&#x6846;&#x3002;</p>
<pre><code>struct Canvas {
    pixels: Vec&lt;Color&gt;,
    width: usize,
    height: usize,
}

impl Canvas {
    // Create a blank canvas
    fn new(width: usize, height: usize) -&gt; Canvas {
        let white = Color { r: 255, g: 255, b: 255, a: 255 };
        return Canvas {
            pixels: repeat(white).take(width * height).collect(),
            width: width,
            height: height,
        }
    }
    // ...
}
</code></pre>
<p>&#x7528; layout tree &#x5EFA;&#x7ACB;&#x4E00;&#x500B; display tree&#xFF0C;&#x5305;&#x542B;&#x6BCF;&#x500B; node &#x7684;&#x756B;&#x7D20;&#x8CC7;&#x8A0A;</p>
<pre><code>fn build_display_list(layout_root: &amp;LayoutBox) -&gt; DisplayList {
    let mut list = Vec::new();
    render_layout_box(&amp;mut list, layout_root);
    return list;
}

fn render_layout_box(list: &amp;mut DisplayList, layout_box: &amp;LayoutBox) {
    render_background(list, layout_box);
    render_borders(list, layout_box);
    // TODO: render text
    // &#x4F5C;&#x8005;&#x9084;&#x6C92;&#x6709;&#x5C07;&#x986F;&#x793A;&#x6587;&#x5B57;&#x5BEB;&#x9032;&#x53BB;

    for child in &amp;layout_box.children {
        render_layout_box(list, child);
    }
}
</code></pre>
<p>&#x628A;&#x76EE;&#x524D;&#x7684; box &#x6240;&#x5728;&#x7684;&#x4F4D;&#x7F6E;&#x7684;&#x6240;&#x6709;&#x756B;&#x7D20;&#x7684;&#x984F;&#x8272;&#x8A2D;&#x5B9A;&#x597D;&#x3002;</p>
<pre><code>fn paint_item(&amp;mut self, item: &amp;DisplayCommand) {
    match item {
        &amp;DisplayCommand::SolidColor(color, rect) =&gt; {
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
</code></pre>
<p>&#x5F9E; display tree &#x8B80;&#x51FA;&#x6240;&#x6709; box &#x7684;&#x4F4D;&#x7F6E;&#x3001;&#x984F;&#x8272;&#x8CC7;&#x8A0A;&#xFF0C;&#x7136;&#x5F8C;&#x756B;&#x5728;&#x756B;&#x5E03;&#x4E0A;&#x3002;</p>
<pre><code>fn paint(layout_root: &amp;LayoutBox, bounds: Rect) -&gt; Canvas {
    let display_list = build_display_list(layout_root);
    let mut canvas = Canvas::new(bounds.width as usize, bounds.height as usize);
    for item in display_list {
        canvas.paint_item(&amp;item);
    }
    return canvas;
}
</code></pre>
<p>&#x6700;&#x5F8C;&#x5C31;&#x53EF;&#x4EE5;&#x900F;&#x904E; <a href="https://github.com/PistonDevelopers/image/" target="_blank">Rust Image</a> &#x4E4B;&#x985E;&#x7684;&#x51FD;&#x5F0F;&#x5EAB;&#xFF0C;&#x628A;&#x5716;&#x50CF;&#x8F38;&#x51FA;&#x3002;</p>
<pre><code>// Save an image:
let (w, h) = (canvas.width as u32, canvas.height as u32);
let buffer: Vec&lt;image::Rgba&lt;u8&gt;&gt; = unsafe { std::mem::transmute(canvas.pixels) };
let img = image::ImageBuffer::from_fn(w, h, Box::new(|&amp;: x: u32, y: u32| buffer[(y * w + x) as usize]));
let result = image::ImageRgba8(img).save(file, image::PNG);
</code></pre>
<hr>
<p>&#x5047;&#x8A2D;&#x4F60;&#x5BEB;&#x6210;&#x8996;&#x7A97;&#x7A0B;&#x5F0F;&#xFF0C;&#x5C07;&#x7DB2;&#x9801;&#x4EE5;&#x5716;&#x50CF;&#x5448;&#x73FE;&#xFF0C;&#x5C31;&#x662F;&#x6700;&#x967D;&#x6625;&#x7684;&#x700F;&#x89BD;&#x5668;&#x4E86;&#xFF01;<br>
&#x5982;&#x6B64;&#x4E00;&#x4F86;&#xFF0C;&#x5BE6;&#x4F5C;&#x7C21;&#x6613;&#x7248;&#x700F;&#x89BD;&#x5668;&#x7684;&#x7CFB;&#x5217;&#x4E5F;&#x544A;&#x4E00;&#x6BB5;&#x843D;&#xFF01;</p>
<hr>
<blockquote>
<h3><em><strong>&#x95DC;&#x65BC;&#x4F5C;&#x8005;</strong></em></h3>
<h2>&#x5289;&#x5B89;&#x9F4A;</h2>
<p>&#x8EDF;&#x9AD4;&#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x71B1;&#x611B;&#x5BEB;&#x7A0B;&#x5F0F;&#xFF0C;&#x66F4;&#x559C;&#x6B61;&#x63A8;&#x5EE3;&#x7A0B;&#x5F0F;&#x8B93;&#x66F4;&#x591A;&#x4EBA;&#x5B78;&#x6703;</p>
<ul>
<li>
<a href="https://tigercosmos.github.io" target="_blank">&#x500B;&#x4EBA;&#x7DB2;&#x7AD9;</a>
</li>
<li>
<a href="https://github.com/tigercosmos" target="_blank">Github</a>
</li>
<li>
<a href="https://www.facebook.com/CodingNeutrino/" target="_blank">FB&#x7C89;&#x5C08;--&#x5FAE;&#x4E2D;&#x5B50;</a>
</li>
</ul>
</blockquote>
 <br>
                                                    </div>
                    </div>
                
