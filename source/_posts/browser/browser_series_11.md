---
title: 瀏覽器引擎處理版面佈局的簡易版（二）
date: 2017-12-22 23:03:17
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x6628;&#x5929;&#x8A0E;&#x8AD6;&#x4E86;&#x4EC0;&#x9EBC;&#x662F; box&#x3002;&#x7B97;&#x662F;&#x5C0D; layout &#x6709;&#x521D;&#x6B65;&#x8A8D;&#x8B58;&#x4E86;&#x3002;<br>
&#x4ECA;&#x5929;&#x4F86;&#x770B; <a href="https://github.com/mbrubeck/robinson/blob/master/src/layout.rs" target="_blank">robinson/src/layout.rs</a> &#x88E1;&#x9762;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#x3002;</p>
<p>&#x9996;&#x5148;&#x5B9A;&#x7FA9; box &#x7684;&#x6A21;&#x578B;&#xFF0C;&#x5305;&#x542B; x&#x3001;y &#x4F4D;&#x7F6E;&#xFF0C;&#x5BEC;&#x5EA6;&#x3001;&#x9AD8;&#x5EA6;&#x3001;padding&#x3001;margin&#x3001;&#x908A;&#x6846;&#x3002;</p>
<pre><code>#[derive(Clone, Copy, Default, Debug)]
pub struct Rect {
    pub x: f32,
    pub y: f32,
    pub width: f32,
    pub height: f32,
}

#[derive(Clone, Copy, Default, Debug)]
pub struct Dimensions {
    /// Position of the content area relative to the document origin:
    pub content: Rect,
    // Surrounding edges:
    pub padding: EdgeSizes,
    pub border: EdgeSizes,
    pub margin: EdgeSizes,
}

#[derive(Clone, Copy, Default, Debug)]
pub struct EdgeSizes {
    pub left: f32,
    pub right: f32,
    pub top: f32,
    pub bottom: f32,
}
</code></pre>
<hr>
<p>layout tree &#x662F;&#x7531;&#x8A31;&#x591A; box &#x6240;&#x7D44;&#x6210;&#x3002;&#x9019;&#x908A;&#x5B9A;&#x7FA9;&#x4E00;&#x500B; box&#xFF0C;&#x5305;&#x542B;&#x4ED6;&#x7684;&#x6A21;&#x578B;&#x3001;&#x578B;&#x5225;&#x548C;&#x4ED6;&#x7684; child&#x3002;</p>
<pre><code>struct LayoutBox&lt;&apos;a&gt; {
    dimensions: Dimensions,
    box_type: BoxType&lt;&apos;a&gt;,
    children: Vec&lt;LayoutBox&lt;&apos;a&gt;&gt;,
}
</code></pre>
<p>&#x518D;&#x4F86;&#x662F;&#x5B9A;&#x7FA9; box &#x578B;&#x5225;&#xFF0C;&#x4E5F;&#x5C31;&#x662F; CSS &#x7684; deplay&#x3002;<br>
&#x9019;&#x908A;&#x53EA;&#x5B9A;&#x7FA9;&#x4E09;&#x7A2E;&#x578B;&#x5225;&#xFF1A;block&#x3001;inline&#x3001;anonymous<br>
&#x9019;&#x908A;&#x53EF;&#x4EE5;&#x770B;&#x4E00;&#x4E0B; <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/display" target="_blank">Mozilla</a> &#x7684;&#x8AAA;&#x660E;&#x3002;</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>block</td>
<td>The element generates a block element box.</td>
</tr>
<tr>
<td>inline</td>
<td>The element generates one or more inline element boxes.</td>
</tr>
</tbody>
</table>
<p>&#x5982;&#x4E0B;&#x5716;&#x6240;&#x793A;&#xFF08;<a href="https://limpet.net/mbrubeck/2014/09/08/toy-layout-engine-5-boxes.html" target="_blank">&#x4F86;&#x6E90;</a>&#xFF09;<br>
<img src="https://i.imgur.com/zGC9r2f.png" alt></p>
<p>&#x81F3;&#x65BC;&#x4EC0;&#x9EBC;&#x662F; Anonymous &#x53EF;&#x4EE5;&#x770B;&#x4EE5;&#x4E0B;&#x5716;&#x89E3;(<a href="https://www.w3.org/TR/CSS2/visuren.html#anonymous-block-level" target="_blank">&#x4F86;&#x6E90;</a>)&#xFF1A;</p>
<pre><code>&lt;DIV&gt;
  Some text
  &lt;P&gt;More text
