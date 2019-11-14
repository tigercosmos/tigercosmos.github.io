---
title: 瀏覽器引擎處理 HTML 的簡易版
date: 2017-12-15 22:43:03
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x9019;&#x7BC7;&#x4E00;&#x6A23;&#x4F7F;&#x7528; <a href="https://github.com/mbrubeck/robinson" target="_blank">robinson</a> &#x9019;&#x500B;&#x300C;&#x73A9;&#x5177;&#x300D;&#x4F86;&#x9032;&#x884C;&#x8B1B;&#x89E3;&#xFF0C;&#x9084;&#x8A18;&#x5F97;&#x6211;&#x5011;&#x7B2C;&#x4E8C;&#x7BC7;&#x6587;&#x7AE0;&#x4E2D;&#x63D0;&#x5230;&#x89E3;&#x6790;&#x7684;&#x90E8;&#x5206;&#x55CE;&#xFF1F;&#x5206;&#x70BA; HTML &#x548C; CSS &#x89E3;&#x6790;&#x3002;&#x5FD8;&#x8A18;&#x7684;&#x8A71;&#x3001;&#x6216;&#x662F;&#x4E4B;&#x524D;&#x5077;&#x61F6;&#x6C92;&#x770B;&#x7684;&#x8A71;&#xFF0C;&#x53EF;&#x4EE5;&#x56DE;&#x53BB;&#x770B;&#x4E00;&#x4E0B;&#xFF0C;&#x90A3;&#x7BC7;&#x89E3;&#x91CB;&#x700F;&#x89BD;&#x5668;&#x5982;&#x4F55;&#x9032;&#x884C;&#x89E3;&#x6790;&#xFF0C;&#x300C;How browser work&#x300D;&#x4E00;&#x7BC7;&#x6587;&#x7AE0;&#x66F4;&#x662F;&#x5C0D;&#x539F;&#x7406;&#x8B1B;&#x5F97;&#x975E;&#x5E38;&#x4ED4;&#x7D30;&#xFF0C;&#x8B80;&#x61C2;&#x539F;&#x7406;&#x624D;&#x80FD;&#x77E5;&#x9053;&#x9019;&#x7BC7;&#x5728;&#x505A;&#x4EC0;&#x9EBC;&#x3002;</p>
<p>&#x6211;&#x5011;&#x77E5;&#x9053;&#x5982;&#x4F55;&#x8655;&#x7406;&#x4E00;&#x500B; DOM &#x4E86;&#xFF0C;&#x63A5;&#x4E0B;&#x4F86;&#x6211;&#x5011;&#x8981;&#x4F86;&#x89E3;&#x6790; HTML &#x672C;&#x8EAB;&#x4E86;&#xFF01;&#x89E3;&#x6790;&#x597D;&#x7684; HTML &#x4FBF;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;&#x6211;&#x5011;&#x6628;&#x5929;&#x5BEB;&#x597D;&#x7684; DOM &#x6A21;&#x7D44;&#x4F86;&#x7D44;&#x88DD;&#x3002;&#x9019;&#x6A23;&#x4E00;&#x4F86;&#x5C31;&#x5B8C;&#x6210; DOM Tree &#x7684;&#x90E8;&#x5206;&#x4E86;&#xFF01;</p>
<p>robinson &#x95DC;&#x65BC; html &#x7684;&#x90E8;&#x5206;&#x5728; <a href="https://github.com/mbrubeck/robinson/blob/master/src/html.rs" target="_blank">robinson/src/html.rs</a>&#x3002;&#x7A0B;&#x5F0F;&#x78BC;&#x4E5F;&#x4E0D;&#x7B97;&#x592A;&#x9577;&#xFF0C;&#x6BD4;&#x6628;&#x5929;&#x7A0D;&#x5FAE;&#x671D;&#x4E00;&#x9EDE;&#x9EDE;&#x800C;&#x5DF2;&#x3002;</p>
<p>&#x73A9;&#x5177;&#x7576;&#x7136;&#x7121;&#x6CD5;&#x6EFF;&#x8DB3;&#x6211;&#x5011;&#xFF0C;&#x6211;&#x5011;&#x6700;&#x7D42;&#x7684;&#x76EE;&#x6A19;&#x662F;&#x8981;&#x53BB;&#x6311;&#x6230; Servo &#x5C08;&#x6848;&#xFF0C;&#x9019;&#x908A;&#x5148;&#x544A;&#x8A34;&#x5927;&#x5BB6;&#xFF0C;Servo &#x7684; html parser &#x662F; <a href="https://github.com/servo/html5ever" target="_blank">html5ever</a>&#xFF0C;&#x5176;&#x5BE6;&#x505A;&#x539F;&#x7406;&#x4E5F;&#x662F;&#x7167;&#x8457; SPEC &#x4F86;&#x5B8C;&#x6210;&#x7684;&#xFF0C;&#x88AB;&#x7368;&#x7ACB;&#x51FA;&#x4F86;&#x4F5C;&#x70BA;&#x4E00;&#x500B;&#x6A21;&#x7D44;&#x3002;&#x610F;&#x601D;&#x662F;&#x4ED6;&#x4E0D;&#x662F;&#x5305;&#x542B;&#x5728; Servo &#x88E1;&#x9762;&#xFF0C;&#x5047;&#x8A2D;&#x4F60;&#x4E5F;&#x7528; Rust &#x8A9E;&#x8A00;&#x5BEB;&#x4E00;&#x500B;&#x300C;&#x73A9;&#x5177;&#x700F;&#x89BD;&#x5668;&#x300D;&#xFF0C;&#x4F60;&#x53EF;&#x4EE5;&#x5B8C;&#x5168;&#x4F7F;&#x7528;&#x9019;&#x500B;&#x5957;&#x4EF6;&#x4F86;&#x5B8C;&#x6210; html &#x7684;&#x89E3;&#x6790;&#x3002;&#x628A;&#x6642;&#x9593;&#x82B1;&#x5728;&#x66F4;&#x60F3;&#x5BE6;&#x4F5C;&#x7DF4;&#x7FD2;&#x7684;&#x9805;&#x76EE;&#x4E0A;&#xFF01;</p>
<h2>&#x5BE6;&#x4F5C;</h2>
<p>&#x4EE5;&#x4E0B;&#x70BA;&#x6211;&#x76F4;&#x63A5;&#x8907;&#x88FD; <a href="https://github.com/mbrubeck/robinson/blob/master/src/html.rs" target="_blank"><code>html.rs</code></a> &#x904E;&#x4F86;&#xFF0C;&#x4E26;&#x62C6;&#x89E3;&#x6210;&#x7247;&#x6BB5;&#x4F86;&#x89E3;&#x91CB;&#x5728;&#x505A;&#x4EC0;&#x9EBC;&#x3002;<br>
&#x5EFA;&#x8B70;&#x5148;&#x53BB;&#x770B;&#x539F;&#x59CB;&#x78BC;&#xFF0C;&#x5927;&#x6982;&#x610F;&#x6703;&#x4E00;&#x4E0B;&#x539F;&#x59CB;&#x7A0B;&#x5F0F;&#x78BC;&#x7684;&#x60F3;&#x6CD5;&#x3002;&#x518D;&#x4F86;&#x770B;&#x6211;&#x7684;&#x89E3;&#x8AAA;&#x3002;<br>
&#x7A0B;&#x5F0F;&#x7684;&#x4F5C;&#x8005;&#x4E5F;&#x6709;&#x5BEB;<a href="https://limpet.net/mbrubeck/2014/08/11/toy-layout-engine-2.html" target="_blank">&#x6587;&#x7AE0;</a>&#x89E3;&#x91CB;&#xFF0C;&#x4F46;&#x6211;&#x7684;&#x7D55;&#x5C0D;&#x6BD4;&#x4ED6;&#x7684;&#x66F4;&#x8A73;&#x7D30;&#xFF0C;&#x7576;&#x7136;&#x9084;&#x662F;&#x4E2D;&#x6587;&#x7684; X)<br>
&#x539F;&#x59CB;&#x7A0B;&#x5F0F;&#x78BC;&#x7684;&#x8A3B;&#x89E3;&#x548C;&#x4E00;&#x4E9B;&#x6211;&#x89BA;&#x5F97;&#x4E0D;&#x7528;&#x7279;&#x5225;&#x89E3;&#x8AAA;&#x7684;&#x90E8;&#x5206;&#x9019;&#x908A;&#x6709;&#x62FF;&#x6389;&#x3002;&#x9019;&#x908A;&#x53EA;&#x6311;&#x51FA;&#x95DC;&#x9375;&#x7684;&#x908F;&#x8F2F;&#x90E8;&#x5206;&#x3002;<br>
&#x9019;&#x6BB5;&#x7A0B;&#x5F0F;&#x78BC;&#x6709;&#x4E00;&#x4E9B;&#x4F7F;&#x7528; Rust &#x8A9E;&#x8A00;&#x7684;&#x7279;&#x6027;&#xFF0C;&#x4E0D;&#x5F71;&#x97FF;&#x908F;&#x8F2F;&#x7406;&#x89E3;&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x60F3;&#x5B8C;&#x5168;&#x77AD;&#x89E3;&#x7A0B;&#x5F0F;&#x78BC;&#x7684;&#x904B;&#x4F5C;&#x904E;&#x7A0B;&#xFF0C;&#x6700;&#x597D;&#x9084;&#x662F;&#x53BB;&#x4E86;&#x89E3;&#x4E00;&#x4E0B; Rust &#x7684;&#x4F7F;&#x7528;&#x65B9;&#x5F0F;&#x3002;</p>
<p>&#x597D;&#x5566;&#xFF01;&#x6211;&#x5011;&#x4E0A;&#x8DEF;&#xFF01;</p>
<hr>
<pre><code>// &#x6628;&#x5929;&#x6211;&#x5011;&#x5BE6;&#x4F5C;&#x7684; DOM &#x9019;&#x908A;&#x5C31;&#x62FF;&#x4F86;&#x4F7F;&#x7528;
use dom;
// &#x7528;&#x4F86;&#x5132;&#x5B58;&#x8CC7;&#x6599;
use std::collections::HashMap;
</code></pre>
<p>&#x7528;&#x6211;&#x5011;&#x5BEB;&#x597D;&#x7684; Parser &#x4F86;&#x9032;&#x884C;&#x89E3;&#x6790;&#xFF0C;&#x5176;&#x4E2D; <code>dom::elem()</code> &#x662F;&#x6211;&#x5011;&#x6628;&#x5929;&#x5B9A;&#x7FA9;&#x7684;&#x51FD;&#x793A;&#xFF0C;&#x89E3;&#x6790;&#x5B8C; HTML &#x5C31;&#x53EF;&#x4EE5;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x65B0;&#x7684; DOM&#x3002;Parser &#x7684;&#x5BE6;&#x4F5C;&#x5728;&#x4E0B;&#x9762;&#x3002;</p>
<pre><code>pub fn parse(source: String) -&gt; dom::Node {
    let mut nodes = Parser { pos: 0, input: source }.parse_nodes();

    // &#x5982;&#x679C;&#x7BC0;&#x9EDE;&#x53EA;&#x6709;&#x4E00;&#x500B;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6839;&#x7BC0;&#x9EDE;&#xFF0C;&#x5C31;&#x8FD4;&#x56DE;
    if nodes.len() == 1 {
        nodes.swap_remove(0)
    // &#x4E0D;&#x7136;&#x5C31;&#x5EFA;&#x7ACB;&#x7BC0;&#x9EDE;
    } else {
        dom::elem(&quot;html&quot;.to_string(), HashMap::new(), nodes)
    }
}
</code></pre>
<p>&#x5EFA;&#x7ACB;&#x4E00;&#x500B; Class &#x53EB;&#x505A; Parser&#xFF0C;&#x4F60;&#x53EF;&#x4EE5;&#x5B8C;&#x5168;&#x4E0D;&#x8981;&#x9019;&#x6A23;&#x5BEB;&#xFF0C;&#x9019;&#x908A;&#x53EA;&#x662F;&#x4E00;&#x7A2E;&#x53EF;&#x884C;&#x7684;&#x65B9;&#x5F0F;</p>
<pre><code>struct Parser {
    pos: usize,
    input: String,
}
</code></pre>
<p>Parser &#x7684; method</p>
<pre><code>impl Parser {
    ...
    ...
}
</code></pre>
<hr>
<p><em><strong>&#x4EE5;&#x4E0B;&#x662F; Parser &#x7684; Methods</strong></em></p>
<p>&#x9019;&#x908A;&#x628A;&#x6240;&#x6709;&#x5B50;&#x7BC0;&#x9EDE;&#x90FD;&#x89E3;&#x6790;&#x9032;&#x4F86;</p>
<pre><code>    /// Parse a sequence of sibling nodes.
    fn parse_nodes(&amp;mut self) -&gt; Vec&lt;dom::Node&gt; {
        let mut nodes = vec!();
        loop {
            self.consume_whitespace();
            if self.eof() || self.starts_with(&quot;&lt;/&quot;) {
                break;
            }
            nodes.push(self.parse_node());
        }
        nodes
    }
