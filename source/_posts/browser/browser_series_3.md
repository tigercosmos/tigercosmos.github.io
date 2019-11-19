---
title: 瀏覽器引擎處理 DOM 的簡易版
date: 2017-12-14 23:47:47
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
<h2>&#x73A9;&#x5177;&#xFF1F;</h2>
<p>&#x63A5;&#x4E0B;&#x4F86;&#x958B;&#x59CB;&#x6703;&#x5BE6;&#x6230;&#x89E3;&#x8AAA;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;&#xFF0C;&#x7531;&#x65BC;&#x6211;&#x6C92;&#x6709;&#x63A5;&#x89F8;&#x904E; Gecko &#x6216;&#x662F; WebKit&#xFF0C;&#x6240;&#x4EE5;&#x6703;&#x7531; Servo &#x4F86;&#x5207;&#x5165;&#xFF0C;&#x9019;&#x5E7E;&#x500B;&#x90FD;&#x662F;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;&#xFF0C;&#x4E4B;&#x524D;&#x6587;&#x7AE0;&#x6709;&#x63D0;&#x5230;&#x904E;&#x3002;Gecko &#x90A3;&#x4E9B;&#x5DF2;&#x7D93;&#x662F;&#x9F90;&#x7136;&#x5927;&#x7269;&#xFF0C;&#x4F46; Servo &#x4E5F;&#x5DF2;&#x7D93;&#x4E0D;&#x5C0F;&#x4E86;&#xFF0C;&#x76F4;&#x63A5;&#x5207;&#x5165;&#x6709;&#x9EDE;&#x592A;&#x56F0;&#x96E3;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x5148;&#x5F9E;&#x300C;&#x73A9;&#x5177;&#x300D;&#x700F;&#x89BD;&#x5668;&#x958B;&#x59CB;&#x89E3;&#x8AAA;&#xFF0C;&#x4E4B;&#x5F8C;&#x518D;&#x9032;&#x968E;&#x6210;&#x771F;&#x6B63;&#x7684;&#x3002;&#x6240;&#x8B02;&#x73A9;&#x5177;&#x7684;&#x610F;&#x601D;&#x662F;&#xFF0C;&#x529F;&#x80FD;&#x975E;&#x5E38;&#x7C21;&#x964B;&#xFF0C;&#x5B58;&#x7CB9;&#x7149;&#x529F;&#x7528;&#x7684;&#xFF0C;&#x5C31;&#x50CF;&#x662F;&#x5927;&#x5B78;&#x4FEE;&#x8CC7;&#x6599;&#x5EAB;&#x3001;&#x7DE8;&#x8B6F;&#x7A0B;&#x5F0F;&#x9019;&#x985E;&#x7684;&#x8AB2;&#x7A0B;&#xFF0C;&#x4E5F;&#x90FD;&#x6703;&#x5BE6;&#x505A;&#x4E00;&#x500B;&#x73A9;&#x5177;&#x7576;&#x4F5C;&#x5C08;&#x984C;&#x3002;&#x73A9;&#x5177;&#x672C;&#x8EAB;&#x7576;&#x7136;&#x4E0D;&#x80FD;&#x8DDF;&#x771F;&#x6B63;&#x7684;&#x7522;&#x54C1;&#x76F8;&#x6BD4;&#xFF0C;&#x4F46;&#x6982;&#x5FF5;&#x662F;&#x4E00;&#x81F4;&#x7684;&#xFF0C;&#x53EF;&#x4EE5;&#x85C9;&#x7531;&#x73A9;&#x5177;&#x4F86;&#x4E86;&#x89E3;&#x7522;&#x54C1;&#x3002;</p>
<p>&#x4EE5;&#x4E0B;&#x9019;&#x5E7E;&#x500B;&#x90FD;&#x662F;&#x6BD4;&#x8F03;&#x5C0F;&#x578B;&#x7684;&#x5F15;&#x64CE;&#x5C08;&#x6848;&#xFF1A;</p>
<ul>
<li>
<a href="https://github.com/philborlin/CSSBox" target="_blank">CSSBox (Java)</a>
</li>
<li>
<a href="https://github.com/silexlabs/Cocktail" target="_blank">Cocktail (Haxe)</a>
</li>
<li>
<a href="https://gngr.info/" target="_blank">gngr (Java)</a>
</li>
<li>
<a href="https://github.com/tordex/litehtml" target="_blank">litehtml (C++)</a>
</li>
<li>
<a href="https://github.com/admin36/LURE" target="_blank">LURE (Lua)</a>
</li>
<li>
<a href="https://www.netsurf-browser.org/" target="_blank">NetSurf (C)</a>
</li>
<li>
<a href="https://hsbrowser.wordpress.com/3s-functional-web-browser/" target="_blank">Simple San Simon (Haskell)</a>
</li>
<li>
<a href="https://github.com/Kozea/WeasyPrint" target="_blank">WeasyPrint (Python)</a>
</li>
<li>
<a href="https://github.com/reesmichael1/WebWhirr" target="_blank">WebWhirr (C++)</a>
</li>
</ul>
<p>&#x56E0;&#x70BA;&#x662F;&#x5C0F;&#x578B;&#x7684;&#xFF0C;&#x6240;&#x4EE5;&#x5F88;&#x9069;&#x5408;&#x62FF;&#x4F86;&#x521D;&#x6B65;&#x5B78;&#x7FD2;&#xFF0C;&#x770B;&#x770B;&#x600E;&#x6A23;&#x5236;&#x5B9A;&#x67B6;&#x69CB;&#x3001;&#x5BE6;&#x4F5C;&#x529F;&#x80FD;&#x7B49;&#x7B49;&#x3002;&#x5927;&#x5BB6;&#x53EF;&#x4EE5;&#x6BCF;&#x500B;&#x5C08;&#x6848;&#x9EDE;&#x9032;&#x53BB;&#x770B;&#x770B;&#x4ED6;&#x5011;&#x7684;&#x67B6;&#x69CB;&#x3001;&#x908F;&#x8F2F;&#x3001;&#x5BEB;&#x6CD5;&#xFF0C;&#x7A0D;&#x5FAE;&#x6709;&#x500B;&#x6982;&#x5FF5;&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x9806;&#x4FBF;&#x6BD4;&#x8F03;&#x770B;&#x770B;&#x5927;&#x5BB6;&#x7684;&#x5DEE;&#x7570;&#x3002;&#x540C;&#x6A23;&#x4E00;&#x4EF6;&#x4E8B;&#x672C;&#x4F86;&#x5C31;&#x6709;&#x5F88;&#x591A;&#x7A2E;&#x505A;&#x6CD5; &#xFF38;&#xFF24;</p>
<p>&#x672C;&#x6587;&#x63A1;&#x7528; <a href="https://github.com/mbrubeck/" target="_blank">@mbrubeck</a> &#x7684;&#x4F5C;&#x54C1; <a href="https://github.com/mbrubeck/robinson" target="_blank">robinson</a> &#x4F86;&#x89E3;&#x8AAA;&#xFF0C;&#x539F;&#x56E0;&#x662F;&#x9019;&#x500B;&#x4EBA;&#x4E5F;&#x662F; Servo &#x7684;&#x958B;&#x767C;&#x5718;&#x968A;&#x8005;&#x4E4B;&#x4E00;&#xFF0C;&#x5BEB;&#x6CD5;&#x7B97;&#x662F;&#x7C21;&#x6613;&#x578B;&#x7684; Servo&#xFF0C;&#x5C0D;&#x6211;&#x5011;&#x4E4B;&#x5F8C;&#x63A2;&#x8A0E; Servo &#x6703;&#x6709;&#x5E6B;&#x52A9;&#x3002;&#x6B64;&#x5916;&#x9019;&#x500B;&#x5C08;&#x6848;&#x662F;&#x7528; Rust &#x8A9E;&#x8A00;&#x5BEB;&#x7684;&#x3002;</p>
<h2>DOM</h2>
<p>&#x5148;&#x4F86;&#x770B;&#x770B;&#x7C21;&#x6613;&#x7248;&#x7684;&#x7684; DOM &#x9577;&#x600E;&#x6A23;&#x5427;&#xFF01;<br>
&#x5BE6;&#x4F5C; DOM &#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#x5728; <a href="https://github.com/mbrubeck/robinson/blob/master/src/dom.rs" target="_blank">robinson/src/dom.rs</a>&#xFF0C;&#x53EF;&#x4EE5;&#x9EDE;&#x9032;&#x53BB;&#x770B;&#x4E00;&#x4E0B;&#xFF0C;&#x5176;&#x5BE6;&#x975E;&#x5E38;&#x77ED;&#x3002;&#x9019;&#x908A;&#x53EF;&#x4EE5;&#x5C0D;&#x7167;&#x4E00;&#x4E0B; Servo &#x7684;&#x90E8;&#x5206;&#xFF0C;&#x662F;&#x5728; <a href="https://github.com/servo/servo/tree/master/components/script/dom" target="_blank">servo/components/script/dom/</a> &#x9EDE;&#x9032;&#x53BB;&#x4F60;&#x5C31;&#x6703;&#x5687;&#x5230;&#x4E86;&#xFF01;</p>
<p>&#x4F86;&#x89E3;&#x91CB;&#x4E00;&#x4E0B; robinson &#x7684; dom &#x5728;&#x505A;&#x4EC0;&#x9EBC;&#x3002;</p>
<h3>&#x5B9A;&#x7FA9;&#x7BC0;&#x9EDE;</h3>
<p>HTML &#x662F;&#x7531;&#x4E00;&#x5806;&#x7684;&#x7BC0;&#x9EDE;&#x7D44;&#x6210;&#x7684;&#x3002;&#x4E5F;&#x5C31;&#x662F;&#x6211;&#x5011;&#x5E73;&#x5E38;&#x770B;&#x5230;&#x7684; <code>&lt;body&gt;</code> &#x3001; <code>&lt;div&gt;</code> &#x3001; <code>&lt;p&gt;</code> &#x4E4B;&#x985E;&#x7684;&#x6A19;&#x7C64;&#xFF0C;&#x800C;&#x9019;&#x4E9B;&#x6A19;&#x7C64;&#x5F7C;&#x6B64;&#x6709;&#x4E0A;&#x4E0B;&#x95DC;&#x4FC2;&#xFF0C;&#x4E5F;&#x5C31;&#x5F62;&#x6210;&#x4E86;&#x7BC0;&#x9EDE;&#x3002;<br>
&#x6240;&#x4EE5;&#x9019;&#x908A;&#x5148;&#x5B9A;&#x7FA9;&#x4EC0;&#x9EBC;&#x662F;&#x7BC0;&#x9EDE;&#xFF0C;&#x7BC0;&#x9EDE;&#x5305;&#x542B;&#x4ED6;&#x7684;&#x300C;&#x5B50;&#x300D;&#x7BC0;&#x9EDE;&#xFF0C;&#x53E6;&#x5916;&#x7BC0;&#x9EDE;&#x4E5F;&#x6709;&#x5206;&#x7A2E;&#x985E;&#xFF0C;&#x4F8B;&#x5982;&#x5143;&#x7D20;&#x3001;&#x5716;&#x7247;&#x3001;&#x6587;&#x5B57;&#xFF0C;&#x56E0;&#x70BA;&#x9019;&#x908A;&#x662F;&#x6700;&#x967D;&#x6625;&#x7684;&#x90A3;&#x7A2E;&#xFF0C;&#x6240;&#x4EE5;&#x53EA;&#x6709;&#x5B9A;&#x7FA9;&#x5169;&#x7A2E;&#x3002;</p>
<pre><code>#[derive(Debug)]
pub struct Node {
    // data common to all nodes:
    pub children: Vec&lt;Node&gt;,

