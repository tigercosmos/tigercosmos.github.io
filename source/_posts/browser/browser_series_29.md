---
title: 瀏覽器快速與平行化佈局（二）
date: 2018-01-09 23:32:51
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x672C;&#x7BC7;&#x63A5;&#x7E8C;<a href="https://ithelp.ithome.com.tw/articles/10196381/" target="_blank">&#x4E4B;&#x524D;&#x4E00;&#x7BC7;</a></p>
<hr>
<p>&#x7814;&#x7A76;&#x8AD6;&#x6587;&#xFF1A; <a href="http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.207.1244&amp;rep=rep1&amp;type=pdf" target="_blank">Fast and Parallel Webpage Layout</a></p>
<blockquote>
<p>&#x8AD6;&#x6587;&#x4F5C;&#x8005;&#x70BA; Leo A. Meyerovich &#x548C; Rastislav Bod&#xED;k&#xFF0C;&#x65BC; 2010 &#x5E74;&#x767C;&#x8868;&#x3002;<br>
&#x672C;&#x7BC7;&#x6587;&#x7AE0;&#x5716;&#x7247;&#x4F86;&#x81EA;&#x539F;&#x59CB;&#x8AD6;&#x6587;</p>
</blockquote>
<hr>
<p>&#x56DE;&#x9867;&#x4E00;&#x4E0B;&#x6838;&#x5FC3;&#x6982;&#x5FF5;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34651274-176a264e-f409-11e7-94b5-5f881711e364.png" alt></p>
<hr>
<p>&#x597D;&#x7684;&#x63A5;&#x8457;&#x8B1B;&#x7B2C;&#x4E8C;&#x90E8;&#x5206;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x8655;&#x7406; tree &#x7684;&#x5E73;&#x884C;&#x5316;</p>
<p><img src="https://user-images.githubusercontent.com/18013815/34727498-0e45dce0-f592-11e7-9c95-0c38f7bd1970.png" alt></p>
<p>&#x9019;&#x908A;&#x63D0;&#x5230;&#x4E00;&#x500B;&#x6982;&#x5FF5;&#xFF0C;&#x56E0;&#x70BA; child &#x7E7C;&#x627F;&#x7684;&#x5C6C;&#x6027;&#x6703;&#x76F4;&#x63A5;&#x84CB;&#x6389; parent&#xFF0C;&#x6240;&#x4EE5;&#x5728;&#x7B97;&#x5C6C;&#x6027;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x56E0;&#x70BA;&#x4E0A;&#x4E0B;&#x5F7C;&#x6B64;&#x7368;&#x7ACB;&#xFF0C;&#x4E5F;&#x5C31;&#x6709;&#x6A5F;&#x6703;&#x5E73;&#x884C;&#x5316;&#x3002;&#x6B64;&#x5916;&#x540C;&#x500B; node &#x7684;&#x591A;&#x500B;&#x5C6C;&#x6027;&#x540C;&#x6642;&#x4E5F;&#x53EF;&#x4EE5;&#x5206;&#x958B;&#x7B97;&#x3002;&#x4E0A;&#x9762;&#x5C31;&#x662F;&#x5979;&#x7684;&#x6982;&#x5FF5;&#x7684;&#x865B;&#x64EC;&#x78BC;&#xFF0C;&#x4E0D;&#x904E;&#x9019;&#x6A23;&#x770B;&#x4E0B;&#x4F86;&#x5176;&#x5BE6;&#x6EFF;&#x62BD;&#x8C61;&#x7684;&#xFF0C;&#x5E73;&#x884C;&#x5316;&#x5BE6;&#x969B;&#x57F7;&#x884C;&#x6703;&#x78B0;&#x5230;&#x5F88;&#x591A;&#x56F0;&#x96E3;&#xFF0C;&#x4F46;&#x662F;&#x8AD6;&#x6587;&#x901A;&#x5E38;&#x53EA;&#x8AAA;&#x4ED6;&#x600E;&#x505A;&#xFF0C;&#x81F3;&#x65BC;&#x9019;&#x6A23;&#x505A;&#x6703;&#x767C;&#x751F;&#x600E;&#x6A23;&#x7684;&#x56F0;&#x96E3;&#x4E0D;&#x89AA;&#x81EA;&#x8A66;&#x8A66;&#x770B;&#x4E5F;&#x4E0D;&#x77E5;&#x9053;&#x3002;</p>
<p>&#x7E3D;&#x4E4B;&#x4ED6;&#x6709;&#x756B;&#x51FA;&#x4ED6;&#x7684;&#x7D50;&#x679C;<br>
<img src="https://user-images.githubusercontent.com/18013815/34727751-ca88b242-f592-11e7-8b0e-e3d12f48b6bb.png" alt><br>
&#x770B;&#x8D77;&#x4F86;&#x53EF;&#x4EE5;&#x5FEB; 2~4 &#x500D;&#x3002;</p>
<hr>
<p>&#x518D;&#x4F86;&#x662F;&#x8655;&#x7406;&#x5B57;&#x578B;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34727925-5a6fb7de-f593-11e7-811b-38977066dbc7.png" alt></p>
<p>&#x9019;&#x908A;&#x8AD6;&#x6587;&#x6C92;&#x6709;&#x8B1B;&#x5F88;&#x8A73;&#x7D30;&#x7684;&#x64CD;&#x4F5C;&#x6B65;&#x9A5F;&#xFF0C;&#x4F46;&#x6982;&#x5FF5;&#x5C31;&#x662F;&#x5F97;&#x5230; layout tree &#x7684;&#x6642;&#x5019;&#xFF0C;&#x5176;&#x5BE6;&#x6211;&#x5011;&#x5C31;&#x77E5;&#x9053;&#x6BCF;&#x500B;&#x5B57;&#x5143;&#x7684;&#x5404;&#x7A2E;&#x7279;&#x6027;&#xFF08;&#x5927;&#x5C0F;&#x3001;&#x984F;&#x8272;&#x3001;&#x5B57;&#x9AD4;&#x7B49;&#x7B49;&#xFF09;&#xFF0C;&#x5728;&#x6E32;&#x67D3;&#x9019;&#x4E9B;&#x5B57;&#x578B;&#x7684;&#x6642;&#x5019;&#x6211;&#x5011;&#x6703;&#x9700;&#x8981;&#x505A;&#x8A08;&#x7B97;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x5C31;&#x628A;&#x76F8;&#x540C;&#x7A2E;&#x985E;&#x7684;&#x5B57;&#x5143;&#x4E1F;&#x5728;&#x4E00;&#x8D77;&#xFF0C;&#x53EA;&#x8981;&#x7B97;&#x4E00;&#x904D;&#x5C31;&#x597D;&#xFF0C;&#x63A5;&#x4E0B;&#x4F86;&#x78B0;&#x5230;&#x5C31;&#x62FF;&#x5FEB;&#x53D6;&#xFF0C;&#x800C;&#x4E0D;&#x540C;&#x7A2E;&#x985E;&#x7684;&#x5B57;&#x5143;&#x5247;&#x53EF;&#x4EE5;&#x5E73;&#x884C;&#x5316;&#x8A08;&#x7B97;&#x3002;</p>
<p>&#x4E00;&#x6A23;&#x4F5C;&#x8005;&#x4E5F;&#x5F97;&#x5230;&#x4E00;&#x500B;&#x7D50;&#x679C;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34728170-1e6a80ba-f594-11e7-92c3-234bcfb86232.png" alt><br>
&#x901F;&#x5EA6;&#x4E0A;&#x4E00;&#x6A23;&#x6709;&#x9032;&#x6B65;&#x3002;</p>
<hr>
<p>&#x96D6;&#x7136;&#x9019;&#x908A;&#x7814;&#x7A76;&#x7D50;&#x679C;&#x770B;&#x8D77;&#x4F86;&#x90FD;&#x5F88;&#x53B2;&#x5BB3;&#xFF0C;&#x4E0D;&#x904E;&#x4EE4;&#x4EBA;&#x8CEA;&#x7591;&#x7684;&#x662F;&#xFF0C;&#x4E5F;&#x8A31;&#x4ED6;&#x5BE6;&#x9A57;&#x74B0;&#x5883;&#x53EF;&#x4EE5;&#x9054;&#x5230;&#x9019;&#x6A23;&#x7684;&#x512A;&#x5316;&#x901F;&#x5EA6;&#xFF0C;&#x4F46; crash &#x7684;&#x6A5F;&#x6703;&#x591A;&#x9AD8;&#xFF1F;&#x5BE6;&#x9A57;&#x7684;&#x6642;&#x5019;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x5FFD;&#x7565;&#x6389;&#x90A3;&#x4E9B;&#x5D29;&#x6F70;&#x7684;&#x60C5;&#x6CC1;&#xFF0C;&#x4F46;&#x5982;&#x679C;&#x662F;&#x4E00;&#x500B;&#x5BE6;&#x969B;&#x7684;&#x7522;&#x54C1;&#xFF0C;&#x826F;&#x7387;&#x6C92;&#x6709; 99.99%&#x6211;&#x76F8;&#x4FE1;&#x5C31;&#x4E0D;&#x80FD;&#x7528;&#x3002;&#x5E73;&#x884C;&#x904B;&#x7B97;&#x5F88;&#x5BB9;&#x6613;&#x78B0;&#x5230;&#x932F;&#x8AA4;&#xFF0C;&#x7136;&#x800C;&#x6211;&#x5011;&#x4E26;&#x4E0D;&#x77E5;&#x9053;&#x9019;&#x4EFD;&#x7814;&#x7A76;&#x5BE6;&#x969B;&#x904B;&#x4F5C;&#x7684;&#x60C5;&#x6CC1;&#x3002;&#x7531;&#x65BC;&#x7DB2;&#x9801;&#x5BB9;&#x932F;&#x80FD;&#x529B;&#x5F88;&#x9AD8;&#xFF0C;&#x4F46;&#x76F8;&#x5C0D;&#x7684;&#x5728;&#x8655;&#x7406;&#x4E0A;&#x98A8;&#x96AA;&#x4E5F;&#x5C31;&#x8B8A;&#x9AD8;&#xFF0C;&#x4E00;&#x822C;&#x7684;&#x6642;&#x5019;&#x5C31;&#x53EF;&#x80FD;&#x6703;&#x767C;&#x751F;&#x5F88;&#x591A;&#x9810;&#x671F;&#x5916;&#x7684;&#x72C0;&#x6CC1;&#xFF0C;&#x5728;&#x5E73;&#x884C;&#x5316;&#x7684;&#x6642;&#x5019;&#x66F4;&#x52A0;&#x5371;&#x96AA;&#xFF0C;&#x5408;&#x683C;&#x7684;&#x7522;&#x54C1;&#x5FC5;&#x9808;&#x8981;&#x80FD;&#x5B8C;&#x5168;&#x638C;&#x63E1;&#x5404;&#x7A2E;&#x7A81;&#x767C;&#x72C0;&#x6CC1;&#x3002;</p>
<p>&#x5E73;&#x884C;&#x5316;&#x5F88;&#x5BB9;&#x6613;&#x51FA;&#x932F;&#xFF0C;&#x5C24;&#x5176;&#x662F;&#x5728;&#x8A18;&#x61B6;&#x9AD4;&#x7BA1;&#x7406;&#x7684;&#x90E8;&#x5206;&#xFF0C;&#x6240;&#x4EE5;&#x96D6;&#x7136;&#x6211;&#x5011;&#x5F88;&#x5BB9;&#x6613;&#x53EF;&#x4EE5;&#x63D0;&#x51FA;&#x4E00;&#x4E9B;&#x8B93;&#x6548;&#x80FD;&#x6539;&#x5584;&#x7684;&#x65B9;&#x6848;&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x6C92;&#x8FA6;&#x6CD5;&#x505A;&#x5230;&#x7D55;&#x5C0D;&#x7684;&#x7A69;&#x5B9A;&#xFF0C;&#x90A3;&#x9EBC;&#x5C31;&#x7121;&#x6CD5;&#x771F;&#x6B63;&#x8B8A;&#x6210;&#x4E00;&#x500B;&#x7522;&#x54C1;&#x3002;C++ &#x6C92;&#x8FA6;&#x6CD5;&#x8655;&#x7406;&#x5E73;&#x884C;&#x5316;&#x7684;&#x4E00;&#x4E9B;&#x56F0;&#x5883;&#xFF0C;&#x610F;&#x601D;&#x662F;&#x6211;&#x5011;&#x6C92;&#x8FA6;&#x6CD5;&#x9810;&#x671F;&#x54EA;&#x908A;&#x6703;&#x51FA;&#x932F;&#xFF0C;&#x53EA;&#x80FD;&#x78B0;&#x5230;&#x932F;&#x8AA4;&#x4E4B;&#x5F8C;&#x5BEB;&#x61C9;&#x5C0D;&#x65B9;&#x5F0F;&#xFF0C;&#x4F46;&#x9019;&#x6A23;&#x6703;&#x8017;&#x8CBB;&#x5927;&#x91CF;&#x4EBA;&#x529B;&#x7DAD;&#x8B77;&#x3001;&#x9664;&#x932F;&#xFF0C;&#x7522;&#x54C1;&#x672C;&#x8EAB;&#x4F9D;&#x820A;&#x5177;&#x6709;&#x4E0D;&#x78BA;&#x5B9A;&#x6027;&#xFF08;&#x842C;&#x4E00;&#x54EA;&#x500B;&#x932F;&#x8AA4;&#x6C92;&#x6709;&#x4E8B;&#x5148;&#x5075;&#x6E2C;&#x5230;&#xFF09;&#x3002;&#x6240;&#x4EE5;&#x5F8C;&#x4F86;&#x624D;&#x6709; Rust &#x8A9E;&#x8A00;&#x7684;&#x8A95;&#x751F;&#xFF0C;&#x900F;&#x904E;&#x8A9E;&#x8A00;&#x672C;&#x8EAB;&#x8A2D;&#x8A08;&#x7684;&#x7279;&#x6027;&#xFF0C;&#x907F;&#x514D;&#x5E73;&#x884C;&#x5316;&#x7684;&#x6642;&#x5019;&#x51FA;&#x932F;&#x3002;&#x6211;&#x9084;&#x4E0D;&#x662F;&#x5E73;&#x884C;&#x5316;&#x5C08;&#x5BB6;&#x6211;&#x4E5F;&#x4E0D;&#x80FD;&#x80AF;&#x5B9A;&#xFF0C;&#x4F46;&#x6211;&#x76F8;&#x4FE1;&#x5982;&#x679C;&#x628A; Rust &#x61C9;&#x7528;&#x5728;&#x9019;&#x4E9B;&#x7814;&#x7A76;&#x4E0A;&#x7684;&#x9EDE;&#x5B50;&#xFF0C;&#x61C9;&#x8A72;&#x6709;&#x6A5F;&#x6703;&#x771F;&#x7684;&#x8B93;&#x9019;&#x4E9B;&#x7814;&#x7A76;&#x6210;&#x679C;&#x8B8A;&#x6210;&#x7522;&#x54C1;&#x3002;&#x751A;&#x81F3;&#x6211;&#x5011;&#x9084;&#x53EF;&#x4EE5;&#x60F3;&#xFF0C;&#x9019;&#x4E9B;&#x6280;&#x8853;&#x662F;&#x5426;&#x80FD;&#x8F49;&#x79FB;&#x5230;&#x884C;&#x52D5;&#x88DD;&#x7F6E;&#x4E0A;&#xFF1F;</p>
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
                