</code></pre>
<p>&#x5224;&#x65B7;&#x89E3;&#x6790;&#x7684;&#x7BC0;&#x9EDE;&#x662F;&#x5143;&#x7D20;&#x9084;&#x662F;&#x6587;&#x5B57;&#x7BC0;&#x9EDE;&#x3002;&#x5982;&#x679C;&#x662F;&#x6587;&#x5B57;&#x7BC0;&#x9EDE;&#x5C31;&#x6703;&#x8005;&#x7684;&#x50CF;&#x662F;&#xFF0C;<code>&lt;h1&gt;Tiltle&lt;/h1&gt;</code>&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x88E1;&#x9762;&#x53EA;&#x6709;&#x6587;&#x5B57;&#xFF0C;&#x6240;&#x4EE5;&#x9019;&#x908A;&#x7528;<code>&lt;</code>&#x4F86;&#x5224;&#x65B7;&#x662F;&#x4EC0;&#x9EBC;&#x7BC0;&#x9EDE;&#x3002;&#x7576;&#x7136;&#x56E0;&#x70BA;&#x9019;&#x908A;&#x5047;&#x8A2D;&#x53EA;&#x6709;&#x5169;&#x7A2E;&#x7BC0;&#x9EDE;&#x578B;&#x614B;&#x624D;&#x80FD;&#x9019;&#x6A23;&#x505A;&#x3002;</p>
<pre><code>    /// Parse a single node.
    fn parse_node(&amp;mut self) -&gt; dom::Node {
        match self.next_char() {
            &apos;&lt;&apos; =&gt; self.parse_element(),
            // &#x5728; Rust &#x4E2D;&#xFF0C;_ &#x4EE3;&#x8868;&#x5176;&#x9918;&#x72C0;&#x6CC1;&#xFF0C;&#x6216;&#x662F;&#x8A2D;&#x5B9A;&#x503C;&#x70BA;&#x7A7A;
            _   =&gt; self.parse_text()
        }
    }
