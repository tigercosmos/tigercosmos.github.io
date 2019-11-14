---
title: 談談 Servo 專案
date: 2017-12-27 23:33:38
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
<h2>&#x524D;&#x8A00;</h2>
<p>&#x4EC0;&#x9EBC;&#x662F; Servo?</p>
<blockquote>
<p>Servo &#x662F;&#x4E00;&#x6B3E;&#x5C08;&#x70BA;&#x61C9;&#x7528;&#x8EDF;&#x9AD4;&#x548C;&#x5D4C;&#x5165;&#x5F0F;&#x61C9;&#x7528;&#x800C;&#x8A2D;&#x8A08;&#x7684;&#x73FE;&#x4EE3;&#x5316;&#x7684;&#x9AD8;&#x6548;&#x80FD;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;</p>
</blockquote>
<h2>&#x7DE3;&#x8D77;</h2>
<p>C++ &#x4E00;&#x76F4;&#x4EE5;&#x4F86;&#x90FD;&#x662F;&#x5F88;&#x68D2;&#x7684;&#x8A9E;&#x8A00;&#xFF0C;&#x5C24;&#x5176;&#x5728;&#x8655;&#x7406;&#x4F4E;&#x968E;&#x7684;&#x7A0B;&#x5F0F;&#x66F4;&#x662F;&#x9069;&#x5408;&#xFF0C;&#x4F46;&#x4ED6;&#x7562;&#x7ADF;&#x4E5F;&#x4E0D;&#x662F;&#x842C;&#x80FD;&#x7684;&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A;&#x4ED6;&#x5728;&#x8655;&#x7406;&#x8A18;&#x61B6;&#x9AD4;&#x591A;&#x7A0B;&#x5E8F;&#x6642;&#xFF0C;&#x6703;&#x6709;&#x5B89;&#x5168;&#x6027;&#x7684;&#x7591;&#x616E;&#xFF0C;&#x50CF;&#x662F;&#x8A18;&#x61B6;&#x9AD4;&#x672A;&#x5982;&#x671F;&#x6E05;&#x9664;&#x3002;</p>
<p>&#x7576;&#x7136;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x7528;&#x500B;&#x56B4;&#x8B39;&#x7684;&#x65B9;&#x5F0F;&#x5BEB; C++&#xFF0C;&#x90A3;&#x9EBC;&#x5F88;&#x591A;&#x4E0D;&#x5B89;&#x5168;&#x7684;&#x908F;&#x8F2F;&#x53EF;&#x80FD;&#x5C31;&#x4E0D;&#x6703;&#x7522;&#x751F;&#xFF0C;&#x4F46;&#x9019;&#x7562;&#x7ADF;&#x4E0D;&#x662F;&#x4E00;&#x500B;&#x597D;&#x7684;&#x89E3;&#x6C7A;&#x65B9;&#x5F0F;&#x3002;&#x6211;&#x5011;&#x5E0C;&#x671B;&#x958B;&#x767C;&#x8005;&#x4E0D;&#x72AF;&#x932F;&#xFF0C;&#x4F46;&#x4E8B;&#x5BE6;&#x4E0A;&#x6700;&#x6703;&#x72AF;&#x932F;&#x7684;&#x5C31;&#x662F;&#x958B;&#x767C;&#x8005;&#xFF01;</p>
<p>Mozilla Firefox &#x700F;&#x89BD;&#x5668;&#x7684;&#x6838;&#x5FC3;&#x5F15;&#x64CE;&#x662F; Gecko&#xFF0C;&#x5C31;&#x662F;&#x7531; C++ &#x6240;&#x64B0;&#x5BEB;&#x3002;&#x800C; Mozilla &#x6DF1;&#x77E5;&#x5B89;&#x5168;&#x6027;&#x554F;&#x984C;&#x5FC5;&#x9808;&#x89E3;&#x6C7A;&#xFF0C;&#x6240;&#x4EE5;&#x4FBF;&#x6709;&#x4E86; Rust &#x8A9E;&#x8A00;&#x4EE5;&#x53CA; Servo &#x5C08;&#x6848;&#x7684;&#x8A95;&#x751F;&#x3002;</p>
<p>&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#xFF0C;<br>
Rust &#x53D6;&#x4EE3; C++<br>
Servo &#x53D6;&#x4EE3; Gecko</p>
<p>&#x4EFB;&#x4E00;&#x500B;&#x90FD;&#x662F;&#x9A5A;&#x5929;&#x52D5;&#x5730;&#xFF0C;&#x9084;&#x4E00;&#x6B21;&#x5169;&#x500B;&#xFF01;</p>
<h2>Rust</h2>
<p>Rust &#x6700;&#x65E9;&#x7531; Mozilla &#x8CC7;&#x52A9;&#x958B;&#x767C;&#xFF0C;&#x5F8C;&#x4F86;&#x56E0;&#x70BA; Dropbox &#x4F7F;&#x7528; Rust &#x6539;&#x5BEB;&#x6A94;&#x6848;&#x7CFB;&#x7D71;&#x670D;&#x52D9;&#x800C;&#x8072;&#x660E;&#x5927;&#x566A;&#x3002;&#x76EE;&#x524D; Rust &#x662F;&#x5F88;&#x6D3B;&#x8E8D;&#x7684;&#x958B;&#x6E90;&#x5C08;&#x6848;&#xFF0C;&#x6709;&#x8D85;&#x904E;&#x5169;&#x5343;&#x540D;&#x958B;&#x767C;&#x8005;&#x5171;&#x540C;&#x958B;&#x767C;&#xFF0C;&#x5927;&#x7D04;&#x4E00;&#x81F3;&#x5169;&#x500B;&#x6708;&#x5C31;&#x6703;&#x6709;&#x4E00;&#x6B21; minor release&#x3002;Rust &#x7684;&#x76EE;&#x6A19;&#x662F;&#x6210;&#x70BA;&#x9AD8;&#x6548;&#x7387;&#x3001;&#x6613;&#x65BC;&#x5E73;&#x884C;&#x904B;&#x7B97;&#x7684;&#x7CFB;&#x7D71;&#x7A0B;&#x5F0F;&#x8A9E;&#x8A00;&#xFF0C;&#x56E0;&#x6B64;&#x5B83;&#x9078;&#x64C7;&#x4E86;&#x4EE5;&#x4E0B;&#x7684;&#x7279;&#x6027;&#xFF1A;</p>
<ul>
<li>&#x975C;&#x614B;&#x578B;&#x5225; (static-typed)</li>
<li>&#x5340;&#x5206; mutable &#x8207; immutable&#xFF0C;&#x6240;&#x6709;&#x8B8A;&#x6578;&#x9810;&#x8A2D;&#x70BA; immutable&#xFF0C;&#x76E1;&#x53EF;&#x80FD;&#x6E1B;&#x5C11; mutable state</li>
<li>&#x4F7F;&#x7528; tagged union &#x8207; pattern matching</li>
<li>&#x4E0D;&#x4F7F;&#x7528;&#x52D5;&#x614B;&#x5783;&#x573E;&#x56DE;&#x6536; (garbage collection)&#xFF0C;&#x800C;&#x4F7F;&#x7528;&#x975C;&#x614B;&#x7684; RAII</li>
<li>&#x4F7F;&#x7528; Move semantics &#x907F;&#x514D;&#x8907;&#x88FD;&#x7269;&#x4EF6;</li>
<li>&#x4F7F;&#x7528; borrow checker &#x78BA;&#x4FDD; memory safety &#x8207; thread safety</li>
</ul>
<h2>Servo</h2>
<p>Servo &#x5C08;&#x6848;&#x6700;&#x65E9;&#x5F9E; 2012 &#x5E74;&#x958B;&#x59CB;&#x70BA;&#x5BE6;&#x9A57;&#x6027;&#x8CEA;&#xFF0C;&#x5F8C;&#x4F86; 2015 &#x5728; CSS &#x4E0A;&#x6709;&#x91CD;&#x5927;&#x7A81;&#x7834;&#xFF0C;2016 &#x6642;&#x6B63;&#x5F0F;&#x91CB;&#x51FA;&#x7B2C;&#x4E00;&#x7248;&#xFF0C;&#x4E26;&#x53EF;&#x4EE5;&#x6B63;&#x78BA;&#x6E32;&#x67D3;&#x4EE5;&#x53CA;&#x6548;&#x80FD;&#x6BD4; Gecko &#x66F4;&#x597D;&#xFF0C;&#x65BC;&#x662F; Mozilla &#x4FBF;&#x6709;&#x4E86;&#x91CF;&#x5B50;&#x5C08;&#x6848;&#xFF0C;&#x628A; Servo &#x5C08;&#x6848;&#x4E2D;&#x6700;&#x6210;&#x719F;&#x7684; CSS &#x6A21;&#x7D44;&#xFF0C;&#x4E5F;&#x5C31;&#x662F; Stylo &#x6574;&#x5408;&#x9032; Gecko&#xFF0C;&#x4F7F;&#x5F97;&#x901F;&#x5EA6;&#x548C;&#x6548;&#x80FD;&#x8B8A;&#x66F4;&#x597D;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x4ECA;&#x5E74; 2017/11 &#x6B63;&#x5F0F;&#x767C;&#x8868;&#x7684;&#x65B0;&#x7248; Firefox&#x3002;</p>
<p>&#x672C;&#x4F86;&#x9810;&#x671F;&#x662F;&#x5E0C;&#x671B; Servo &#x80FD;&#x5B8C;&#x5168;&#x53D6;&#x4EE3; Gecko&#xFF0C;&#x4E0D;&#x904E;&#x5149;&#x662F;&#x7DAD;&#x8B77; Firefox&#xFF0C;Mozilla &#x5C31;&#x5E7E;&#x4E4E;&#x6C92;&#x4EC0;&#x9EBC;&#x9918;&#x529B;&#x4E86;&#xFF0C;&#x6295;&#x5165;&#x65B0;&#x7684; Servo &#x7684;&#x4EBA;&#x529B;&#x5C31;&#x5F88;&#x5C11;&#xFF0C;&#x9032;&#x5C55;&#x4E5F;&#x5C31;&#x5F88;&#x56F0;&#x96E3;&#x3002;&#x9577;&#x9060;&#x4F86;&#x770B; Servo &#x548C; Gecko &#x61C9;&#x8A72;&#x6703;&#x4E92;&#x76F8;&#x642D;&#x914D;&#xFF0C;&#x8981;&#x9054;&#x5230;&#x5B8C;&#x5168;&#x5207;&#x5272;&#x53D6;&#x4EE3;&#x6050;&#x6015;&#x5F88;&#x96E3;&#x3002;&#x96D6;&#x7136;&#x80FD;&#x6295;&#x5165;&#x7684;&#x4EBA;&#x529B;&#x5F88;&#x5C11;&#xFF0C;&#x503C;&#x5F97;&#x6176;&#x5E78;&#x7684;&#x662F; Servo &#x7684;&#x5FD7;&#x9858;&#x8CA2;&#x737B;&#x8005;&#x6578;&#x91CF;&#x53EF;&#x89C0;&#xFF0C;&#x9019;&#x662F;&#x56E0;&#x70BA;&#x4E0D;&#x540C;&#x65BC; Firefox &#x820A;&#x6642;&#x4EE3;&#x7684;&#x958B;&#x767C;&#x6D41;&#x7A0B;&#xFF0C;Servo &#x63A1;&#x7528; Github &#x7D93;&#x71DF;&#x793E;&#x7FA4;&#xFF0C;&#x4E26;&#x900F;&#x904E;&#x8A31;&#x591A; bot &#x4F86;&#x9054;&#x5230;&#x81EA;&#x52D5;&#x5316;&#x7684;&#x6B65;&#x9A5F;&#xFF0C;&#x6574;&#x9AD4;&#x7684;&#x958B;&#x767C;&#x9AD4;&#x9A57;&#x975E;&#x5E38;&#x9806;&#x66A2;&#xFF0C;&#x793E;&#x7FA4;&#x4E5F;&#x975E;&#x5E38;&#x53CB;&#x5584;&#xFF0C;&#x8B93; Servo &#x4E0A;&#x7684;&#x958B;&#x767C;&#x8005;&#x975E;&#x5E38;&#x84EC;&#x52C3;&#x3002;&#x81F3;&#x65BC;&#x6211;&#x5247;&#x662F;&#x6E34;&#x671B;&#x770B;&#x5230; Servo &#x5B8C;&#x5168;&#x6210;&#x719F;&#x7684;&#x4E00;&#x5929;&#xFF0C;&#x89BA;&#x5F97;&#x5C07;&#x6703;&#x662F;&#x5283;&#x6642;&#x4EE3;&#x7684;&#x7A81;&#x7834;&#xFF01;</p>
<p>&#x6B64;&#x5916; Servo &#x548C; Rust &#x6709;&#x5171;&#x751F;&#x95DC;&#x4FC2;&#xFF0C;&#x57FA;&#x672C;&#x4E0A; Servo &#x53EF;&#x4EE5;&#x8AAA;&#x662F; Rust &#x7684;&#x6700;&#x5927;&#x8A66;&#x9A57;&#x5E73;&#x53F0;&#x3002;Servo &#x5C08;&#x6848;&#x540C;&#x6642;&#x4E5F;&#x548C; W3C &#x7684;<a href="https://github.com/w3c/web-platform-tests" target="_blank">&#x7DB2;&#x8DEF;&#x5E73;&#x53F0;&#x6E2C;&#x8A66;</a> &#x5C08;&#x6848;&#x540C;&#x6B65;&#xFF0C;&#x5F8C;&#x8005;&#x662F;&#x5C08;&#x9580;&#x6E2C;&#x8A66;&#x700F;&#x89BD;&#x5668;&#x662F;&#x5426;&#x7B26;&#x5408; W3C &#x6A19;&#x6E96;&#x7684;&#x6E2C;&#x8A66;&#x5C08;&#x6848;&#x3002;&#x6B64;&#x5916; Servo &#x5C08;&#x6848;&#x4E5F;&#x5B8C;&#x5168;&#x7167; <a href="https://whatwg.org/" target="_blank">WHATWG</a> &#x7684;&#x700F;&#x89BD;&#x5668;&#x898F;&#x7BC4;&#x5BE6;&#x4F5C;&#x3002;</p>
<blockquote>
<p>&#x7DB2;&#x9801;&#x8D85;&#x6587;&#x5B57;&#x61C9;&#x7528;&#x6280;&#x8853;&#x5DE5;&#x4F5C;&#x5C0F;&#x7D44;&#xFF08;Web Hypertext Application Technology Working Group, WHATWG&#xFF09;&#xFF0C;&#x662F;&#x4E00;&#x500B;&#x4EE5;&#x63A8;&#x52D5;&#x7DB2;&#x8DEF;HTML&#x6A19;&#x6E96;&#x70BA;&#x76EE;&#x7684;&#x800C;&#x6210;&#x7ACB;&#x7684;&#x7D44;&#x7E54;&#x3002;&#x5728;2004&#x5E74;&#xFF0C;&#x7531;Apple&#x516C;&#x53F8;&#x3001;Mozilla&#x57FA;&#x91D1;&#x6703;&#x548C;Opera&#x8EDF;&#x9AD4;&#x516C;&#x53F8;&#x6240;&#x7D44;&#x6210;&#x3002;</p>
</blockquote>
<hr>
<h2>&#x9023;&#x7D50;</h2>
<p><a href="https://github.com/servo/servo" target="_blank">Servo Github</a><br>
<a href="https://download.servo.org/zh-TW/index.html" target="_blank">&#x4E0B;&#x8F09; Servo</a> &#x4F86;&#x9AD4;&#x9A57;&#x770B;&#x770B;<br>
<a href="https://servo.org/zh-TW/index.html" target="_blank">Servo &#x4E2D;&#x6587;&#x5B98;&#x7DB2;</a><br>
<a href="https://www.rust-lang.org/en-US/" target="_blank">Rust</a><br>
<a href="https://doc.rust-lang.org/book/first-edition/" target="_blank">Rust book</a><br>
<a href="http://bholley.net/blog/2017/stylo.html" target="_blank">how stylp brough rust and servo to firefox</a></p>
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
                
