---
title: 瀏覽器引擎處理 CSS 的簡易版（二）
date: 2017-12-17 21:15:08
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x8655;&#x7406; CSS &#x53C8;&#x5206;&#x5169;&#x500B;&#x6B65;&#x9A5F;&#xFF0C;&#x6709; Parser &#x548C; style&#xFF0C;&#x524D;&#x8005;&#x662F;&#x89E3;&#x6790;&#x539F;&#x59CB; CSS&#xFF0C;&#x5F8C;&#x8005;&#x5247;&#x662F;&#x8B93; DOM &#x6709; style&#x3002;<br>
&#x6628;&#x5929;&#x8A0E;&#x8AD6;&#x904E; CSS parser &#x4E86;&#xFF0C;&#x800C;&#x4ECA;&#x5929;&#x5C31;&#x4F86;&#x8AC7;&#x8AC7; style&#x3002;</p>
<hr>
<h2>Style</h2>
<p>&#x5728;&#x958B;&#x59CB;&#x8B1B;&#x89E3;&#x5BE6;&#x4F5C;&#x4E4B;&#x524D;&#xFF0C;&#x5148;&#x4F86;&#x8AC7;&#x8AC7; style &#x5E7E;&#x500B;&#x6027;&#x8CEA;&#x3002;</p>
<ul>
<li>Cascading</li>
<li>Specified, computed, and actual values</li>
<li>Inheritance</li>
<li>Attribute</li>
</ul>
<h3>Cascade</h3>
<p>&#x53EF;&#x4EE5;&#x5148;&#x770B;&#x4E00;&#x4E0B; <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade" target="_blank">mozilla</a> &#x7684;&#x6587;&#x4EF6;&#x3002;<br>
&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F; style &#x6709;&#x5206;&#x597D;&#x5E7E;&#x500B;&#x7B49;&#x7D1A;&#xFF0C;&#x4F7F;&#x7528;&#x8005;&#x5B9A;&#x7FA9;&#x9AD8;&#x904E;&#x700F;&#x89BD;&#x5668;&#x9810;&#x8A2D;&#xFF0C;&#x6709;&#x52A0;&#x4E0A; <code>!important</code> &#x7684;&#x7B49;&#x7D1A;&#x6BD4;&#x6C92;&#x52A0;&#x7684;&#x9AD8;&#x3002;&#x7576;&#x4F7F;&#x7528;&#x8005;&#x6C92;&#x6709;&#x5B9A;&#x7FA9; style &#x7684;&#x6642;&#x5019;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x5C31;&#x6703;&#x4F7F;&#x7528;&#x81EA;&#x5DF1;&#x9810;&#x8A2D;&#x7684;&#x3002;&#x6240;&#x4EE5;&#x4F60;&#x6703;&#x767C;&#x73FE; <code>&lt;h1&gt;</code> &#x6BD4; <code>&lt;h2&gt;</code> &#x5B57;&#x9AD4;&#x8981;&#x5927;&#xFF0C;&#x660E;&#x660E;&#x81EA;&#x5DF1;&#x7684; CSS &#x6C92;&#x6709;&#x5B9A;&#x7FA9;&#xFF0C;&#x9019;&#x5C31;&#x662F;&#x56E0;&#x70BA;&#x700F;&#x89BD;&#x5668;&#x6709;&#x9810;&#x8A2D;&#x7684; style &#x4E86;&#x3002;</p>
<h3>Specified, computed, and actual values</h3>
<p>&#x9019;&#x90E8;&#x5206;&#x53EF;&#x4EE5;&#x770B; <a href="https://www.w3.org/TR/CSS2/cascade.html#computed-value" target="_blank">W3C</a> &#x7684;&#x6587;&#x4EF6;&#x3002;<br>
&#x4E3B;&#x8981;&#x662F;&#x8AAA;&#x7576;&#x700F;&#x89BD;&#x5668;&#x958B;&#x59CB;&#x89E3;&#x6790;&#x4E26;&#x69CB;&#x5EFA; DOM &#x6A39;&#xFF0C;&#x90A3;&#x9EBC;&#x5C31;&#x5FC5;&#x9808;&#x70BA; DOM &#x6A39;&#x4E2D;&#x7684;&#x6BCF;&#x500B;&#x5143;&#x7D20;&#x7684;&#x6BCF;&#x500B;&#x5C6C;&#x6027;&#x8CE6;&#x4E88;&#x4E00;&#x500B;&#x503C;&#x3002;</p>
<p>&#x7136;&#x800C;&#x6BCF;&#x500B;&#x5C6C;&#x6027;&#x7684;&#x6700;&#x7D42;&#x503C;&#x6700;&#x7D42;&#x503C;&#x662F;&#x901A;&#x904E;&#x56DB;&#x6B65;&#x8A08;&#x7B97;&#x5F97;&#x4F86;&#x7684;&#xFF1A;</p>
<ol>
<li>&#x901A;&#x904E;&#x6BCF;&#x500B;&#x5C6C;&#x6027;&#x7684;&#x898F;&#x7BC4;&#x8AAA;&#x660E;&#x7684;&#x9ED8;&#x8A8D;&#x503C;&#x6216;&#x8005;&#x662F;&#x7528;&#x6236;&#x986F;&#x793A;&#x901A;&#x904E; CSS &#x898F;&#x5247;&#x6307;&#x5B9A;&#x7684;&#x4E00;&#x500B;&#x503C;&#xFF0C;&#x7A31;&#x70BA;&#x6307;&#x5B9A;&#x503C;&#x3002;</li>
<li>&#x6307;&#x5B9A;&#x503C;&#x88AB;&#x89E3;&#x6790;&#x70BA; DOM &#x6A39;&#x7E7C;&#x627F;&#x6642;&#x4F7F;&#x7528;&#x7684;&#x503C;&#xFF0C;&#x7A31;&#x70BA;&#x8A08;&#x7B97;&#x503C;&#x3002;</li>
<li>&#x8A08;&#x7B97;&#x503C;&#x5728;&#x5FC5;&#x8981;&#x6642;&#x6703;&#x88AB;&#x8F49;&#x63DB;&#x70BA;&#x4E00;&#x500B;&#x7D55;&#x5C0D;&#x503C;&#xFF0C;&#x7A31;&#x70BA;&#x4F7F;&#x7528;&#x7684;&#x503C;&#x3002;</li>
<li>&#x6700;&#x5F8C;&#x4F7F;&#x7528;&#x7684;&#x503C;&#x6703;&#x7531;&#x65BC;&#x672C;&#x5730;&#x74B0;&#x5883;&#x7684;&#x9650;&#x5236;&#x518D;&#x505A;&#x4E00;&#x6B21;&#x8FD1;&#x4F3C;&#x8F49;&#x5316;&#xFF0C;&#x6BD4;&#x5982;&#x4F7F;&#x7528;&#x7684;&#x503C;&#x662F;1.5px&#xFF0C;&#x4F46;&#x662F;&#x67D0;&#x4E9B;&#x700F;&#x89BD;&#x5668;&#x4E0D;&#x652F;&#x6301;.5px&#x6703;&#x505A;&#x4E00;&#x6B21;&#x8FD1;&#x4F3C;&#x53D6;&#x503C;&#xFF0C;&#x6700;&#x7D42;&#x7684;&#x503C;&#x662F;2px&#xFF0C;&#x7A31;&#x70BA;&#x5BE6;&#x969B;&#x50F9;&#x503C;&#x3002;</li>
</ol>
<h3>Inheritance</h3>
<p>&#x7E7C;&#x627F;&#x662F;&#x6307;&#x5EF6;&#x7E8C;&#x7236;&#x7BC0;&#x9EDE;&#x7684;&#x5C6C;&#x6027;&#xFF0C;&#x76F4;&#x63A5;&#x7E7C;&#x7E8C;&#x5957;&#x7528;&#x3002;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x8B93;&#x5B50;&#x7BC0;&#x9EDE;&#x9032;&#x884C;&#x7E7C;&#x627F;&#x7236;&#x7BC0;&#x9EDE;&#x7684;&#x5C6C;&#x6027;&#xFF0C;&#x4F8B;&#x5982;&#x5B57;&#x9AD4;&#x548C;&#x984F;&#x8272;&#xFF0C;&#x5982;&#x4E0B;&#xFF1A;</p>
<pre><code class="language-html">&lt;div style=&quot;color: red;&quot;&gt;
    &lt;p&gt; &#x9019;&#x908A;&#x7684;&#x6587;&#x5B57;&#x5C31;&#x6703;&#x662F;&#x7D05;&#x8272; &lt;/p&gt;