</code></pre>
<p>&#x89E3;&#x6790;&#x4E00;&#x500B;&#x5143;&#x7D20;&#xFF0C;&#x9019;&#x908A;&#x628A;&#x6AA2;&#x67E5;&#x4E00;&#x8D77;&#x5BEB;&#x9032;&#x4F86;&#x4E86;&#xFF0C;&#x6B63;&#x5F0F;&#x7684;&#x7522;&#x54C1;&#x4E0D;&#x5EFA;&#x8B70;&#x9019;&#x6A23;&#x505A;&#xFF0C;&#x6700;&#x597D;&#x662F;&#x80FD;&#x5920;&#x628A;&#x6E2C;&#x8A66;&#x5206;&#x96E2;&#x3002;<br>
&#x4E00;&#x500B;&#x5143;&#x7D20;&#x5927;&#x6982;&#x9577;&#x9019;&#x6A23;:</p>
<pre><code class="language-html">&lt;div&gt;
    &lt;p&gt; Hello &lt;/p&gt;
&lt;/div&gt;
</code></pre>
<p>&#x7136;&#x5F8C;&#x4F60;&#x518D;&#x770B;&#x4E00;&#x4E0B;&#x9019;&#x908A;&#x89E3;&#x6790;&#x5143;&#x7D20;&#x4F5C;&#x7684;&#x90E8;&#x5206;&#xFF0C;&#x5C31;&#x80FD;&#x660E;&#x767D;&#x70BA;&#x5565;&#x8981;&#x6709;&#x4E09;&#x500B;&#x6B65;&#x9A5F;&#x3002;</p>
<pre><code>    /// Parse a single element, including its open tag, contents, and closing tag.
    fn parse_element(&amp;mut self) -&gt; dom::Node {
        // Opening tag.
        assert_eq!(self.consume_char(), &apos;&lt;&apos;);
        let tag_name = self.parse_tag_name();
        let attrs = self.parse_attributes();
        assert_eq!(self.consume_char(), &apos;&gt;&apos;);

        // Contents.
        let children = self.parse_nodes();

        // Closing tag.
        assert_eq!(self.consume_char(), &apos;&lt;&apos;);
        assert_eq!(self.consume_char(), &apos;/&apos;);
        assert_eq!(self.parse_tag_name(), tag_name);
        assert_eq!(self.consume_char(), &apos;&gt;&apos;);

        dom::elem(tag_name, attrs, children)
    }
