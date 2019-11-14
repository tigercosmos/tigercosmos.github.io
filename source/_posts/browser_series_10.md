---
title: 瀏覽器引擎處理版面佈局的簡易版（一）
date: 2017-12-21 23:31:34
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x7D93;&#x904E;&#x5E7E;&#x5929;&#x8EAB;&#x5FC3;&#x8ABF;&#x990A;&#x5F8C;&#xFF0C;&#x6211;&#x5011;&#x518D;&#x56DE;&#x4F86;&#x8A0E;&#x8AD6; robinson &#x9019;&#x500B;&#x300C;&#x73A9;&#x5177;&#x300D;&#x5C08;&#x6848;&#x3002;&#x63A5;&#x8457;&#x6211;&#x5011;&#x4F86;&#x770B; <a href="https://github.com/mbrubeck/robinson/blob/master/src/layout.rs" target="_blank">robinson/src/layout.rs</a> &#x9019;&#x500B;&#x6A21;&#x7D44;&#x3002;&#x5982;&#x679C;&#x4F60;&#x9084;&#x6C92;&#x770B;&#x904E;&#x672C;&#x7CFB;&#x5217;&#x7684;&#x524D;&#x9762;&#x90E8;&#x5206;&#xFF0C;&#x5EFA;&#x8B70;&#x4F60;&#x5148;&#x770B;&#x4E00;&#x4E0B;&#x3002;&#x5982;&#x679C;&#x662F;&#x7CFB;&#x5217;&#x7684;&#x65B0;&#x8B80;&#x8005;&#xFF0C;&#x5EFA;&#x8B70;&#x4F60;&#x5F9E;&#x7B2C;&#x4E00;&#x7BC7;&#x958B;&#x59CB;&#x8B80;&#x3002;</p>
<p>&#x9084;&#x8A18;&#x5F97;&#x700F;&#x89BD;&#x5668;&#x7684;&#x7C21;&#x6613;&#x6B65;&#x9A5F;&#x55CE;&#xFF1F;</p>
<pre><code class="language-sh">DOM tree \
           --&gt; style tree --&gt; layout --&gt; painting
