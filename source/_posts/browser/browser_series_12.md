---
title: 瀏覽器引擎處理版面佈局的簡易版（三）
date: 2017-12-23 23:31:29
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x63A5;&#x7E8C;&#x6628;&#x5929;&#x8A0E;&#x8AD6; <a href="https://github.com/mbrubeck/robinson/blob/master/src/layout.rs" target="_blank">robinson/src/layout.rs</a> &#x9019;&#x500B; layout &#x6A21;&#x7D44;&#x3002;</p>
<p>&#x4E00;&#x822C;&#x4F86;&#x8AAA;&#xFF0C;box &#x662F;&#x5F9E;&#x4E0A;&#x5230;&#x4E0B;&#x5806;&#x8D77;&#x4F86;&#x7684;&#xFF0C;&#x5982;&#x679C;&#x6709;&#x5B9A;&#x7FA9;&#x662F; inline &#x7684;&#x8A71;&#xFF0C;&#x5247;&#x662F;&#x5F9E;&#x5DE6;&#x5230;&#x53F3;&#x3002;&#x4E0D;&#x904E;&#x9019;&#x662F;&#x5728; Normal flow &#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6C92;&#x6709;&#x5B9A;&#x7FA9;&#x300C;<a href="https://www.w3.org/TR/CSS2/visuren.html#positioning-scheme" target="_blank">&#x4F4D;&#x7F6E;</a>&#x300D;&#xFF0C;&#x4E0D;&#x7136;&#x4F60;&#x4E5F;&#x53EF;&#x4EE5;&#x8B93;&#x67D0;&#x500B; box &#x56FA;&#x5B9A;&#x5728;&#x90A3;&#x908A;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x4E0D;&#x6703;&#x53D7;&#x4EFB;&#x4F55;&#x6771;&#x897F;&#x5F71;&#x97FF;&#x4ED6;&#x7684;&#x4F4D;&#x7F6E;&#xFF0C;&#x6216;&#x662F;&#x8B93;&#x67D0;&#x500B; box &#x5F9E;&#x53F3;&#x908A;&#x5C0D;&#x9F4A;&#x3002;</p>
<hr>
<p>LayoutBox &#x7B97;&#x51FA; layout &#x7684;&#x521D;&#x59CB;&#x51FD;&#x6578;&#xFF0C;&#x91DD;&#x5C0D;&#x81EA;&#x5DF1;&#x662F;&#x90A3;&#x7A2E;&#x578B;&#x5225;&#x4F86;&#x958B;&#x59CB;&#xFF0C;&#x9019;&#x500B;&#x5C08;&#x6848;&#x4E2D;&#x76EE;&#x524D;&#x53EA;&#x5BE6;&#x4F5C; block&#x3002;<br>
&#x6240;&#x4EE5;&#x4EE5;&#x4E0B;&#x90FD;&#x662F;&#x91DD;&#x5C0D; block &#x7684;&#x7B97;&#x6CD5;&#x505A;&#x89E3;&#x91CB;&#x3002;</p>
<pre><code>// implimpl&lt;&apos;a&gt; LayoutBox&lt;&apos;a&gt;

    /// Lay out a box and its descendants.
    fn layout(&amp;mut self, containing_block: Dimensions) {
        match self.box_type {
            BlockNode(_) =&gt; self.layout_block(containing_block),
            InlineNode(_) | AnonymousBlock =&gt; {} // TODO
        }
    }
</code></pre>
<hr>
<p>&#x4E00;&#x500B; box &#x5BE6;&#x969B;&#x5927;&#x5C0F;&#x9AD8;&#x5EA6;&#x6703;&#x53D7;&#x5B50;&#x5F71;&#x97FF;&#xFF0C;&#x800C;&#x81EA;&#x5DF1;&#x7684;&#x5BEC;&#x5EA6;&#x6703;&#x9650;&#x5236;&#x5B50;&#x7684;&#x6392;&#x5217;&#x3002;</p>
<p>&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x89E3;&#x91CB;&#xFF1A;</p>
<pre><code>&lt;A hieght = 100&gt;
    &lt;a heught = 200&gt;
&lt;/A&gt;
</code></pre>
<p>&#x9019;&#x6A23;&#x7684;&#x8A71; <code>A</code> &#x7684;&#x5BE6;&#x969B;&#x9AD8;&#x5EA6;&#x6703;&#x662F; 200&#xFF0C;&#x7576;&#x7136;&#x5982;&#x679C;&#x6709;&#x8A2D;&#x5B9A;&#x5176;&#x4ED6;&#x7684;&#x5C6C;&#x6027;&#x7684;&#x8A71;&#xFF0C;&#x4F8B;&#x5982;&#x8A2D;&#x5B9A; <code>A</code> &#x53EA;&#x986F;&#x793A;&#x5B9A;&#x7FA9;&#x7684;&#x9AD8;&#x5EA6;&#xFF0C;&#x90A3;&#x9EBC; <code>a</code> &#x5C31;&#x6703;&#x6709;&#x4E00;&#x534A;&#x4E0D;&#x6703;&#x986F;&#x793A;&#x51FA;&#x4F86;&#x3002;</p>
<pre><code>&lt;B width = 100&gt;
    &lt;b width = 70&gt;
    &lt;c width = 40&gt;