</code></pre>
<p>&#x9019;&#x908A;&#x8A8D;&#x5B9A; <code>tag</code> &#x7684;&#x540D;&#x7A31;&#x53EA;&#x6703;&#x6709;&#x82F1;&#x6587;&#x548C;&#x6578;&#x5B57;</p>
<pre><code>    /// Parse a tag or attribute name.
    fn parse_tag_name(&amp;mut self) -&gt; String {
        self.consume_while(|c| match c {
            &apos;a&apos;...&apos;z&apos; | &apos;A&apos;...&apos;Z&apos; | &apos;0&apos;...&apos;9&apos; =&gt; true,
            _ =&gt; false
        })
    }
</code></pre>
<p>Attibutes &#x5C31;&#x50CF;&#x662F; <code>class=&quot;btn red box&quot;</code>&#xFF0C;&#x6703;&#x7528;&#x7A7A;&#x767D;&#x9694;&#x958B;&#xFF0C;&#x6240;&#x4EE5;&#x9019;&#x908A;&#x89E3;&#x6790;&#x5C6C;&#x6027;&#x6642;&#xFF0C;&#x5C07;&#x5C6C;&#x6027;&#x5167;&#x5BB9;&#x7528;&#x7A7A;&#x767D;&#x5207;&#x958B;&#xFF0C;&#x8DD1;&#x56DE;&#x5708;&#x4F86;&#x8A18;&#x9304;&#x3002;</p>
<pre><code>    /// Parse a list of name=&quot;value&quot; pairs, separated by whitespace.
    fn parse_attributes(&amp;mut self) -&gt; dom::AttrMap {
        let mut attributes = HashMap::new();
        loop {
            self.consume_whitespace();
            if self.next_char() == &apos;&gt;&apos; {
                break;
            }
            let (name, value) = self.parse_attr();
            attributes.insert(name, value);
        }
        attributes
    }
