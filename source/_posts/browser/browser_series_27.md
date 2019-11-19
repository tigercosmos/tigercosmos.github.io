---
title: 瀏覽器快速與平行化佈局（ㄧ）
date: 2018-01-07 23:50:14
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x4ECA;&#x5929;&#x7814;&#x7A76;&#x8AD6;&#x6587;&#xFF1A; <a href="https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.207.1244&amp;rep=rep1&amp;type=pdf" target="_blank">Fast and Parallel Webpage Layout</a></p>
<blockquote>
<p>&#x8AD6;&#x6587;&#x4F5C;&#x8005;&#x70BA; Leo A. Meyerovich &#x548C; Rastislav Bod&#xED;k&#xFF0C;&#x65BC; 2010 &#x5E74;&#x767C;&#x8868;&#x3002;<br>
&#x672C;&#x7BC7;&#x6587;&#x7AE0;&#x5716;&#x7247;&#x4F86;&#x81EA;&#x539F;&#x59CB;&#x8AD6;&#x6587;</p>
</blockquote>
<p>&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x6EFF;&#x65E9;&#x7684;&#xFF0C;&#x6211;&#x60F3;&#x5927;&#x6982;&#x4E5F;&#x7B97;&#x662F;&#x700F;&#x89BD;&#x5668;&#x958B;&#x767C;&#x4EE5;&#x5E73;&#x884C;&#x5316;&#x6280;&#x8853;&#x70BA;&#x4E3B;&#x9AD4;&#x7684;&#x5148;&#x92D2;&#x4E86;&#x3002;&#x88E1;&#x9762;&#x5F88;&#x591A;&#x6982;&#x5FF5;&#x6211;&#x90FD;&#x6709;&#x5728;&#x6700;&#x65B0;&#x7684; Firefox <a href="https://hacks.mozilla.org/2017/11/entering-the-quantum-era-how-firefox-got-fast-again-and-where-its-going-to-get-faster/" target="_blank">&#x770B;&#x5230;&#x5F71;&#x5B50;</a>&#x3002;&#x50CF;&#x662F;&#x8A08;&#x7B97;&#x8CC7;&#x6E90;&#x8ABF;&#x914D;&#x3001;&#x8A08;&#x7B97; tree &#x7684;&#x5E73;&#x884C;&#x5316;&#xFF0C;&#x96D6;&#x7136;&#x8AAA;&#x4E00;&#x4E9B;&#x5BE6;&#x4F5C;&#x65B9;&#x5F0F;&#x90FD;&#x4E0D;&#x96E3;&#x60F3;&#x5230;&#xFF0C;&#x4F46;&#x6211;&#x60F3;&#x65E9;&#x671F;&#x7684;&#x7814;&#x7A76;&#x5C0D;&#x5F8C;&#x4F86;&#x7684;&#x767C;&#x5C55;&#x4ECD;&#x6709;&#x5F71;&#x97FF;&#x3002;</p>
<p>&#x4E0D;&#x904E;&#x9019;&#x4E00;&#x7BC7;&#x5728;&#x6F14;&#x7B97;&#x6CD5;&#x7684;&#x90E8;&#x5206;&#x6709;&#x7279;&#x5225;&#x8457;&#x58A8;&#xFF0C;&#x6709;&#x5F88;&#x591A;&#x865B;&#x64EC;&#x78BC;&#xFF0C;&#x6B64;&#x5916;&#x95DC;&#x65BC;&#x5B57;&#x9AD4;&#x986F;&#x793A;&#x7B97;&#x662F;&#x7368;&#x5275;&#xFF0C;&#x8B1B;&#x4E86;&#x5F88;&#x591A;&#x5BE6;&#x4F5C;&#x7684;&#x7D30;&#x7BC0;&#x3002;&#x4EE5;&#x4E0B;&#x5C31;&#x4F86;&#x4ECB;&#x7D39;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#xFF0C;&#x591A;&#x534A;&#x662F;&#x8AD6;&#x6587;&#x4E2D;&#x7684;&#x89C0;&#x9EDE;&#xFF0C;&#x7D93;&#x904E;&#x6211;&#x7684;&#x7406;&#x89E3;&#x5F8C;&#x91CD;&#x65B0;&#x8A6E;&#x91CB;&#x3002;</p>
<hr>
<p>&#x4ECA;&#x5929;&#x8981;&#x8AC7;&#x7684;&#x8AD6;&#x6587;&#x7684;&#x6838;&#x5FC3;&#x6982;&#x5FF5;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34651274-176a264e-f409-11e7-94b5-5f881711e364.png" alt></p>
<p>&#x9019;&#x5F35;&#x5716;&#x986F;&#x793A;&#x4E86;&#x9019;&#x500B;&#x7814;&#x7A76;&#x5E73;&#x884C;&#x5316;&#x7684;&#x6D41;&#x7A0B;&#xFF0C;&#x5176;&#x4E2D;&#x5206;&#x70BA;&#x56DB;&#x5927;&#x9EDE;&#xFF1A;</p>
<ul>
<li>&#x9078;&#x64C7;&#x5668;&#x5339;&#x914D;&#xFF08;selector matching&#xFF1A;1</li>
<li>box &#x548C; text &#x4F48;&#x5C40;: 2, 4~6</li>
<li>&#x5B57;&#x5F62;&#x8655;&#x7406;: 3</li>
<li>&#x4E0A;&#x8272;&#x548C;&#x6E32;&#x67D3;: 7</li>
</ul>
<blockquote>
<p>&#x9019;&#x908A;&#x5E6B;&#x5927;&#x5BB6;&#x8907;&#x7FD2;&#x4E00;&#x4E0B;&#x672C;&#x7CFB;&#x6587;&#x7AE0;&#xFF0C;&#x9078;&#x64C7;&#x5668;&#x5339;&#x914D;&#x53EF;&#x4EE5;&#x770B;<a href="https://ithelp.ithome.com.tw/articles/10192102" target="_blank">&#x9019;&#x7BC7;</a>&#xFF0C;&#x95DC;&#x65BC;&#x4F48;&#x5C40;&#x53EF;&#x4EE5;&#x770B;<a href="https://ithelp.ithome.com.tw/articles/10193108" target="_blank">&#x9019;&#x7BC7;</a>&#xFF06;<a href="https://ithelp.ithome.com.tw/articles/10193340" target="_blank">&#x9019;&#x7BC7;</a>&#xFF0C;&#x756B;&#x9762;&#x8F38;&#x51FA;&#x770B;<a href="https://ithelp.ithome.com.tw/articles/10193573" target="_blank">&#x9019;&#x7BC7;</a>&#x3002;&#x9019;&#x4E9B;&#x90FD;&#x662F;&#x300C;&#x7C21;&#x6613;&#x7248;&#x300D;&#x7684;&#x5BE6;&#x4F5C;&#xFF0C;&#x770B;&#x61C2;&#x4E86;&#x518D;&#x4F86;&#x770B;&#x8AD6;&#x6587;&#xFF0C;&#x6703;&#x6709;&#x66F4;&#x6DF1;&#x7684;&#x9AD4;&#x6703;&#x3002;</p>
</blockquote>
<hr>
<p>&#x9996;&#x5148;&#x662F;&#x9078;&#x64C7;&#x5668;&#x5339;&#x914D;&#x7684;&#x90E8;&#x5206;&#xFF0C;&#x4F5C;&#x8005;&#x91DD;&#x5C0D;&#x300C;&#x4E00;&#x822C;&#x7684;&#x300D;CSS &#x9032;&#x884C;&#x512A;&#x5316;&#xFF0C;&#x300C;&#x4E00;&#x822C;&#x300D;&#x5B9A;&#x7FA9;&#x5728;&#x4E0B;&#x5716;&#xFF08;6&#xFF09;&#x7684;&#xFF08;a&#xFF09;&#xFF0C;&#x4F8B;&#x5982; <code>&lt;div id=&quot;account&quot; class=&quot;first,on&quot;/&gt;</code>&#x6703;&#x5C0D;&#x61C9; <code>div.first</code>&#xFF0C;&#x7576;&#x904B;&#x7B97;&#x5B50;&#x70BA; <code>s1 &lt; s2</code>&#xFF0C;&#x4EE3;&#x8868; s2 &#x5728; s1 &#x4E4B;&#x4E0B;&#xFF0C;&#x9019;&#x985E;&#x578B;&#x7684; CSS &#x7D04;&#x83AB;&#x4F54;&#x7DB2;&#x7AD9;&#x7684; 99%&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5E7E;&#x4E4E;&#x5305;&#x542B;&#x6240;&#x6709;&#x4E86;&#xFF0C;&#x7136;&#x5F8C;&#x6703;&#x88AB;&#x8F49;&#x63DB;&#x6210;&#xFF08;b&#xFF09;&#x7684;&#x5F62;&#x5F0F;</p>
<p><img src="https://user-images.githubusercontent.com/18013815/34651907-3efef794-f412-11e7-861a-a6baefcf98ef.png" alt></p>
<p>&#x63A5;&#x8457;&#x4F5C;&#x8005;&#x5728;&#x8655;&#x7406;&#x5339;&#x914D;&#x7684;&#x6F14;&#x7B97;&#x6CD5;&#x7528;&#x5230;&#x5E7E;&#x500B;&#x6280;&#x5DE7;&#xFF1A;</p>
<ul>
<li>&#x96DC;&#x6E4A;&#xFF1A;&#x4ED6;&#x5728; CSS &#x7684;&#x9078;&#x64C7;&#x5668;&#x4F7F;&#x7528;&#x96DC;&#x6E4A;&#x8868;&#x5206;&#x985E;&#xFF0C;&#x4F8B;&#x5982;&#x6709;&#x95DC; img &#x7684; CSS&#x5206;&#x70BA;&#x4E00;&#x985E;&#xFF0C;&#x78B0;&#x5230;&#x6709; img &#x7684; node&#xFF0C;&#x53EA;&#x8981;&#x53BB;&#x627E; img &#x985E;&#x5225;&#x7684; stylesheet&#x3002;</li>
<li>&#x5F9E;&#x53F3;&#x908A;&#x627E;&#xFF1A;&#x4E00;&#x822C;&#x662F;&#x5F9E;&#x5DE6;&#x908A;&#x627E;&#x8D77;&#xFF0C;&#x4F8B;&#x5982; <code>div #id1</code>&#xFF0C;&#x6703;&#x5148;&#x627E; <code>div</code> &#x518D;&#x53BB;&#x627E; <code>#id1</code>&#x3002;&#x4F46;&#x4F5C;&#x8005;&#x8A8D;&#x70BA;&#x901A;&#x5E38;&#x5F9E;&#x53F3;&#x908A;&#x627E;&#x8D77;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x627E;&#x5230;&#x5C0D;&#x8C61;&#xFF0C;&#x53CD;&#x800C;&#x6BD4;&#x8F03;&#x5FEB;&#x3002;&#xFF08;&#x53EF;&#x80FD;&#x53EF;&#x4EE5;&#x505A;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#xFF0C;&#x8B93;&#x6211;&#x5011;&#x6C7A;&#x5B9A;&#x54EA;&#x4E9B;&#x72C0;&#x6CC1;&#x5F9E;&#x5DE6;&#x908A;&#xFF0C;&#x54EA;&#x4E9B;&#x72C0;&#x6CC1;&#x5F9E;&#x53F3;&#x908A;&#xFF09;</li>
<li>&#x9810;&#x8655;&#x7406;&#xFF1A;CSS &#x4E0D;&#x6703;&#x505A;&#x8A9E;&#x6CD5;&#x6AA2;&#x67E5;&#x3002;&#x6240;&#x4EE5;&#x53EF;&#x4EE5;&#x5148;&#x6392;&#x9664;&#x4E00;&#x4E9B;&#x5197;&#x7A0B;&#x5F0F;&#x78BC;&#x3002;&#x4F8B;&#x5982;&#xFF0C;&#x591A;&#x500B;&#x9078;&#x64C7;&#x5668;&#x5176;&#x5BE6;&#x53EF;&#x4EE5;&#x5408;&#x4F75;&#xFF0C;&#x50CF;&#x662F; <code>div { color }</code> &#x548C; <code>div { padding }</code> &#x9019;&#x5169;&#x500B;&#x90FD;&#x662F;&#x91DD;&#x5C0D; <code>div</code>&#xFF0C;&#x5982;&#x679C;&#x5408;&#x4F75;&#x7684;&#x8A71;&#x53EF;&#x4EE5;&#x6E1B;&#x5C11;&#x67E5;&#x8A62;&#x5339;&#x914D;&#x7684;&#x6B21;&#x6578;&#x3002;</li>
<li>&#x96DC;&#x6E4A;&#x5E73;&#x92EA;&#xFF08;hash tiling)&#xFF1A;&#x4F3C;&#x4E4E;&#x662F;&#x628A;&#x96DC;&#x6E4A;&#x8868;&#x91CD;&#x65B0;&#x5283;&#x5206;&#x3002;&#x56E0;&#x70BA;&#x5FEB;&#x53D6;&#x5927;&#x5C0F;&#x6709;&#x9650;&#xFF0C;&#x907F;&#x514D;&#x7121;&#x610F;&#x7FA9;&#x7684;&#x67E5;&#x8A62;&#xFF0C;&#x5C07;&#x8981;&#x8655;&#x7406;&#x7684;&#x6771;&#x897F;&#x5148;&#x5206;&#x914D;&#x597D;&#xFF0C;&#x78BA;&#x5B9A;&#x5728;&#x7576;&#x4E0B;&#x7684;&#x5FEB;&#x53D6;&#x5927;&#x5C0F;&#x4E0B;&#x53EF;&#x4EE5;&#x5B8C;&#x6210;&#x5DE5;&#x4F5C;&#xFF0C;&#x4EE5;&#x6B64;&#x70BA;&#x524D;&#x63D0;&#x9032;&#x884C;&#x91CD;&#x65B0;&#x5283;&#x5206;&#x3002;</li>
<li>&#x5E8F;&#x865F;&#x5316;&#xFF1A;&#x628A; DOM &#x7684;&#x5C6C;&#x6027;&#x548C; CSS &#x540C;&#x6A23;&#x540D;&#x7A31;&#x7684;&#x63DB;&#x6210;&#x4E00;&#x6A23;&#x7684;&#x6578;&#x5B57;&#xFF0C;&#x5339;&#x914D;&#x901F;&#x5EA6;&#x6703;&#x52A0;&#x5FEB;&#xFF0C;&#x800C;&#x4E14;&#x4E4B;&#x5F8C;&#x5982;&#x679C;&#x8981;&#x9032;&#x884C;&#x6BD4;&#x5927;&#x5C0F;&#x7684;&#x5224;&#x65B7;&#xFF0C;&#x6703;&#x66F4;&#x5BB9;&#x6613;&#x3002;</li>
<li>&#x5E73;&#x884C;&#x8655;&#x7406;&#x6A39;&#xFF1A;&#x6A39;&#x6709;&#x5F88;&#x591A;&#x6A39;&#x679D;&#xFF0C;&#x6240;&#x4EE5;&#x53EF;&#x4EE5;&#x540C;&#x6642;&#x8DD1;&#x597D;&#x5E7E;&#x500B;&#x6A39;&#x679D;&#x3002;&#x9019;&#x8DDF;&#x6211;&#x5011;&#x4E4B;&#x524D;&#x6587;&#x7AE0;&#x63D0;&#x5230;&#x6982;&#x5FF5;&#x4E00;&#x6A23;&#x3002;</li>
<li>&#x8ABF;&#x6574;&#x8CC7;&#x6E90;&#xFF1A;&#x54EA;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#x88AB;&#x5206;&#x914D;&#x7684;&#x9078;&#x64C7;&#x5668;&#x770B;&#x8D77;&#x4F86;&#x6BD4;&#x8F03;&#x591A;&#x5DE5;&#x4F5C;&#xFF0C;&#x5C31;&#x5206;&#x5C11;&#x4E00;&#x9EDE;&#x5176;&#x4ED6;&#x9078;&#x64C7;&#x5668;&#x7D66;&#x4ED6;&#x3002;&#x9019;&#x500B;&#x6982;&#x5FF5;&#x6211;&#x5011;&#x4E4B;&#x524D;&#x4E5F;&#x63D0;&#x5230;&#x904E;&#x3002;</li>
<li>&#x9810;&#x5148;&#x7559;&#x8A18;&#x61B6;&#x7A7A;&#x9593;&#xFF1A;&#x4E00;&#x822C;&#x90FD;&#x662F;&#x9700;&#x8981;&#x624D;&#x53EB;&#x7A7A;&#x9593;&#xFF0C;&#x73FE;&#x5728;&#x5148;&#x4FDD;&#x7559;&#x3002;&#xFF08;&#x6E1B;&#x5C11;I/O&#x6642;&#x9593;&#xFF0C;&#x4F46;&#x5F88;&#x5403;&#x8CC7;&#x6E90;&#xFF09;</li>
<li>&#x5EF6;&#x9072;&#x63D2;&#x5165; rules&#xFF1A;&#x7B49;&#x6578;&#x91CF;&#x5230;&#x4E00;&#x5B9A;&#x7A0B;&#x5EA6;&#x624D;&#x4E00;&#x6B21;&#x63D2;&#x5165;&#x3002;</li>
<li>&#x4E0D;&#x4F7F;&#x7528; STL&#xFF1A;STL &#x4F3C;&#x4E4E;&#x4E0D;&#x662F;&#x5E73;&#x884C;&#x7684;&#x6A23;&#x5B50;&#xFF0C;&#x6240;&#x4EE5;&#x4F5C;&#x8005;&#x81EA;&#x5DF1;&#x5BEB;&#x4E86;&#x4E00;&#x500B;&#x4F86;&#x505A;&#x8CC7;&#x6599;&#x8655;&#x7406;</li>
</ul>
<p>&#x7D93;&#x904E;&#x4EE5;&#x4E0A;&#x5E7E;&#x9EDE;&#x8655;&#x7406;&#x3002;&#x4F5C;&#x8005;&#x5F97;&#x5230;&#x7D50;&#x8AD6;&#xFF1A;</p>
<ul>
<li>&#x96DC;&#x6E4A;&#x5E73;&#x92EA;&#x53EF;&#x4EE5;&#x5FEB; 3&#x500D;</li>
<li>&#x5E73;&#x884C;&#x8655;&#x7406;&#x6A39;&#xFF0B;&#x9810;&#x8655;&#x7406;&#x53EF;&#x4EE5;&#x5FEB; 4&#xFF5E;13 &#x500D;&#x4E4B;&#x9593;</li>
<li>&#x628A;&#x4E0A;&#x9762;&#x6240;&#x6709;&#x7684;&#x65B9;&#x6CD5;&#x52A0;&#x9032;&#x4F86;&#x6700;&#x5FEB;&#x53EF;&#x4EE5;&#x5230; 25 &#x500D;</li>
</ul>
<p>&#x9019;&#x908A;&#x4F5C;&#x8005;&#x6709;&#x8A0E;&#x8AD6;&#x5230;&#x5E73;&#x884C;&#x5316;&#x7684;&#x65B9;&#x6CD5;&#x4E0D;&#x540C;&#x7684;&#x512A;&#x7F3A;&#x9EDE;&#xFF0C;&#x4F46;&#x5DEE;&#x5225;&#x53EA;&#x662F;&#x4ED6;&#x7528;&#x4E0D;&#x540C;&#x7684;&#x5957;&#x4EF6;&#xFF0C;&#x4E0D;&#x662F;&#x91CD;&#x9EDE;&#x5C31;&#x4E0D;&#x8A0E;&#x8AD6;&#x4E86;&#x3002;<br>
&#x4F5C;&#x8005;&#x7684;&#x5BE6;&#x9A57;&#x6578;&#x64DA;&#xFF0C;&#x7528; Safari on the 2.4GHz Intel Core 2 Duo MacBook Pro &#x539F;&#x672C;&#x8981; 204 ms &#x73FE;&#x5728;&#x53EA;&#x8981;&#x82B1; 3.5 ms&#x3002;&#x4ED6;&#x4F30;&#x8A08;&#xFF0C;&#x624B;&#x6A5F;&#x539F;&#x672C;&#x8981; 3.5s &#x7684;&#x8A71;&#xFF0C;&#x73FE;&#x5728;&#x53EA;&#x8981; 50ms&#x3002;&#x4E0D;&#x904E;&#x9019;&#x53EA;&#x662F;&#x4ED6;&#x731C;&#x6E2C;&#x800C;&#x5DF2;&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A;&#x6211;&#x4E0D;&#x8A8D;&#x70BA;&#x624B;&#x6A5F;&#x6703;&#x6709;&#x9019;&#x9EBC;&#x597D;&#x7684;&#x6548;&#x679C;&#xFF0C;&#x624B;&#x6A5F;&#x8655;&#x7406;&#x5668;&#x8A08;&#x7B97;&#x80FD;&#x529B;&#x4ECD;&#x7136;&#x4E0D;&#x5F37;&#xFF0C;&#x6B64;&#x5916;&#x6709;&#x6C92;&#x6709;&#x5B8C;&#x5168;&#x652F;&#x63F4;&#x5E73;&#x884C;&#x8655;&#x7406;&#x4E5F;&#x6709;&#x5F85;&#x78BA;&#x8A8D;&#x3002;</p>
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
                