CSS tree /
</code></pre>
<p>&#x524D;&#x5E7E;&#x500B;&#x6B65;&#x9A5F;&#x6211;&#x5011;&#x4E4B;&#x524D;&#x5DF2;&#x7D93;&#x8B1B;&#x904E;&#x4E86;&#x3002;&#x6240;&#x4EE5;&#x63A5;&#x4E0B;&#x4F86;&#x8981;&#x4ECB;&#x7D39; layout&#x3002;&#x800C;&#x9019;&#x500B;&#x6A21;&#x7D44;&#x5C31;&#x5728;&#x5BE6;&#x73FE; layout &#x7684;&#x90E8;&#x5206;&#x3002;</p>
<p>layout&#xFF08;&#x7248;&#x9762;&#x4F48;&#x5C40;&#xFF09;&#x5C31;&#x662F;&#x4E00;&#x5806;&#x7684; box&#xFF08;&#x76D2;&#x5B50;&#xFF09;&#x3002;&#x4E00;&#x500B;&#x76D2;&#x5B50;&#x662F;&#x4E00;&#x500B;&#x7DB2;&#x9801;&#x7684;&#x77E9;&#x5F62;&#x90E8;&#x5206;&#x3002;&#x76D2;&#x5B50;&#x5177;&#x6709;&#x5BEC;&#x5EA6;&#x3001;&#x9AD8;&#x5EA6;&#x548C;&#x9801;&#x9762;&#x4E0A;&#x7684;&#x4F4D;&#x7F6E;&#xFF0C;&#x5F62;&#x6210;&#x4E00;&#x500B;&#x77E9;&#x5F62;&#x3002; &#x9019;&#x500B;&#x77E9;&#x5F62;&#x88AB;&#x7A31;&#x70BA;&#x5167;&#x5BB9;&#x5340;&#xFF0C;&#x56E0;&#x70BA;&#x5167;&#x5BB9;&#x6703;&#x5448;&#x73FE;&#x5728;&#x5340;&#x584A;&#x5167;&#x3002;&#x5167;&#x5BB9;&#x53EF;&#x4EE5;&#x662F;&#x6587;&#x5B57;&#x3001;&#x5716;&#x50CF;&#x3001;&#x5F71;&#x7247;&#x6216;&#x5176;&#x4ED6;&#x5C0F;&#x76D2;&#x5B50;&#x3002;</p>
<p>&#x9019;&#x5F35;&#x5716;&#x7247;&#x5927;&#x5BB6;&#x61C9;&#x8A72;&#x5F88;&#x719F;&#x6089;&#xFF1A;<br>
<img src="https://www.w3.org/TR/CSS2/images/boxdim.png" alt="box"><br>
&#x6216;&#x662F;&#x6709;&#x984F;&#x8272;&#x7684;&#x53EF;&#x80FD;&#x66F4;&#x719F;&#x6089;&#xFF1A;<br>
<img src="https://i.imgur.com/crDJAoT.png" alt="box"><br>
&#x6C92;&#x932F;&#xFF0C;&#x5C31;&#x662F;&#x4F60;&#x6309; F12&#xFF0C;&#x5728;&#x958B;&#x767C;&#x8005;&#x5DE5;&#x5177;&#x4E2D;&#x770B;&#x5230;&#x7684;&#x756B;&#x9762;&#xFF01;</p>
<p>box &#x7684;&#x5468;&#x570D;&#x4E5F;&#x53EF;&#x80FD;&#x6703;&#x6709; padding&#x3001;borders&#x3001;margins &#x7B49;&#x5C6C;&#x6027;&#x3002;&#x5C31;&#x50CF;&#x4E0A;&#x9762;&#x5169;&#x5F35;&#x5716;&#x6240;&#x986F;&#x793A;&#x7684;&#x3002;<br>
<a href="https://www.w3.org/TR/CSS2/box.html" target="_blank">W3C</a>&#x4E5F;&#x6709;&#x5B8C;&#x6574;&#x7684;&#x6587;&#x4EF6;&#x5B9A;&#x7FA9;&#x3002;</p>
<p>&#x9019;&#x908A;&#x9700;&#x8981;&#x5927;&#x5BB6;&#x5C0D; <a href="https://developer.mozilla.org/zh-TW/docs/Web/CSS/padding" target="_blank">padding</a>&#x3001;<a href="https://developer.mozilla.org/zh-TW/docs/Web/CSS/margin" target="_blank">margin</a> &#x6709;&#x66F4;&#x591A;&#x4E86;&#x89E3;&#x3002;&#x96D6;&#x7136;&#x6211;&#x5011;&#x5728;&#x5BE6;&#x4F5C;&#x7C21;&#x55AE;&#x7248;&#x7684; layout &#x6642;&#x4E0D;&#x6703;&#x53BB;&#x8655;&#x7406;&#x9019;&#x4E9B;&#x6027;&#x8CEA;&#xFF0C;&#x4F46;&#x5728;&#x771F;&#x5BE6;&#x7684;&#x700F;&#x89BD;&#x5668;&#x4E2D;&#x78BA;&#x662F;&#x81F3;&#x95DC;&#x91CD;&#x8981;&#xFF0C;&#x771F;&#x6B63;&#x7684;&#x700F;&#x89BD;&#x5668;&#x4E00;&#x9EDE;&#x504F;&#x5DEE;&#x90FD;&#x4E0D;&#x80FD;&#x6709;&#xFF0C;&#x80FD;&#x4E0D;&#x80FD;&#x5C07;&#x6240;&#x6709; box &#x8655;&#x7406;&#x597D;&#xFF0C;&#x5F71;&#x97FF;&#x6700;&#x7D42;&#x7684;&#x7D50;&#x679C;&#x3002;</p>
<p>&#x6B64;&#x5916;&#x50CF;&#x662F; scroll&#x3001;client &#x7B49;&#x7B49;&#x7684;&#x529F;&#x80FD;&#x90FD;&#x6703;&#x9700;&#x8981;&#x597D;&#x7684; box&#x3002;&#x4E0D;&#x7136;&#x5C31;&#x6703;&#x767C;&#x751F;&#x756B;&#x9762;&#x6372;&#x52D5;&#x7684;&#x4F4D;&#x5B50;&#x5C31;&#x6703;&#x662F;&#x932F;&#x7684;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x672C;&#x8EAB;&#x7684;&#x8996;&#x7A97;&#x5927;&#x5C0F;&#x4E5F;&#x4E0D;&#x662F;&#x5C0D;&#x7684;&#x3002;</p>
<p>&#x4EE5;&#x4E0A;&#x7684;&#x5E7E;&#x500B;&#x9023;&#x7D50;&#x5E0C;&#x671B;&#x5927;&#x5BB6;&#x80FD;&#x9EDE;&#x9032;&#x53BB;&#x66F4;&#x8FD1;&#x4E00;&#x6B65;&#x4E86;&#x89E3;&#xFF0C;&#x660E;&#x5929;&#x6211;&#x5011;&#x4F86;&#x770B;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#x3002;</p>
<p>&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