</code></pre>
<p>&#x53EA;&#x8655;&#x7406;&#x5143;&#x7D20;&#x7684; <code>name</code>&#xFF0C;&#x50CF;&#x662F; <code>&lt;input name=&quot;upload&quot;&gt;</code> &#x9019;&#x7A2E;&#x3002;</p>
<pre><code>    /// Parse a single name=&quot;value&quot; pair.
    fn parse_attr(&amp;mut self) -&gt; (String, String) {
        let name = self.parse_tag_name();
        assert_eq!(self.consume_char(), &apos;=&apos;);
        let value = self.parse_attr_value();
        (name, value)
    }
</code></pre>
<p>&#x89E3;&#x6790;&#x6587;&#x5B57;&#x7BC0;&#x9EDE;&#xFF0C;&#x4E0A;&#x9762;&#x6709;&#x63D0;&#x904E;&#xFF0C;&#x7BC0;&#x9EDE;&#x5167;&#x4E0D;&#x8A72;&#x6709;<code>&lt;</code>&#x5B58;&#x5728;</p>
<pre><code>    /// Parse a text node.
    fn parse_text(&amp;mut self) -&gt; dom::Node {
        dom::text(self.consume_while(|c| c != &apos;&lt;&apos;))
    }
</code></pre>
<p>&#x4E00;&#x822C;&#x700F;&#x89BD;&#x5668;&#x5C0D;&#x65BC;&#x591A;&#x9918;&#x7684;&#x7A7A;&#x767D;&#x90FD;&#x6703;&#x76F4;&#x63A5;&#x5FFD;&#x8996;&#xFF0C;&#x6240;&#x4EE5;&#x9019;&#x908A;&#x6709;&#x7279;&#x5225;&#x8655;&#x7406;&#x4E00;&#x4E0B;&#xFF0C;&#x5176;&#x5BE6;&#x4E0D;&#x662F;&#x5F88;&#x91CD;&#x8981;&#x5566;</p>
<pre><code>    /// Consume and discard zero or more whitespace characters.
    fn consume_whitespace(&amp;mut self) {
        self.consume_while(char::is_whitespace);
    }
