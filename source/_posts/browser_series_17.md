---
title: 瀏覽器開發進階實戰（三）捲動
date: 2017-12-28 23:21:25
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x4ECA;&#x5929;&#x7E7C;&#x7E8C;&#x4EE5;<a href="https://github.com/servo/servo" target="_blank">Servo</a> &#x5C08;&#x6848;&#x4F86;&#x8A0E;&#x8AD6;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#x3002;</p>
<p>&#x4ECA;&#x5929;&#x4E3B;&#x984C;&#x662F; scroll&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6372;&#x52D5;&#x3002;&#x7576;&#x9801;&#x9762;&#x5927;&#x65BC;&#x8996;&#x7A97;&#xFF0C;&#x6216;&#x662F;&#x5143;&#x7D20;&#x5167;&#x5BB9;&#x5927;&#x65BC;&#x5143;&#x7D20;&#x672C;&#x8EAB;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x6211;&#x5011;&#x5E38;&#x5E38;&#x6703;&#x770B;&#x5230;&#x5230;&#x300C;&#x6372;&#x8EF8;&#x300D;&#x51FA;&#x73FE;&#x3002;&#x4E26;&#x4E14;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x6372;&#x52D5;&#x8996;&#x7A97;&#xFF0C;&#x9019;&#x5C31;&#x662F; scroll &#x505A;&#x7684;&#x4E8B;&#x60C5;&#x4E86;&#x3002;&#x4E0D;&#x904E;&#x4ECA;&#x5929;&#x8A0E;&#x8AD6;&#x7684;&#x662F;&#x4F7F;&#x7528; script &#x53BB;&#x505A;&#x6372;&#x52D5;&#x3002;&#x6372;&#x52D5;&#x727D;&#x626F;&#x5230;&#x7684;&#x6771;&#x897F;&#x592A;&#x591A;&#xFF0C;&#x4E0D;&#x53EF;&#x80FD;&#x628A;&#x6240;&#x6709;&#x6A5F;&#x5236;&#x90FD;&#x8B1B;&#xFF0C;&#x6240;&#x4EE5;&#x4ECA;&#x5929;&#x6311;&#x4E00;&#x5C0F;&#x90E8;&#x5206;&#x4F86;&#x8AAA;&#x660E;&#x3002;</p>
<p>&#x5728;&#x5BE6;&#x4F5C;&#x4E4B;&#x524D;&#xFF0C;&#x6211;&#x5011;&#x5148;&#x4F86;&#x770B;&#x770B;<a href="https://drafts.csswg.org/cssom-view/#scrolling-box" target="_blank">&#x6587;&#x4EF6;</a>&#x600E;&#x9EBC;&#x5BEB;&#x7684;&#x3002;</p>
<blockquote>
<p>Elements and viewports have an associated scrolling box if has a scrolling mechanism or it overflows its content area and the used value of the overflow-x or overflow-y property is hidden.<br>
An element body (which will be the HTML body element) is potentially scrollable if all of the following conditions are true:</p>
<ul>
<li>body has an associated CSS layout box.</li>
<li>body&#x2019;s parent element&#x2019;s computed value of the overflow-x or overflow-y properties is not visible.</li>
<li>body&#x2019;s computed value of the overflow-x or overflow-y properties is not visible.</li>
</ul>
</blockquote>
<p>&#x9019;&#x6BB5;&#x6587;&#x5B57;&#x544A;&#x8A34;&#x6211;&#x5011;&#xFF0C;&#x5982;&#x679C;&#x5143;&#x7D20;&#x662F; scrolling box&#xFF08;&#x6372;&#x52D5;&#x76D2;&#x5B50;&#xFF09;&#x7684;&#x8A71;&#xFF0C;&#x4ED6;&#x6703;&#x6709;&#x6372;&#x52D5;&#x7684;&#x6A5F;&#x5236;&#xFF08;&#x4F8B;&#x5982;&#x6372;&#x8EF8;&#xFF09;&#x6216;&#x662F;&#x4ED6;&#x7684;&#x5167;&#x5BB9;&#x9762;&#x7A4D;&#x8D85;&#x904E;&#x539F;&#x672C;&#x5927;&#x5C0F;&#xFF0C;&#x4E26;&#x4E14;&#x8D85;&#x904E;&#x7684; overflow-x &#x6216; overflow-y &#x88AB;&#x8A2D;&#x5B9A;&#x70BA;&#x96B1;&#x85CF;&#x3002;</p>
<p>&#x9019;&#x908A;&#x6709;&#x5E7E;&#x500B;&#x95DC;&#x9375;&#xFF0C;&#x57FA;&#x672C;&#x4E0A;&#x8981;&#x80FD;&#x6372;&#x52D5;&#x5C31;&#x4ED6;&#x5C31;&#x5FC5;&#x9808;&#x662F;&#x6372;&#x52D5;&#x76D2;&#x5B50;&#x3002;&#x6B64;&#x5916;&#x5982;&#x679C;&#x5143;&#x7D20;&#x8D85;&#x904E;&#x7684;&#x90E8;&#x5206;&#x6C92;&#x6709;&#x88AB;&#x96B1;&#x85CF;&#xFF0C;&#x800C;&#x662F;&#x8A2D;&#x5B9A;&#x70BA;&#x986F;&#x793A;&#xFF0C;&#x90A3;&#x8D85;&#x51FA;&#x7684;&#x5730;&#x65B9;&#x5DF2;&#x7D93;&#x986F;&#x793A;&#x4E86;&#xFF0C;&#x81EA;&#x7136;&#x4E0D;&#x6703;&#x6709;&#x6372;&#x52D5;&#x7684;&#x554F;&#x984C;&#x3002;</p>
<p>&#x7136;&#x5F8C;&#x4ED6;&#x53C8;&#x8AAA;&#x5982;&#x679C;&#x5143;&#x7D20;&#x7684;&#x672C;&#x9AD4;&#x662F;&#x6709;&#x6372;&#x52D5;&#x7684;&#x300C;&#x6F5B;&#x529B;&#x300D;&#xFF0C;&#x5247;&#x6703;&#x6EFF;&#x8DB3;&#xFF1A;</p>
<ul>
<li>&#x662F; layout box</li>
<li>&#x5143;&#x7D20;&#x7684;&#x7236;&#x5143;&#x7D20;&#x4E0D;&#x662F;&#x8A2D;&#x5B9A; overflow &#x70BA;&#x986F;&#x793A;&#xFF08;&#x4E0D;&#x7136;&#x5B50;&#x5143;&#x7D20;&#x4E5F;&#x6703;&#x5957;&#x7528;&#x986F;&#x793A;&#xFF09;</li>
<li>&#x5143;&#x7D20;&#x7684; computed value &#x7684; overflow-x &#x548C; overflow-y &#x4E0D;&#x662F;&#x8A2D;&#x70BA;&#x986F;&#x793A; &#xFF08;computed value &#x5148;&#x524D;<a href="https://ithelp.ithome.com.tw/articles/10191967" target="_blank">&#x6587;&#x7AE0;</a>&#x6709;&#x89E3;&#x91CB;&#x904E;&#xFF09;</li>
</ul>
<p>&#x518D;&#x4F86;&#x8981;&#x89E3;&#x91CB;&#x4E00;&#x4E0B;&#xFF0C;&#x4EC0;&#x9EBC;&#x662F;&#x300C;&#x6709; overflow&#x300D;&#xFF1F;<br>
&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F;&#x300C;&#x8996;&#x7A97;&#x5927;&#x5C0F;&#x300D;&#x5C0F;&#x65BC;&#x300C;&#x5167;&#x5BB9;&#x5927;&#x5C0F;&#x300D;&#x3002;</p>
<hr>
<p>&#x63A5;&#x8457;&#x6211;&#x5011;&#x4F86;&#x8A8D;&#x8B58;&#x5E7E;&#x500B; script &#x7684;&#x7528;&#x6CD5;&#xFF1A;</p>
<pre><code>//&#x5047;&#x8A2D;&#x6709;&#x500B; box &#x5143;&#x7D20;&#x5DF2;&#x7D93;&#x6307;&#x5B9A;&#x597D;&#x4E86;
box.scroll(50, 60);  // &#x6372;&#x52D5;&#x5230; (x: 50, y: 60)
console.log(box.scrollLeft); // 50
console.log(box.scrollTop); // 60
</code></pre>
<p>&#x7B2C;&#x4E00;&#x884C;&#x662F;&#x8A2D;&#x5B9A;&#x6372;&#x5230;&#x54EA;&#x88E1;&#xFF0C;&#x6240;&#x4EE5;&#x662F; setter<br>
&#x7B2C;&#x4E8C;&#x3001;&#x7B2C;&#x4E09;&#x884C;&#x662F;&#x53D6;&#x5F97;&#x6372;&#x5230;&#x54EA;&#x88E1;&#x4E86;&#xFF0C;&#x6240;&#x4EE5;&#x662F; getter</p>
<hr>
<p>&#x597D;&#x4E86;&#xFF0C;&#x8A72;&#x77E5;&#x9053;&#x7684;&#x90FD;&#x77E5;&#x9053;&#x4E86;&#x3002;&#x6211;&#x5011;&#x4E0A;&#x5DE5;&#xFF01;</p>
<p>&#x73FE;&#x5728;&#x6211;&#x5011;&#x60F3;&#x5B8C;&#x6210; <code>scroll</code> setter &#x7684;&#x4E00;&#x90E8;&#x5206;&#xFF0C;&#x6587;&#x4EF6;&#x5728;<a href="https://drafts.csswg.org/cssom-view/#dom-element-scroll" target="_blank">&#x9019;&#x908A;</a>&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A; <code>scroll</code>&#x3001;<code>scrollTop</code>&#x3001;<code>scrollLeft</code> &#x5728; setter &#x7684;&#x5B9A;&#x7FA9;&#x90FD;&#x5F88;&#x63A5;&#x8FD1;&#x3002;<br>
&#x6211;&#x5011;&#x4ECA;&#x5929;&#x60F3;&#x5B8C;&#x6210; <code>scroll</code> setter &#x7684;&#x7B2C;&#x5341;&#x6B65;&#x9A5F;&#x3002;</p>
<p>&#x5176;&#x4ED6;&#x6B65;&#x9A5F;&#x5927;&#x5BB6;&#x53EF;&#x4EE5;&#x81EA;&#x884C;&#x9EDE;&#x9032;&#x53BB;&#x770B;&#xFF0C;&#x9019;&#x908A;&#x5C31;&#x4E0D;&#x9644;&#x4E0A;&#x4E86;&#x3002;&#x7B2C;&#x5341;&#x6B65;&#x662F;&#x8AAA;&#xFF1A;</p>
<blockquote>
<p>If the element does not have any associated CSS layout box, the element has no associated scrolling box, or the element has no overflow, terminate these steps.</p>
</blockquote>
<p>&#x610F;&#x601D;&#x662F;&#x8AAA;&#x5047;&#x8A2D;&#x5143;&#x7D20;&#xFF1A;</p>
<ol>
<li>&#x4E0D;&#x662F; CSS layout box</li>
<li>&#x4E0D;&#x662F; scrolling box</li>
<li>&#x5143;&#x7D20;&#x6C92;&#x6709; overflow</li>
</ol>
<p>&#x6EFF;&#x8DB3;&#x4EE5;&#x4E0A;&#x4E09;&#x9EDE;&#x7684;&#x4EFB;&#x4E00;&#x500B;&#xFF0C;<code>scroll</code> &#x5C31;&#x6703;&#x88AB;&#x7D42;&#x6B62;&#xFF0C;&#x610F;&#x601D;&#x662F;&#x5373;&#x4F7F; script &#x53EB;&#x4F60;&#x5377;&#x52D5;&#xFF0C;&#x4E5F;&#x4E0D;&#x6703;&#x5BE6;&#x969B;&#x53BB;&#x57F7;&#x884C;&#xFF0C;&#x56E0;&#x70BA;&#x4E0D;&#x6EFF;&#x8DB3;&#x53EF;&#x4EE5;&#x6372;&#x52D5;&#x7684;&#x5B9A;&#x7FA9;&#x3002;&#x800C;&#x9019;&#x4E09;&#x9EDE;&#x7279;&#x6027;&#xFF0C;&#x5728;&#x6587;&#x7AE0;&#x4E00;&#x958B;&#x59CB;&#x6211;&#x5011;&#x4FBF;&#x89E3;&#x91CB;&#x904E;&#x4E86;&#x3002;</p>
<hr>
<p>&#x63A5;&#x8457;&#x5C31;&#x53EF;&#x4EE5;&#x5BE6;&#x4F5C;&#x4E86;&#xFF1A;</p>
<p>&#x7B2C;&#x5341;&#x6B65;&#x5176;&#x5BE6;&#x5C31;&#x662F;&#xFF1A;</p>
<pre><code>// Step 10
if !self.has_css_layout_box() ||
   !self.has_scrolling_box() ||
   !self.has_overflow()
{
    return;
}
</code></pre>
<p>&#x9084;&#x6709;&#x6587;&#x7AE0;&#x4E00;&#x958B;&#x59CB;&#x5B9A;&#x7FA9;&#x7684;&#x5E7E;&#x500B;&#x7279;&#x6027;&#xFF1A;</p>
<pre><code>// https://drafts.csswg.org/cssom-view/#scrolling-box
fn has_scrolling_box(&amp;self) -&gt; bool {
    // TODO: scrolling mechanism, such as scrollbar (We don&apos;t have scrollbar yet)
    //       self.has_scrolling_mechanism()
    self.overflow_x_is_hidden() ||
    self.overflow_y_is_hidden()
}

fn has_overflow(&amp;self) -&gt; bool {
    self.ScrollHeight() &gt; self.ClientHeight() ||
    self.ScrollWidth() &gt; self.ClientWidth()
}
</code></pre>
<p>&#x9019;&#x5176;&#x5BE6;&#x662F;&#x4E00;&#x6B21; <a href="https://github.com/servo/servo/commit/9965f7e2cc0f722acfee5f0710b74a84d1112b54" target="_blank">commit</a> &#x6240;&#x5B8C;&#x6210;&#x7684;&#x4E8B;&#x60C5;&#xFF0C;&#x5927;&#x5BB6;&#x6709;&#x8208;&#x8DA3;&#x53EF;&#x4EE5;&#x9EDE;&#x9032;&#x53BB;&#x770B;&#x90A3;&#x6B21;&#x8CA2;&#x737B;&#x7E3D;&#x5171;&#x505A;&#x4E86;&#x54EA;&#x4E9B;&#x4E8B;&#x60C5;&#x3002;</p>
<hr>
<p>&#x5E0C;&#x671B;&#x6709;&#x5E6B;&#x5230;&#x5927;&#x5BB6;&#xFF0C;&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