&lt;/B&gt;
</code></pre>
<p><code>B</code> &#x7684;&#x7684;&#x5BEC;&#x5EA6;&#x662F; 100&#xFF0C;&#x96D6;&#x7136; <code>b</code> &#x548C; <code>c</code> &#x52A0;&#x8D77;&#x4F86;&#x8D85;&#x904E;&#x4E86;&#xFF0C;&#x4F46;&#x4ED6;&#x7684;&#x5BEC;&#x5EA6;&#x4F9D;&#x820A;&#x662F; 100&#x3002;</p>
<p>&#x4E86;&#x89E3;&#x4E86;&#x4E0A;&#x9762;&#x7684;&#x6982;&#x5FF5;&#x5F8C;&#x4E4B;&#x5F8C;&#x6211;&#x5011;&#x958B;&#x59CB;&#x5BE6;&#x4F5C;</p>
<hr>
<p>&#x9019;&#x908A;&#x6392;&#x7248;&#x4E00;&#x500B; block box &#x7684;&#x505A;&#x6CD5;&#xFF1A;</p>
<pre><code>fn layout_block(&amp;mut self, containing_block: Dimensions) {
    // &#x5B50;&#x53D7;&#x7236;&#x7684;&#x5BEC;&#x5EA6;&#x5F71;&#x97FF;
    self.calculate_block_width(containing_block);

    // &#x6C7A;&#x5B9A;&#x9019;&#x500B; box &#x7684;&#x4F4D;&#x7F6E;
    self.calculate_block_position(containing_block);

    // &#x628A;&#x5E95;&#x4E0B;&#x7684;&#x5B50;&#x7B97;&#x4E00;&#x4E0B;
    self.layout_block_children();

    // &#x7236;&#x7684;&#x9AD8;&#x5EA6;&#x53D7;&#x5B50;&#x5F71;&#x97FF;&#xFF0C;&#x6240;&#x4EE5;&#x8981;&#x7B49;&#x5B50;&#x7B97;&#x5B8C;&#x624D;&#x5F97;&#x5230;&#x7236;
    self.calculate_block_height();
}
</code></pre>
<p>&#x5982;&#x679C;&#x5B50;&#x5167;&#x5BB9;&#x8D85;&#x904E;&#x7236;&#xFF0C;&#x662F;&#x70BA; overflow&#x3002;&#x53CD;&#x4E4B;&#x5B50;&#x5167;&#x5BB9;&#x6BD4;&#x7236;&#x5167;&#x5BB9;&#x5C11;&#xFF0C;&#x662F;&#x70BA; underflow&#x3002;<br>
&#x5728; auto &#x6A21;&#x5F0F;&#x4E0B;&#xFF0C; normal flow &#x8655;&#x7406; block &#x7684;&#x6642;&#x5019;&#xFF0C;&#x6709;&#x4E00;&#x5957;<a href="https://www.w3.org/TR/CSS2/visudet.html#blockwidth" target="_blank">&#x6F14;&#x7B97;&#x6CD5;</a>&#x4F86;&#x60F3;&#x8FA6;&#x6CD5;&#x76E1;&#x91CF;&#x8B93;&#x5B50;&#x5143;&#x7D20;&#x7B26;&#x5408;&#x7236;&#x3002;<br>
&#x4E5F;&#x5C31;&#x662F;&#x85C9;&#x7531;&#x8ABF;&#x6574;&#x5927;&#x5BB6;&#x7684; margin &#x4F86;&#x9054;&#x5230;&#x76EE;&#x7684;&#x3002;<br>
&#x4F8B;&#x5982;&#x5B50;&#x5143;&#x7D20;&#x8D85;&#x904E;&#x7236;&#x5143;&#x7D20;&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x628A;&#x5B50;&#x5143;&#x7D20;&#x7684; margin &#x62FF;&#x6389;&#xFF0C;&#x5C31;&#x543B;&#x5408;&#x4E86;&#x3002;<br>
&#x6216;&#x8457;&#x662F;&#x5B50;&#x5143;&#x7D20;&#x586B;&#x4E0D;&#x6EFF;&#x7236;&#x5143;&#x7D20;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x5C31;&#x628A;&#x5B50;&#x5143;&#x7D20;&#x7684; margin &#x52A0;&#x9577;&#x3002;</p>
<pre><code>// Calculate the width of a block-level non-replaced element in normal flow.
// Sets the horizontal margin/padding/border dimensions, and the `width`.
fn calculate_block_width(&amp;mut self, containing_block: Dimensions) {
    ...
}
</code></pre>
<p>&#x5C07;&#x5B50;&#x5143;&#x7D20;&#x548C;&#x81EA;&#x5DF1;&#x672C;&#x8EAB;&#x7684;&#x5167;&#x5BB9;&#x5340;&#x57DF;&#x9032;&#x884C;&#x6392;&#x7248;</p>
<pre><code>fn layout_block_children(&amp;mut self) {
    // &#x5C07; `self.dimensions.height` &#x8A2D;&#x70BA;&#x5168;&#x90E8;&#x5167;&#x5BB9;&#x52A0;&#x8D77;&#x4F86;&#x7684;&#x7E3D;&#x9AD8;&#x5EA6;
    let d = &amp;mut self.dimensions;
    for child in &amp;mut self.children {
        child.layout(*d);
        // &#x628A;&#x6240;&#x6709;&#x5B50;&#x5143;&#x7D20;&#x7684;&#x9AD8;&#x5EA6;&#x76F8;&#x52A0;
        d.content.height = d.content.height + child.dimensions.margin_box().height;
    }
}
</code></pre>
<p>&#x9019;&#x908A;&#x6982;&#x5FF5;&#x6EFF;&#x7C21;&#x55AE;&#x7684;&#xFF0C;&#x5982;&#x679C;&#x9AD8;&#x5EA6;&#x6709;&#x5B9A;&#x7FA9;&#xFF0C;&#x4ED6;&#x5C31;&#x662F;&#x90A3;&#x9EBC;&#x9AD8;&#xFF0C;&#x4E0D;&#x7136;&#x5C31;&#x7531;&#x5167;&#x5BB9;&#x9AD8;&#x5EA6;&#x6C7A;&#x5B9A;</p>
<pre><code>    /// Height of a block-level non-replaced element in normal flow with overflow visible.
    fn calculate_block_height(&amp;mut self) {
        // If the height is set to an explicit length, use that exact length.
        // Otherwise, just keep the value set by `layout_block_children`.
        if let Some(Length(h, Px)) = self.get_style_node().value(&quot;height&quot;) {
            self.dimensions.content.height = h;
        }
}
</code></pre>
<p>&#x5982;&#x4F55;&#x7B97;&#x51FA;&#x4F4D;&#x7F6E;&#x5462;&#xFF1F;&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F;&#x53D6;&#x5F97;&#x5148;&#x524D; box &#x7684;&#x4F4D;&#x7F6E;&#xFF0C;&#x5728;&#x91DD;&#x5C0D;&#x81EA;&#x5DF1;&#x7684; margin&#x3001;padding &#x4F5C;&#x8655;&#x7406;&#xFF0C;&#x56E0;&#x70BA;&#x6211;&#x5011;&#x7684;&#x4F4D;&#x7F6E;&#x662F;&#x91DD;&#x5C0D;&#x6700;&#x88E1;&#x9762;&#x7684; comtent area &#x4F86;&#x8A02;&#x3002;&#xFF08;&#x610F;&#x601D;&#x5C31;&#x662F;&#x908A;&#x908A;&#x96D6;&#x7136;&#x96D6;&#x7136;&#x4F54;&#x9762;&#x7A4D;&#xFF0C;&#x4F46;&#x5143;&#x7D20;&#x7684;&#x539F;&#x9EDE;&#x662F;&#x5728; cotent area&#xFF09;</p>
<pre><code>    fn calculate_block_position(&amp;mut self, containing_block: Dimensions) {
        let style = self.get_style_node();
        let d = &amp;mut self.dimensions;

        // margin, border, and padding have initial value 0.
        let zero = Length(0.0, Px);

        // If margin-top or margin-bottom is `auto`, the used value is zero.
        d.margin.top = style.lookup(&quot;margin-top&quot;, &quot;margin&quot;, &amp;zero).to_px();
        d.margin.bottom = style.lookup(&quot;margin-bottom&quot;, &quot;margin&quot;, &amp;zero).to_px();

        d.border.top = style.lookup(&quot;border-top-width&quot;, &quot;border-width&quot;, &amp;zero).to_px();
        d.border.bottom = style.lookup(&quot;border-bottom-width&quot;, &quot;border-width&quot;, &amp;zero).to_px();

        d.padding.top = style.lookup(&quot;padding-top&quot;, &quot;padding&quot;, &amp;zero).to_px();
        d.padding.bottom = style.lookup(&quot;padding-bottom&quot;, &quot;padding&quot;, &amp;zero).to_px();

        d.content.x = containing_block.content.x +
                      d.margin.left + d.border.left + d.padding.left;

        // Position the box below all the previous boxes in the container.
        d.content.y = containing_block.content.height + containing_block.content.y +
                      d.margin.top + d.border.top + d.padding.top;
}
</code></pre>
<hr>
<p>&#x5C31;&#x7531;&#x4EE5;&#x4E0A;&#x7684;&#x7A0B;&#x5F0F;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x628A;&#x4E00;&#x500B;&#x4E00;&#x500B;&#x7684; box &#x5806;&#x758A;&#x8D77;&#x4F86;&#x3002;<br>
&#x800C;&#x7DB2;&#x9801;&#x672C;&#x8EAB;&#x5C31;&#x662F;&#x4E00;&#x5806;&#x7684; box &#x5806;&#x4F86;&#x5806;&#x53BB;&#x3002;&#x73FE;&#x5728;&#x4F60;&#x77E5;&#x9053;&#x5982;&#x4F55;&#x505A;&#x4E86;&#xFF01;<br>
&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