</code></pre>
<p>&#x9019;&#x908A;&#x5BE6;&#x73FE;&#x7684;&#x89E3;&#x6790;&#x5668;&#xFF0C;&#x662F;&#x5F9E;&#x5DE6;&#x5230;&#x53F3;&#xFF0C;&#x4E00;&#x500B;&#x5B57;&#x5143;&#x4E00;&#x500B;&#x5B57;&#x5143;&#x5411;&#x53F3;&#x5224;&#x65B7;&#xFF0C;&#x7136;&#x5F8C;&#x628A;&#x8F38;&#x5165;&#x7684;&#x5B57;&#x4E32;&#x8DD1;&#x5B8C;&#x4F86;&#x505A;&#x89E3;&#x6790;</p>
<pre><code>    /// Return the current character, and advance self.pos to the next character.
    fn consume_char(&amp;mut self) -&gt; char {
        let mut iter = self.input[self.pos..].char_indices();
        let (_, cur_char) = iter.next().unwrap();
        let (next_pos, _) = iter.next().unwrap_or((1, &apos; &apos;));
        self.pos += next_pos;
        cur_char
    }
</code></pre>
<hr>
<p>&#x4EE5;&#x4E0A;&#x5C31;&#x662F;&#x7C21;&#x55AE;&#x7684; HTML &#x89E3;&#x6790;&#x5668;&#xFF0C;&#x57FA;&#x672C;&#x529F;&#x80FD;&#x90FD;&#x6709;&#x4E86;&#xFF0C;&#x7576;&#x7136;&#x5F88;&#x591A;&#x7F3A;&#x9677;&#xFF0C;&#x4E0D;&#x50C5;&#x4E00;&#x5806;&#x7279;&#x6B8A;&#x72C0;&#x6CC1;&#x7121;&#x6CD5;&#x8655;&#x7406;&#xFF0C;&#x5F88;&#x591A;&#x7684;&#x6A19;&#x6E96; HTML &#x5BEB;&#x6CD5;&#x4E5F;&#x4E0D;&#x652F;&#x63F4;&#x3002;&#x4E0D;&#x904E;&#x6211;&#x5011;&#x4E5F;&#x5927;&#x6982;&#x4E86;&#x89E3; Parser &#x7684;&#x4F5C;&#x7528;&#x548C;&#x505A;&#x6CD5;&#x4E86;&#xFF0C;&#x53EF;&#x4EE5;&#x4EE5;&#x6B64;&#x6539;&#x9032;&#xFF0C;&#x6216;&#x662F;&#x6709;&#x8208;&#x8DA3;&#x7684;&#x8A71;&#x5C31;&#x53BB;&#x8CA2;&#x737B;&#x4E00;&#x4E0B;&#x5230; html5ever &#x5427;&#xFF01;</p>
<p>&#x660E;&#x5929;&#x8A0E;&#x8AD6; CSS&#xFF0C;&#x5927;&#x5BB6;&#x518D;&#x898B;&#xFF01;</p>
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
                
