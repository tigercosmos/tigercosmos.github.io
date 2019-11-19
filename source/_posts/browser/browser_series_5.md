---
title: 瀏覽器引擎處理 CSS 的簡易版（一）
date: 2017-12-16 15:52:02
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
<img src="https://youtubehindivideos.com/wp-content/uploads/2017/06/CSS-Tutorial-in-Hindi.jpg" alt="CSS"><br>
&#x4ECA;&#x5929;&#x7E7C;&#x7E8C;&#x4F7F;&#x7528; <a href="https://github.com/mbrubeck/robinson" target="_blank">robinson</a> &#x9019;&#x500B;&#x300C;&#x73A9;&#x5177;&#x300D;&#x4F86;&#x9032;&#x884C;&#x8B1B;&#x89E3;&#xFF0C;&#x7B2C;&#x4E8C;&#x7BC7;&#x6587;&#x7AE0;&#x8B1B;&#x5230;&#x89E3;&#x6790;&#xFF0C;&#x76EE;&#x524D;&#x6211;&#x5011;&#x5DF2;&#x7D93;&#x6703;&#x8655;&#x7406; DOM &#x548C; HTML &#x4E86;&#xFF0C;&#x63A5;&#x4E0B;&#x4F86;&#x5C31;&#x662F;&#x8655;&#x7406; CSS &#x7684;&#x90E8;&#x5206;&#x3002;&#x5728;&#x958B;&#x59CB;&#x4E4B;&#x524D;&#xFF0C;&#x4E0D;&#x77E5;&#x9053;&#x4F60;&#x5C0D; CSS &#x4E86;&#x89E3;&#x591A;&#x5C11;&#xFF0C;&#x5E73;&#x5E38;&#x6709;&#x5728;&#x958B;&#x767C;&#x7DB2;&#x9801;&#x7684;&#x8A71;&#x61C9;&#x8A72;&#x9084;&#x7B97;&#x662F;&#x61C2;&#x5427;&#xFF0C;&#x4E0D;&#x904E;&#x6211;&#x60F3;&#x4E26;&#x6C92;&#x6709;&#x771F;&#x6B63;&#x5B8C;&#x5168;&#x53BB;&#x7406;&#x89E3;&#x5B83;&#xFF0C;&#x56E0;&#x70BA;&#x5176;&#x5BE6;&#x53EA;&#x662F;&#x958B;&#x767C;&#x7DB2;&#x9801;&#x7684;&#x8A71;&#xFF0C;&#x4E5F;&#x4E0D;&#x9700;&#x8981;&#x61C2;&#x3002;</p>
<p>&#x4F46;&#x662F;&#x65E2;&#x7136;&#x6211;&#x5011;&#x73FE;&#x5728;&#x8981;&#x8655;&#x7406; CSS &#x7684;&#x90E8;&#x5206;&#xFF0C;&#x6709;&#x5B8C;&#x6574;&#x7684;&#x4E86;&#x89E3;&#x7576;&#x7136;&#x6700;&#x597D;&#xFF0C;&#x53EF;&#x4EE5;&#x53C3;&#x8003; <a href="https://developer.mozilla.org/zh-TW/docs/Web/CSS" target="_blank">Mozilla &#x6587;&#x4EF6;</a> &#x6216;&#x662F; <a href="https://www.w3.org/Style/CSS/specs.en.html" target="_blank">W3C &#x6587;&#x4EF6;</a>&#x3002;</p>
<p>&#x8655;&#x7406; CSS &#x53C8;&#x5206;&#x5169;&#x500B;&#x6B65;&#x9A5F;&#xFF0C;&#x6709; Parser &#x548C; style&#xFF0C;&#x524D;&#x8005;&#x662F;&#x89E3;&#x6790;&#x539F;&#x59CB; CSS&#xFF0C;&#x5F8C;&#x8005;&#x5247;&#x662F;&#x8B93; DOM &#x6709; style&#x3002;</p>
<p>robinson &#x9019;&#x500B;&#x5C08;&#x6848;&#x4E2D;&#xFF0C;CSS &#x62C6;&#x6210;&#x5169;&#x500B;&#x6A21;&#x7D44;&#xFF0C;&#x5728; <a href="https://github.com/mbrubeck/robinson/blob/master/src/css.rs" target="_blank">robinson/src/css.rs</a> &#x548C; <a href="https://github.com/mbrubeck/robinson/blob/master/src/style.rs" target="_blank">robinson/src/style.rs</a>&#x3002;&#x6709;&#x4E00;&#x9EDE;&#x9EDE;&#x5C0F;&#x9577;&#x4E86;&#xFF0C;&#x56E0;&#x70BA; CSS &#x672C;&#x4F86;&#x5C31;&#x883B;&#x8907;&#x96DC;&#x7684;&#x3002;&#x5C0D;&#x7167;&#x4E00;&#x4E0B;&#xFF0C;Servo &#x7684; CSS &#x90E8;&#x5206;&#x5728; <a href="https://github.com/servo/servo/tree/master/components/style" target="_blank">servo/components/style</a>&#xFF0C;&#x9EDE;&#x9032;&#x53BB;&#x5C31;&#x6703;&#x767C;&#x73FE;&#x5B83;&#x5F88;&#x8907;&#x96DC;&#x3002;CSS &#x90E8;&#x5206;&#x5DF2;&#x7D93;&#x88AB;&#x62FF;&#x53BB;&#x5728; Firefox &#x4E0A;&#x4F7F;&#x7528;&#xFF0C;&#x7B97;&#x662F;&#x6EFF;&#x5B8C;&#x6574;&#x7684;&#xFF0C;&#x6B63;&#x5F0F;&#x7684;&#x540D;&#x7A31;&#x53EB;&#x505A; <a href="https://wiki.mozilla.org/Quantum/Stylo" target="_blank">Stylo</a>&#xFF0C;&#x73FE;&#x5728;&#x53EA;&#x662F;&#x7A0D;&#x5FAE;&#x63D0;&#x4E00;&#x4E0B;&#xFF0C;&#x4E4B;&#x5F8C;&#x6703;&#x518D;&#x7D30;&#x8B1B;&#x3002;</p>
<hr>
<h2>Parser</h2>
<p>&#x4ECA;&#x5929;&#x5148;&#x91DD;&#x5C0D; parser &#x4F86;&#x89E3;&#x8AAA;&#xFF0C; &#x4E5F;&#x5C31;&#x662F; <a href="https://github.com/mbrubeck/robinson/blob/master/src/css.rs" target="_blank"><code>css.rs</code></a> &#x7684;&#x90E8;&#x5206;&#x3002;&#xFF08;&#x89E3;&#x8AAA;&#x90FD;&#x662F;&#x5728;&#x7A0B;&#x5F0F;&#x78BC;&#x5340;&#x584A;&#x7684;&#x4E0A;&#x65B9;&#xFF09;</p>
<p>&#x5B9A;&#x7FA9; css &#x7684;&#x898F;&#x5247;&#xFF0C;&#x6240;&#x4EE5;&#x662F;&#x898F;&#x5247;&#x7684;&#x5411;&#x91CF;</p>
<pre><code>pub struct Stylesheet {
    pub rules: Vec&lt;Rule&gt;,
}
</code></pre>
<p>&#x4E00;&#x689D;&#x4E00;&#x689D;&#x7684;&#x898F;&#x5247;&#xFF0C;&#x5305;&#x542B;&#x9078;&#x64C7;&#x5B50;&#x548C;&#x5BA3;&#x544A;</p>
<pre><code>struct Rule {
    selectors: Vec&lt;Selector&gt;,
    declarations: Vec&lt;Declaration&gt;,
}
</code></pre>
<p>&#x9019;&#x908A;&#x7684; <code>SimpleSelector</code> &#x53EA;&#x652F;&#x63F4;&#x55AE;&#x4E00;&#x908F;&#x8F2F;&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A;&#x61C9;&#x8A72;&#x9084;&#x6709;<a href="https://www.w3schools.com/css/css_combinators.asp" target="_blank">&#x7D44;&#x5408;&#x5B50;&#x908F;&#x8F2F;</a>&#xFF0C;&#x53EA;&#x662F;&#x5728;&#x9019;&#x908A;&#x7684;&#x7BC4;&#x4F8B;&#x78BC;&#x4E2D;&#x4E26;&#x6C92;&#x6709;&#x5BE6;&#x73FE;&#x3002;<br>
&#x8209;&#x4F8B;&#x4F86;&#x8AAA;&#x591A;&#x91CD;&#x9078;&#x64C7;&#x5C31;&#x662F;&#x50CF; <code>div &gt; p</code> &#x6216; <code>div + p</code> &#x9019;&#x6A23;&#x3002;</p>
<p><code>tag</code> &#x5C31;&#x662F; <code>div</code> &#x3001; <code>p</code> &#x3001; <code>h1</code> &#x4E4B;&#x985E;&#x7684;&#xFF0C; <code>id</code> &#x5247;&#x662F; <code>#</code> &#x958B;&#x982D;&#xFF0C;&#x800C; <code>class</code> &#x5C31;&#x662F; <code>.</code> &#x958B;&#x982D;</p>
<pre><code>pub struct SimpleSelector {
    pub tag_name: Option&lt;String&gt;,
    pub id: Option&lt;String&gt;,
    pub class: Vec&lt;String&gt;,
}
</code></pre>
<p>&#x9078;&#x64C7;&#x5668;&#x9078;&#x5230;&#x6771;&#x897F;&#x4E4B;&#x5F8C;&#xFF0C;&#x6703;&#x770B;&#x88E1;&#x9762;&#x7684;&#x5167;&#x5BB9;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5BA3;&#x544A;&#x4E86;&#x3002;<br>
&#x4F8B;&#x5982; <code>padding: 10px</code>&#xFF0C;<code>padding</code> &#x662F;&#x540D;&#x7A31;&#xFF0C;<code>10px</code> &#x5247;&#x662F;&#x4ED6;&#x7684;&#x503C;&#x3002;</p>
<pre><code>struct Declaration {
    name: String,
    value: Value,
}
</code></pre>
<p>&#x800C;&#x5BA3;&#x544A;&#x7684;&#x503C;&#xFF0C;&#x55AE;&#x4F4D;&#x9805;&#x76EE;&#x90FD;&#x4E0D;&#x4E00;&#x6A23;&#xFF0C;&#x5FC5;&#x9808;&#x8981;&#x6709;&#x6771;&#x897F;&#x4F86;&#x8B80;&#x4ED6;&#x5011;&#x3002;&#x4F8B;&#x5982;&#x9577;&#x5EA6;&#x5C31;&#x6709;&#x53EF;&#x80FD;&#x662F; <code>px</code> &#x3001; <code>em</code>&#xFF0C;&#x984F;&#x8272;&#x53EF;&#x4EE5;&#x7528; <code>white</code> &#x6216;&#x662F; <code>#000</code> &#x4F86;&#x8868;&#x793A;&#x3002;&#x9019;&#x908A;&#x5C31;&#x662F;&#x5B9A;&#x7FA9;&#x4ED6;&#x5011;&#x3002;</p>
<pre><code>enum Value {..}
enum Unit {..}
struct Color {..}
</code></pre>
<p>&#x7C21;&#x55AE;&#x7684; CSS &#x9078;&#x64C7;&#x5668;&#xFF0C;&#x5F9E;&#x5DE6;&#x5230;&#x53F3;&#x8B80;&#x9032;&#x53BB;&#xFF0C;&#x7136;&#x5F8C;&#x5B58;&#x9032; <code>SimpleSelector</code>&#xFF0C;&#x9019;&#x908A;&#x4E26;&#x4E0D;&#x56B4;&#x8B39;&#xFF0C;&#x5F88;&#x591A;&#x932F;&#x8AA4;&#x7684;&#x8F38;&#x5165;&#x6703;&#x88AB;&#x7576;&#x6210;&#x6B63;&#x78BA;&#x7684;&#xFF0C;&#x5C31;&#x50CF;&#x662F; <code>*ABC*</code>&#xFF0C;&#x4F46;&#x4E8B;&#x5BE6;&#x4E0A; <code>*</code> &#x7576;&#x7136;&#x4E0D;&#x6703;&#x63A5;&#x5728;&#x5C3E;&#x5DF4;&#x3002;&#x4E00;&#x822C;&#x6B63;&#x5F0F;&#x7684;&#x700F;&#x89BD;&#x5668;&#x5728;&#x89E3;&#x6790;&#x78B0;&#x5230;&#x932F;&#x8AA4;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x6703;&#x76F4;&#x63A5;&#x5FFD;&#x8996;&#x90A3;&#x500B;&#x932F;&#x8AA4;&#x7684; CSS&#xFF0C;&#x4E00;&#x4E9B;&#x5947;&#x602A;&#x7684;&#x8F38;&#x5165;&#x4E5F;&#x6703;&#x88AB;&#x5FFD;&#x8996;&#x3002;&#x6240;&#x4EE5;&#x50CF;&#x662F;&#x8F38;&#x5165; <code>padding: red</code> &#x9019;&#x7A2E;&#x5B8C;&#x5168;&#x932F;&#x8AA4;&#x7684;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x5C31;&#x4E0D;&#x6703;&#x628A;&#x4ED6;&#x5217;&#x5165; CSS tree &#x4E2D;&#x3002;</p>
<pre><code>    fn parse_simple_selector(&amp;mut self) -&gt; SimpleSelector {
        let mut selector = SimpleSelector { tag_name: None, id: None, class: Vec::new() };
        while !self.eof() {
            match self.next_char() {
                &apos;#&apos; =&gt; {
                    self.consume_char();
                    selector.id = Some(self.parse_identifier());
                }
                &apos;.&apos; =&gt; {
                    self.consume_char();
                    selector.class.push(self.parse_identifier());
                }
                &apos;*&apos; =&gt; {
                    // universal selector
                    self.consume_char();
                }
                c if valid_identifier_char(c) =&gt; {
                    selector.tag_name = Some(self.parse_identifier());
                }
                _ =&gt; break
            }
        }
        selector
}
</code></pre>
<p>Parser &#x7684;&#x7D30;&#x7BC0;&#x90E8;&#x5206;&#x8DDF;&#x6628;&#x5929;&#x7684; HTML &#x90FD;&#x975E;&#x5E38;&#x63A5;&#x8FD1;&#xFF0C;&#x50CF;&#x662F; <code>parse_declarations</code> &#x5C31;&#x662F;&#x6293;&#x5169;&#x500B;&#x5927;&#x62EC;&#x5F27;&#x4E2D;&#x7684;&#x5167;&#x5BB9;&#xFF0C;&#x7136;&#x5F8C;&#x518D;&#x91DD;&#x5C0D;&#x5167;&#x5BB9;&#x6709;&#x66F4;&#x8FD1;&#x4E00;&#x6B65;&#x7684;&#x62C6;&#x89E3;&#xFF0C;&#x9019;&#x90E8;&#x5206;&#x770B;&#x539F;&#x59CB;&#x78BC;&#x5C31;&#x975E;&#x5E38;&#x597D;&#x7406;&#x89E3;&#x4E86;&#xFF0C;&#x5C31;&#x4E0D;&#x5728;&#x4E00;&#x4E00;&#x8AAA;&#x660E;&#x3002;</p>
<pre><code>    /// Parse a list of declarations enclosed in `{ ... }`.
    fn parse_declarations(&amp;mut self) -&gt; Vec&lt;Declaration&gt; {
        assert_eq!(self.consume_char(), &apos;{&apos;);
        let mut declarations = Vec::new();
        loop {
            self.consume_whitespace();
            if self.next_char() == &apos;}&apos; {
                self.consume_char();
                break;
            }
            declarations.push(self.parse_declaration());
        }
        declarations
}
</code></pre>
<p>&#x6700;&#x5F8C;&#x6BD4;&#x8F03;&#x91CD;&#x8981;&#x7684;&#x90E8;&#x5206;&#x662F;&#xFF0C;<a href="https://www.w3.org/TR/selectors/#specificity" target="_blank">&#x6B0A;&#x91CD;&#x5206;&#x914D;</a>&#x3002;&#x540C;&#x4E00;&#x500B; DOM &#x53EF;&#x80FD;&#x540C;&#x6642;&#x6709;&#x5F88;&#x591A; CSS &#x5B9A;&#x7FA9;&#x5B83;&#xFF0C;&#x90A3;&#x7A76;&#x7ADF;&#x8981;&#x9078;&#x64C7;&#x54EA;&#x500B;&#x7576;&#x4F5C;&#x6700;&#x5F8C;&#x5448;&#x73FE;&#x7684;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x5C31;&#x770B;&#x4ED6;&#x5011;&#x7684;&#x91CD;&#x8981;&#x7A0B;&#x5EA6;&#x5566;&#x3002;&#x4E00;&#x822C;&#x800C;&#x8A00; id &gt; class &gt; tag&#xFF0C;&#x6240;&#x4EE5;&#x5C31;&#x53EF;&#x4EE5;&#x5B9A;&#x7FA9;&#xFF0C;&#x6BD4;&#x65B9;&#x8AAA; id &#x52A0;&#x6B0A; 3&#xFF0C;tag &#x53EA;&#x6709;&#x52A0;&#x6B0A; 1 &#x4E4B;&#x985E;&#x7684;&#xFF0C;&#x6700;&#x5F8C;&#x54EA;&#x500B; CSS &#x91DD;&#x5C0D;&#x9019;&#x500B; DOM &#x6578;&#x503C;&#x6700;&#x9AD8;&#xFF0C;&#x5C31;&#x4F7F;&#x7528;&#x5B83;&#x3002;</p>
<pre><code>impl Selector {
    pub fn specificity(&amp;self) -&gt; Specificity {
        // https://www.w3.org/TR/selectors/#specificity
        let Selector::Simple(ref simple) = *self;
        let a = simple.id.iter().count();
        let b = simple.class.len();
        let c = simple.tag_name.iter().count();
        (a, b, c)
    }
}
</code></pre>
<hr>
<p>&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