&lt;/DIV&gt;
</code></pre>
<p><img src="https://www.w3.org/TR/CSS2/images/anon-block.png" alt></p>
<pre><code>pub enum BoxType&lt;&apos;a&gt; {
    BlockNode(&amp;&apos;a StyledNode&lt;&apos;a&gt;),
    InlineNode(&amp;&apos;a StyledNode&lt;&apos;a&gt;),
    AnonymousBlock,
}
</code></pre>
<hr>
<p>&#x70BA;&#x4E86;&#x8B93; layout tree &#x53D6;&#x5F97; DOM &#x7684; display &#x662F;&#x4EC0;&#x9EBC;&#xFF0C;&#x6211;&#x5011;&#x5728; style &#x7684;&#x6A21;&#x7D44;&#x4E2D;&#x6709;&#x4EE5;&#x4E0B;&#x7684; code &#x4F86;&#x53D6;&#x5F97;&#xFF1A;</p>
<pre><code>enum Display {
    Inline,
    Block,
    None,
}

impl StyledNode {
    // Return the specified value of a property if it exists, otherwise `None`.
    fn value(&amp;self, name: &amp;str) -&gt; Option&lt;Value&gt; {
        self.specified_values.get(name).map(|v| v.clone())
    }

    // The value of the `display` property (defaults to inline).
    fn display(&amp;self) -&gt; Display {
        match self.value(&quot;display&quot;) {
            Some(Keyword(s)) =&gt; match &amp;*s {
                &quot;block&quot; =&gt; Display::Block,
                &quot;none&quot; =&gt; Display::None,
                _ =&gt; Display::Inline
            },
            _ =&gt; Display::Inline
        }
    }
}
</code></pre>
<hr>
<p>&#x63A5;&#x8457;&#x5C31;&#x53EF;&#x4EE5;&#x4F86;&#x5EFA;&#x7ACB;&#x7528; style tree &#x5EFA;&#x7ACB; layout tree&#x3002;<br>
&#x9806;&#x8457; root &#x4E0D;&#x65B7;&#x905E;&#x8FF4;&#x628A;&#x6A39;&#x5EFA;&#x69CB;&#x8D77;&#x4F86;&#x3002;<br>
&#x5982;&#x679C; display &#x662F; none &#x7684;&#x7BC0;&#x9EDE;&#x5247;&#x4E0D;&#x5217;&#x5165;&#x8A08;&#x7B97;&#x3002;</p>
<pre><code>/// Transform a style tree into a layout tree.
pub fn layout_tree&lt;&apos;a&gt;(node: &amp;&apos;a StyledNode&lt;&apos;a&gt;, mut containing_block: Dimensions) -&gt; LayoutBox&lt;&apos;a&gt; {
    // The layout algorithm expects the container height to start at 0.
    containing_block.content.height = 0.0;

    let mut root_box = build_layout_tree(node);
    root_box.layout(containing_block);
    root_box
}

/// Build the tree of LayoutBoxes, but don&apos;t perform any layout calculations yet.
fn build_layout_tree&lt;&apos;a&gt;(style_node: &amp;&apos;a StyledNode&lt;&apos;a&gt;) -&gt; LayoutBox&lt;&apos;a&gt; {
    // Create the root box.
    let mut root = LayoutBox::new(match style_node.display() {
        Display::Block =&gt; BlockNode(style_node),
        Display::Inline =&gt; InlineNode(style_node),
        Display::None =&gt; panic!(&quot;Root node has display: none.&quot;)
    });

    // Create the descendant boxes.
    for child in &amp;style_node.children {
        match child.display() {
            Display::Block =&gt; root.children.push(build_layout_tree(child)),
            Display::Inline =&gt; root.get_inline_container().children.push(build_layout_tree(child)),
            Display::None =&gt; {} // Don&apos;t lay out nodes with `display: none;`
        }
    }
    root
}
</code></pre>
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
                