&lt;/div&gt;
</code></pre>
<p>&#x56E0;&#x70BA;&#x6709;&#x7E7C;&#x627F;&#xFF0C;&#x6211;&#x5011;&#x4E0D;&#x7528;&#x6BCF;&#x500B;&#x5143;&#x7D20;&#x90FD;&#x7279;&#x5730;&#x8A2D;&#x5B9A;&#x5B57;&#x9AD4;&#x3001;&#x984F;&#x8272;&#x7B49;&#x7B49;&#x5C6C;&#x6027;&#xFF0C;&#x4ED6;&#x5011;&#x81EA;&#x5DF1;&#x5C31;&#x6703;&#x9075;&#x5FAA;&#x7236;&#x7BC0;&#x9EDE;&#x7684;&#x8A2D;&#x5B9A;&#xFF0C;&#x8981;&#x662F;&#x6BCF;&#x500B;&#x7BC0;&#x9EDE;&#x90FD;&#x8981;&#x7279;&#x5730;&#x8A2D;&#x5B9A;&#xFF0C;&#x90A3;&#x8A72;&#x6709;&#x591A;&#x9EBB;&#x7169;&#xFF01;</p>
<p>&#x7136;&#x800C;&#x50CF;&#x662F; margin&#x3001;padding&#x3001;border&#x3001;background-image &#x9019;&#x4E9B;&#x5C31;&#x4E0D;&#x6703;&#x88AB;&#x7E7C;&#x627F;&#x3002;&#x9019;&#x4E9B;&#x6538;&#x95DC;&#x65BC;&#x7248;&#x9762;&#x8F38;&#x51FA;&#xFF0C;&#x8981;&#x662F;&#x4ED6;&#x5011;&#x4E5F;&#x88AB;&#x7E7C;&#x627F;&#xFF0C;&#x90A3;&#x756B;&#x9762;&#x6839;&#x672C;&#x5C31;&#x6703;&#x662F;&#x4E00;&#x5718;&#x4E82;&#x4E86;&#xFF01;</p>
<h3>Attribute</h3>
<p>CSS &#x6211;&#x5011;&#x901A;&#x5E38;&#x5B9A;&#x7FA9;&#x5728; <code>.css</code> &#xFF0C;&#x4E26;&#x88AB; <code>.html</code> &#x5F15;&#x5165;&#xFF0C;&#x6216;&#x662F;&#x5728; html &#x4E2D;&#x4F7F;&#x7528; <code>&lt;style&gt;</code> &#x6A19;&#x7C64;&#x4F86;&#x8457;&#x540D;&#x662F; CSS &#x7684;&#x5B9A;&#x7FA9;&#x5340;&#x584A;&#x3002;&#x4F46;&#x6211;&#x5011;&#x4E5F;&#x53EF;&#x4EE5;&#x5728;&#x5BEB; HTML DOM &#x7684;&#x6642;&#x5019;&#xFF0C;&#x76F4;&#x63A5;&#x8CE6;&#x4E88;&#x5B83; CSS&#xFF0C;&#x9019;&#x5C31;&#x53EB;&#x505A; attribute&#x3002;&#x6240;&#x4EE5;&#x700F;&#x89BD;&#x5668;&#x9664;&#x4E86;&#x5F9E; CSS &#x4E2D;&#x89E3;&#x6790;&#x4E4B;&#x5916;&#xFF0C;&#x5728;&#x8655;&#x7406; DOM &#x7684;&#x6642;&#x5019;&#x4E5F;&#x8981;&#x7559;&#x610F;&#x6709;&#x6C92;&#x6709; CSS &#x4E26;&#x628A;&#x5B83;&#x63D2;&#x5165; CSS &#x7684;&#x6A39;&#x7576;&#x4E2D;&#x3002;<br>
&#x4F8B;&#x5982;&#x539F;&#x672C;&#x61C9;&#x8A72;&#x662F;&#xFF1A;</p>
<pre><code>&lt;style&gt;
    div {
        padding: 10px;
        color: red;
    }