    // data specific to each node type:
    pub node_type: NodeType,
}

#[derive(Debug)]
pub enum NodeType {
    Element(ElementData),
    Text(String),
}
</code></pre>
<h3>&#x5C6C;&#x6027;</h3>
<p>&#x9019;&#x908A;&#x5BE6;&#x4F5C;&#x5143;&#x7D20;&#x7684;&#x5C6C;&#x6027;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5E73;&#x5E38;&#x770B;&#x5230;&#x7684; <code>class</code> &#x3001; <code>name</code> &#x3001; <code>id</code>&#xFF0C;&#x7576;&#x7136;&#x9019;&#x908A;&#x4E5F;&#x662F;&#x7C21;&#x55AE;&#x5730;&#x5448;&#x73FE;&#x800C;&#x5DF2;&#x3002;</p>
<pre><code>pub type AttrMap = HashMap&lt;String, String&gt;;
</code></pre>
<pre><code>#[derive(Debug)]
pub struct ElementData {
    pub tag_name: String,
    pub attributes: AttrMap,
}
</code></pre>
<h3>&#x5EFA;&#x69CB;&#x5B50;</h3>
<p>&#x6240;&#x8B02;&#x5EFA;&#x69CB;&#x5B50;&#x5C31;&#x662F;&#x521D;&#x59CB;&#x5316;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x7269;&#x4EF6;&#xFF0C;&#x9019;&#x908A;&#x4E5F;&#x662F;&#x4E00;&#x6A23;&#x7684;&#x6982;&#x5FF5;&#xFF0C;&#x8B93;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x8F15;&#x9B06;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x5143;&#x7D20;&#x7269;&#x4EF6;&#x3002;<br>
&#x7531;&#x65BC;&#x4F5C;&#x8005;&#x53EA;&#x5BEB;&#x4E86;&#x5169;&#x7A2E;&#x7BC0;&#x9EDE;&#xFF0C;&#x6240;&#x4EE5;&#x5EFA;&#x69CB;&#x5B50;&#x4E5F;&#x5C31;&#x53EA;&#x6709;&#x5169;&#x7A2E;&#xFF0C;&#x4ED4;&#x7D30;&#x770B;&#x7684;&#x8A71;&#x61C9;&#x8A72;&#x4E0D;&#x96E3;&#x7406;&#x89E3;&#xFF0C;&#x50CF;&#x662F; <code>elem</code> &#x5C31;&#x662F;&#x5EFA;&#x7ACB;&#x5143;&#x7D20;&#xFF0C;&#x4ED6;&#x9023;&#x5B50;&#x5143;&#x7D20;&#x548C;&#x5C6C;&#x6027;&#x4E00;&#x8D77;&#x5EFA;&#x7ACB;&#x8D77;&#x4F86;&#x3002;</p>
<pre><code>pub fn text(data: String) -&gt; Node {
    Node { children: vec![], node_type: NodeType::Text(data) }
}

pub fn elem(name: String, attrs: AttrMap, children: Vec&lt;Node&gt;) -&gt; Node {
    Node {
        children: children,
        node_type: NodeType::Element(ElementData {
            tag_name: name,
            attributes: attrs,
        })
    }
}
</code></pre>
<h3>&#x5C6C;&#x6027;&#x7D81;&#x5B9A;</h3>
<p>&#x5143;&#x7D20;&#x6B78;&#x5143;&#x7D20;&#xFF0C;&#x5C6C;&#x6027;&#x6B78;&#x5C6C;&#x6027;&#xFF0C;&#x8981;&#x8B93;&#x5143;&#x7D20;&#x6709;&#x5C6C;&#x6027;&#xFF0C;&#x7576;&#x7136;&#x9084;&#x8981;&#x505A;&#x9EDE;&#x4E8B;&#xFF0C;&#x9019;&#x908A;&#x5C31;&#x662F;&#x628A;&#x5C6C;&#x6027;&#x7D81;&#x5B9A;&#x5143;&#x7D20;&#x7684;&#x5BE6;&#x73FE;&#xFF0C;&#x9019;&#x908A;&#x53EA;&#x662F;&#x7C21;&#x55AE;&#x7684;&#x53D6;&#x5F97;&#x9019;&#x500B;&#x5143;&#x7D20;&#x7684; <code>id</code> &#x548C; <code>class</code>&#x3002;&#x4E8B;&#x5BE6;&#x4E0A;&#x5BE6;&#x969B;&#x60C5;&#x6CC1;&#x8907;&#x67E5;&#x5F97;&#x591A;&#xFF0C;&#x4F8B;&#x5982;&#x9084;&#x8981;&#x6AA2;&#x67E5;&#x5C6C;&#x6027;&#x7684;&#x6B63;&#x78BA;&#x6027;&#xFF0C;&#x9084;&#x8981;&#x8DDF; JS &#x505A;&#x9023;&#x7D50;&#xFF0C;&#x6709;&#x4E9B;&#x5C6C;&#x6027;&#x9084;&#x6703;&#x6709;&#x908F;&#x8F2F;&#xFF0C;&#x4F8B;&#x5982; <code>&lt;input&gt;</code> &#x7684; <code>type</code> &#x5C31;&#x597D;&#x5E7E;&#x7A2E;&#xFF0C;&#x5982; <code>month</code> &#x3001; <code>date</code> &#x3001; <code>color</code>&#xFF0C;&#x6BCF;&#x7A2E;&#x908F;&#x8F2F;&#x90FD;&#x6709;&#x5404;&#x81EA;&#x7684;&#x6F14;&#x7B97;&#x6CD5;&#x3002;</p>
<pre><code>impl ElementData {
    pub fn id(&amp;self) -&gt; Option&lt;&amp;String&gt; {
        self.attributes.get(&quot;id&quot;)
    }

    pub fn classes(&amp;self) -&gt; HashSet&lt;&amp;str&gt; {
        match self.attributes.get(&quot;class&quot;) {
            Some(classlist) =&gt; classlist.split(&apos; &apos;).collect(),
            None =&gt; HashSet::new()
        }
    }
}
</code></pre>
<hr>
<p>&#x4ECA;&#x5929;&#x770B;&#x4E86;&#x7C21;&#x55AE;&#x7684; DOM &#x5BE6;&#x4F5C;&#x65B9;&#x5F0F;&#xFF0C;&#x771F;&#x5BE6;&#x7684;&#x700F;&#x89BD;&#x5668;&#x7D55;&#x5C0D;&#x66F4;&#x8907;&#x96DC;&#xFF0C;&#x842C;&#x4E8B;&#x8D77;&#x982D;&#x96E3;&#xFF0C;&#x5343;&#x842C;&#x5225;&#x7070;&#x5FC3;&#xFF01;&#x6211;&#x5011;&#x5148;&#x5F9E;&#x7C21;&#x55AE;&#x7684;&#x5B78;&#x8D77;&#xFF0C;&#x4E4B;&#x5F8C;&#x518D;&#x7E7C;&#x7E8C;&#x6311;&#x6230;&#x66F4;&#x8907;&#x96DC;&#x7684;&#x771F;&#x5BE6;&#x7248;&#x672C;&#x3002;&#x9019;&#x5E7E;&#x5929;&#x90FD;&#x6703;&#x662F;&#x7C21;&#x55AE;&#x7248;&#x7684;&#x8B1B;&#x89E3;&#xFF0C;&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