&lt;/style&gt;
&lt;div&gt;&lt;/div&gt;
</code></pre>
<p>&#x53EF;&#x4EE5;&#x5BEB;&#x6210;&#xFF1A;</p>
<pre><code class="language-html">&lt;div style=&quot;padding:10px; color: red;&quot;&gt;&lt;/div&gt;
</code></pre>
<hr>
<p>&#x660E;&#x5929;&#x518D;&#x4F86;&#x8A0E;&#x8AD6;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#xFF0C;&#x4E00;&#x6A23;&#x6703;&#x4F7F;&#x7528; robinson &#x9019;&#x500B;&#x300C;&#x73A9;&#x5177;&#x300D;&#x5C08;&#x6848;&#x3002;robinson &#x5C07; CSS &#x62C6;&#x6210;&#x5169;&#x500B;&#x6A21;&#x7D44;&#xFF0C;&#x5728; <a href="https://github.com/mbrubeck/robinson/blob/master/src/css.rs" target="_blank">robinson/src/css.rs</a> &#x548C; <a href="https://github.com/mbrubeck/robinson/blob/master/src/style.rs" target="_blank">robinson/src/style.rs</a>&#x3002;&#x518D;&#x63D0;&#x4E00;&#x6B21;&#xFF0C;Servo &#x7684; CSS &#x90E8;&#x5206;&#x5728; <a href="https://github.com/servo/servo/tree/master/components/style" target="_blank">servo/components/style</a>&#xFF0C;&#x5C0D;&#x7167;&#x8457;&#x770B;&#x5C0D;&#x4E4B;&#x5F8C;&#x6211;&#x5011;&#x5B78;&#x7FD2; Servo &#x6703;&#x6709;&#x5E6B;&#x52A9;&#x3002;</p>
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
                
