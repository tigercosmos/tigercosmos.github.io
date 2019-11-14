---
title: <論文> Servo 案例分析：平行化瀏覽器效能-能源的預測模型
date: 2018-01-19 17:49:09
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x4ECA;&#x65E5;&#x8AD6;&#x6587;&#xFF1A;<a href="http://ieeexplore.ieee.org/document/7839666/" target="_blank">Parallel Performance-Energy Predictive Modeling of Browsers: Case Study of Servo</a><br>
&#x767C;&#x8868;&#xFF1A; High Performance Computing (HiPC), 2016 IEEE 23rd International Conference<br>
&#x4F5C;&#x8005;&#xFF1A; Rohit Zambre(CA)&#x3001;Lars Bergstrom(Mozilla)&#x3001;Laleh Aghababaie Beni(CA)</p>
<blockquote>
<p>&#x672C;&#x6587;&#x5716;&#x7247;&#x4F86;&#x81EA;&#x539F;&#x59CB;&#x8AD6;&#x6587;</p>
</blockquote>
<hr>
<p><a href="https://ithelp.ithome.com.tw/users/20103745/ironman/1270" target="_blank">&#x672C;&#x7CFB;&#x5217;</a>&#x6709;&#x4ECB;&#x7D39;&#x904E; Servo&#xFF0C;&#x662F;&#x4E00;&#x500B;&#x5E73;&#x884C;&#x5316;&#x7684;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;&#x3002;&#x800C;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x7B2C;&#x4E8C;&#x4F5C;&#x8005;&#x662F;&#x4E4B;&#x524D; Servo &#x5718;&#x968A;&#x7684;&#x4E3B;&#x7BA1;&#x3002;</p>
<p>&#x5E73;&#x884C;&#x5316;&#x8655;&#x7406;&#x4E0D;&#x4E00;&#x5B9A;&#x6BCF;&#x6B21;&#x90FD;&#x6BD4;&#x8F03;&#x5FEB;&#x3002;&#x6709;&#x6642;&#x5019;&#xFF0C;&#x8207;&#x5176;&#x5206;&#x6563;&#x7D66;&#x56DB;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#x8DD1;&#xFF0C;&#x4E0D;&#x5982;&#x8B93;&#x55AE;&#x4E00;&#x57F7;&#x884C;&#x7DD2;&#x6642;&#x8108;&#x885D;&#x9AD8;&#xFF0C;&#x53EF;&#x80FD;&#x8655;&#x7406;&#x5F97;&#x66F4;&#x5FEB;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x8AAA;&#xFF0C;&#x4E0D;&#x662F;&#x6BCF;&#x6B21;&#x90FD;&#x63A1;&#x7528;&#x5E73;&#x884C;&#x5316;&#x5C31;&#x662F;&#x6700;&#x597D;&#x7684;&#x3002;&#x800C;&#x4ECA;&#x5929;&#x6211;&#x5011;&#x65E2;&#x7136;&#x60F3;&#x8981;&#x505A;&#x4E00;&#x500B;&#x66F4;&#x5FEB;&#x7684;&#x5F15;&#x64CE;&#xFF0C;&#x7576;&#x7136;&#x5C31;&#x4E0D;&#x80FD;&#x53CD;&#x800C;&#x88AB;&#x300C;&#x5E73;&#x884C;&#x5316;&#x300D;&#x800C;&#x626F;&#x5F8C;&#x817F;&#xFF0C;&#x6240;&#x4EE5;&#x9019;&#x7BC7;&#x5728;&#x7814;&#x7A76;&#x5982;&#x4F55;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x6A21;&#x578B;&#xFF0C;&#x8B93;&#x6211;&#x5011;&#x5728;&#x8655;&#x7406;&#x7DB2;&#x7AD9;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x80FD;&#x6C7A;&#x5B9A;&#x8981;&#x7528;&#x5E7E;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#xFF0C;&#x4F86;&#x9054;&#x5230;&#x6700;&#x4F73;&#x6548;&#x80FD;&#x3002;</p>
<hr>
<p>&#x4F8B;&#x5982;&#x6211;&#x5011;&#x770B;&#x9019;&#x5F35;&#x5716;&#xFF0C;&#x986F;&#x793A;&#x4E0D;&#x540C;&#x6A21;&#x578B;&#x4E0B;&#x7684;&#x7D50;&#x679C;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/35107469-f7c35d46-fcab-11e7-8751-0560ae75c7fb.png" alt><br>
&#x5176;&#x4E2D; <code>Servo</code> &#x6A19;&#x7C64;&#x662F; Servo &#x9810;&#x8A2D;&#x57F7;&#x884C;&#x60C5;&#x6CC1;&#xFF0C;&#x901A;&#x5E38;&#x6703;&#x662F;&#x56DB;&#x57F7;&#x884C;&#x7DD2;&#x3002;&#x800C; <code>Best</code> &#x662F;&#x8A66;&#x8A66;&#x770B; 1, 2, 4&#x57F7;&#x884C;&#x7DD2;&#xFF0C;&#x5F97;&#x5230;&#x6700;&#x597D;&#x6548;&#x80FD;&#x7684;&#x90A3;&#x6B21;&#x3002;&#x800C; <code>Our</code> model &#x5247;&#x662F;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x7528;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#x65B9;&#x5F0F;&#x63A8;&#x5F97;&#x51FA;&#x4F86;&#x8A72;&#x7528;&#x5E7E;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#x5F97;&#x5230;&#x7684;&#x7D50;&#x679C;&#x3002;</p>
<p>&#x53EF;&#x4EE5;&#x767C;&#x73FE;&#xFF0C;&#x5047;&#x8A2D;&#x9019;&#x500B;&#x7DB2;&#x7AD9;&#x5176;&#x5BE6;&#x7528; 1 &#x57F7;&#x884C;&#x7DD2;&#x6BD4;&#x8F03;&#x597D;&#xFF0C;&#x4F46; Servo &#x9810;&#x8A2D;&#x662F;&#x5168;&#x958B;&#xFF0C;&#x90A3;&#x53CD;&#x800C;&#x5C31;&#x6162;&#x4E86;&#x3002;&#x800C;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x9810;&#x6E2C;&#x7684;&#x6E96;&#x5EA6;&#x4E5F;&#x9084;&#x7B97;&#x4E0D;&#x932F;&#xFF0C;&#x770B;&#x5716;&#x5927;&#x81F4;&#x4E0A; <code>Our</code> &#x90FD;&#x6709;&#x543B;&#x5408; <code>Best</code>&#x3002;</p>
<hr>
<p>&#x65E2;&#x7136;&#x8AC7;&#x5230;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#xFF0C;&#x5C31;&#x8981;&#x9078;&#x4E00;&#x4E9B;&#x7279;&#x5FB5;&#x503C;&#xFF0C;&#x9019;&#x908A;&#x4F5C;&#x8005;&#x63A1;&#x7528; DOM tree &#x7684;&#x4E00;&#x4E9B;&#x6578;&#x64DA;&#x4F86;&#x7576;&#x7279;&#x5FB5;&#x3002;<br>
&#x9019;&#x5F35;&#x5716;&#x8996;&#x89BA;&#x5316;&#x4E00;&#x68F5; DOM tree &#x7684;&#x6A23;&#x5B50;&#xFF0C;&#x9806;&#x5E36;&#x4E00;&#x63D0;&#x7528;&#x7684;&#x5DE5;&#x5177;&#x662F; <a href="https://chikeichan.wordpress.com/2014/12/23/treeify-visualizing-dom-tree/" target="_blank">treeify</a>&#xFF0C;&#x5927;&#x5BB6;&#x53EF;&#x4EE5;&#x73A9;&#x73A9;&#x770B;<br>
<img src="https://user-images.githubusercontent.com/18013815/35138533-f388b216-fd29-11e7-9ee9-69a019544581.png" alt><br>
&#x6700;&#x5F8C;&#x4F5C;&#x8005;&#x6311;&#x51FA;&#x4EE5;&#x4E0B;&#x4E5D;&#x9EDE;&#x7576;&#x7279;&#x5FB5;&#x503C;&#xFF0C;&#x4E0D;&#x904E;&#x5F8C;&#x4F86;&#x6709;&#x5169;&#x500B;&#x767C;&#x73FE;&#x6C92;&#x5565;&#x7528;&#xFF1A;</p>
<ol>
<li>DOM tree &#x7684; node &#x7E3D;&#x6578;&#xFF08;DOM &#x5C3A;&#x5BF8;&#xFF09;</li>
<li>HTML tag &#x7528; attributes &#x7684;&#x6578;&#x91CF;</li>
<li>&#x7DB2;&#x9801;&#x7684; bytes &#x5927;&#x5C0F;</li>
<li>DOM tree &#x6709;&#x5E7E;&#x5C64;&#xFF08;&#x6DF1;&#x5EA6;&#xFF09;</li>
<li>DOM tree &#x7684;&#x8449;&#x5B50;&#x6578;&#x91CF;</li>
<li>&#x6BCF;&#x5C64;&#x6709;&#x591A;&#x5C11; node &#x7684;&#x5E73;&#x5747;&#x503C; (avg-tree-width)</li>
<li>&#x6BCF;&#x5C64;&#x6709;&#x591A;&#x5C11; node &#x7684;&#x6700;&#x5927;&#x503C; (max-tree-width)</li>
<li>max-tree-width &#x548C; average-tree-width &#x7684;&#x6BD4;&#x503C;(max-avg-width-ratio)</li>
<li>DOM-size &#x548C; tree-depth &#x7684;&#x6BD4;&#x503C;(avg-work-per-level)</li>
</ol>
<p>&#x9019;&#x908A;&#x53EF;&#x4EE5;&#x770B;&#x4E0B;&#x4E00;&#x4E9B;&#x7DB2;&#x7AD9; tree &#x6DF1;&#x5EA6;&#x548C;&#x5EE3;&#x5EA6;&#x7684;&#x95DC;&#x4FC2;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/35139483-4e5cc3ae-fd2e-11e7-81ff-1e52fb24c945.png" alt></p>
<p>&#x800C;&#x4E8B;&#x5BE6;&#x4E0A;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x731C;&#x6E2C;&#x8AAA;&#xFF0C;avg-tree-width &#x548C; avg-work-per-level &#x8D8A;&#x5927;&#xFF0C;&#x5E73;&#x884C;&#x5316;&#x6548;&#x679C;&#x8D8A;&#x597D;&#xFF0C;&#x5176;&#x5BE6;&#x6EFF;&#x597D;&#x60F3;&#x7684;&#xFF0C;&#x5C31;&#x662F;&#x4E8B;&#x60C5;&#x8D8A;&#x591A;&#x8D8A;&#x591A;&#x4EBA;&#x505A;&#x8D8A;&#x5BB9;&#x6613;&#xFF0C;&#x4F46;&#x4E8B;&#x60C5;&#x5F88;&#x5C11;&#x5206;&#x7D66;&#x5F88;&#x591A;&#x4EBA;&#x5C31;&#x662F;&#x96DE;&#x808B;&#x3002;&#x6240;&#x4EE5;&#x5F9E;&#x4E0A;&#x5716;&#xFF08;&#x5716;3&#xFF09;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x767C;&#x73FE; Facebook &#x666E;&#x904D;&#x5BEC;&#x5EA6;&#x5F88;&#x5C0F;&#xFF0C;avg-tree-width &#x548C; avg-work-per-level &#x4E5F;&#x5C31;&#x7576;&#x7136;&#x90FD;&#x6BD4;&#x8F03;&#x5C0F;&#xFF0C;&#x5BE6;&#x9A57;&#x4E5F;&#x8B49;&#x660E;&#x5728; Facebook &#x4E0A;&#x7528;&#x5E73;&#x884C;&#x5316;&#x6548;&#x679C;&#x4E0D;&#x4F73;&#x3002;</p>
<hr>
<p>&#x63A5;&#x8457;&#x4F86;&#x8AC7;&#x4E09;&#x7A2E; cost model&#xFF1A;</p>
<ul>
<li>&#x6548;&#x80FD;&#xFF1A;&#x5E73;&#x884C;&#x5316;&#x5E36;&#x4F86;&#x7684;&#x9032;&#x6B65;</li>
<li>&#x80FD;&#x6E90;&#xFF1A;&#x5E73;&#x884C;&#x5316;&#x5E36;&#x4F86;&#x7684;&#x80FD;&#x6E90;&#x6D88;&#x8017;</li>
<li>&#x6548;&#x80FD;&#x8207;&#x80FD;&#x6E90;&#xFF1A;&#x5169;&#x8005;&#x7686;&#x8003;&#x616E;</li>
</ul>
<p>&#x9019;&#x5F35;&#x5716;&#x986F;&#x793A;&#xFF0C;&#x8655;&#x7406; Styling &#x548C; Layout &#x82B1;&#x7684;&#x6BD4;&#x4F8B;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/35141500-0e5dbe9a-fd36-11e7-8146-b4c797491d82.png" alt><br>
&#x53EF;&#x4EE5;&#x767C;&#x73FE; Layout &#x771F;&#x7684;&#x5F88;&#x5C11;&#xFF0C;&#x4E5F;&#x56E0;&#x70BA;&#x5DE5;&#x4F5C;&#x91CF;&#x5C11;&#xFF0C;&#x5BE6;&#x9A57;&#x5F8C;&#x9019;&#x90E8;&#x5206;&#x62FF;&#x53BB;&#x5E73;&#x884C;&#x5316;&#x6548;&#x679C;&#x4E5F;&#x4E0D;&#x4F73;</p>
<p>&#x63A5;&#x8457;&#x5C31;&#x4F86;&#x505A;&#x5BE6;&#x9A57;&#x4E86;&#x3002;&#x9996;&#x5148;&#x662F;&#x6548;&#x80FD;&#x6A21;&#x578B;&#xFF0C;&#x5BE6;&#x9A57;&#x65B9;&#x6CD5;&#x5F88;&#x7C21;&#x55AE;&#xFF0C;&#x5C07;&#x6240;&#x6709;&#x8981;&#x6E2C;&#x8A66;&#x7684;&#x7DB2;&#x9801;&#xFF0C;&#x90FD;&#x5206;&#x5225;&#x7528; 1, 2, 4 &#x57F7;&#x884C;&#x7DD2;&#x90FD;&#x8DD1;&#x8DD1;&#x770B;&#xFF0C;&#x770B;&#x63A1;&#x7528;&#x5E7E;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#x8655;&#x7406;&#x901F;&#x5EA6;&#x6BD4;&#x8F03;&#x5FEB;&#xFF0C;&#x5C31;&#x6A19;&#x4E0A;&#x6700;&#x4F73;&#x7684;&#x90A3;&#x500B;&#x6578;&#x5B57;&#xFF0C;&#x7576;&#x505A;&#x4ED6;&#x5728;&#x6548;&#x80FD;&#x6A21;&#x578B;&#x4E0A;&#x7684;&#x6A19;&#x7C64;&#x3002;&#x63DB;&#x53E5;&#x8A71;&#x8AAA;&#xFF0C;&#x5C31;&#x662F;&#x770B;&#x90A3;&#x500B;&#x7DB2;&#x9801;&#x8A72;&#x7528;&#x5E7E;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#x6700;&#x597D;&#x3002;&#x5BE6;&#x9A57;&#x5F8C;&#x767C;&#x73FE;&#x6A19;&#x7C64; 1, 2 &#x548C; 4 &#x5206;&#x5225;&#x70BA; 299 (55.88%), 49 (9.15%) &#x548C; 187 (34.95%)&#x3002;</p>
<p>&#x80FD;&#x6E90;&#x6A21;&#x578B;&#x61C9;&#x8A72;&#x4E5F;&#x5F88;&#x6709;&#x8DA3;&#xFF0C;&#x525B;&#x525B;&#x662F;&#x8003;&#x616E;&#x8655;&#x7406;&#x901F;&#x5EA6;&#x8B8A;&#x5FEB;&#xFF0C;&#x6539;&#x6210;&#x6D88;&#x8017;&#x80FD;&#x6E90;&#x5C31;&#x597D;&#x3002;&#x4E0D;&#x904E;&#x4F5C;&#x8005;&#x6C92;&#x6709;&#x91DD;&#x5C0D;&#x9019;&#x90E8;&#x4EFD;&#x505A;&#x6E2C;&#x8A66;&#xFF0C;&#x53EA;&#x6709;&#x63D0;&#x51FA;&#x4F86;&#x800C;&#x5DF2;&#x3002;&#x4F46;&#x662F;&#x80FD;&#x6E90;&#x5C0D;&#x624B;&#x6A5F;&#x700F;&#x89BD;&#x5668;&#x61C9;&#x8A72;&#x5C31;&#x5F88;&#x91CD;&#x8981;&#x4E86;&#xFF0C;&#x4EE5;&#x5F8C;&#x53EF;&#x4EE5;&#x505A;&#x505A;&#x770B;&#x3002;</p>
<p>&#x63A5;&#x8457;&#x662F;&#x6548;&#x80FD;&#x80FD;&#x6E90;&#x6A21;&#x578B;&#xFF0C;&#x5169;&#x8457;&#x63A5;&#x8003;&#x616E;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x6211;&#x5011;&#x4EE5;&#x80FD;&#x6E90;&#x4E0D;&#x8D85;&#x904E;&#x67D0;&#x500B;&#x4E0A;&#x9650;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x6C7A;&#x5B9A;&#x6548;&#x80FD;&#x6700;&#x4F73;&#x7684;&#x90A3;&#x500B;&#x3002;&#x7576;&#x5168;&#x90E8;&#x4E0D;&#x7B26;&#x5408;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x5C31;&#x8A8D;&#x5B9A;&#x57F7;&#x884C;&#x7DD2;1&#x70BA;&#x6700;&#x4F73;&#x3002;&#x6700;&#x5F8C;&#x7D50;&#x8AD6;&#x662F;&#x6A19;&#x7C64; 1, 2 &#x548C; 4 &#x5206;&#x5225;&#x70BA; 317 (59.25%), 50 (9.34%) &#x548C; 168 (31.40%)&#x3002;</p>
<hr>
<p>&#x63A5;&#x8457;&#x4F86;&#x770B;&#x7279;&#x5FB5;&#x503C;&#x548C;&#x6548;&#x80FD;(p)&#x3001;&#x80FD;&#x6E90;(e)&#x7684;&#x95DC;&#x806F;&#xFF08;p2 &#x662F;&#x6548;&#x80FD;&#x6A21;&#x578B; 2 &#x57F7;&#x884C;&#x7DD2;&#x7684;&#x610F;&#x601D;&#xFF0C;&#x4EE5;&#x6B64;&#x985E;&#x63A8;&#xFF09;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/35143636-22395076-fd3d-11e7-990f-a8a2c09f6bc8.png" alt><br>
&#x7136;&#x5F8C;&#x767C;&#x73FE;  tree-depth &#x548C; max-avg-width-ratio &#x5E7E;&#x4E4E;&#x6C92;&#x5F71;&#x97FF;&#xFF0C;&#x76F8;&#x95DC;&#x4FC2;&#x6578;&#x4E0D;&#x8DB3; 0.1&#xFF0C;&#x6240;&#x4EE5;&#x5C31;&#x88AB;&#x6392;&#x9664;&#x6389;&#x3002;</p>
<p>&#x63A5;&#x8457;&#x7528; 90-10% &#x8CC7;&#x6599;-&#x6E2C;&#x8A66;&#x7684;&#x6BD4;&#x4F8B;&#xFF0C;&#x5C07;&#x6E2C;&#x8CC7;&#x5206;&#x6210;&#x5341;&#x7D44;&#xFF0C;&#x6BCF;&#x7D44;&#x7D04;55&#x500B;&#x6A23;&#x672C;&#xFF0C;&#x7136;&#x5F8C;&#x7528;&#x4E09;&#x7A2E;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#x7684;&#x6A21;&#x578B;&#x4F86;&#x6E2C;&#xFF1A;</p>
<ul>
<li>MNR&#xFF1A; &#x5728; 90-10% &#x8A13;&#x7DF4;&#x6E2C;&#x8A66;&#x7684;&#x4EA4;&#x53C9;&#x9A57;&#x8B49;&#x4E0B;&#xFF0C;&#x5E73;&#x5747;&#x548C;&#x6700;&#x5927;&#x7684;&#x6B63;&#x78BA;&#x7387;&#x70BA; 72.22% &#x548C; 87.27%&#x3002;</li>
<li>emsmeble&#xFF1A;AdaBoostM2&#xFF0B;&#x6C7A;&#x7B56;&#x6A39;&#x642D;&#x914D; surrogate splits&#xFF0C;&#x5E73;&#x5747;&#x548C;&#x6700;&#x5927;&#x7684;&#x6B63;&#x78BA;&#x7387;&#x70BA; 69.44% &#x548C; 85.45%&#x3002;</li>
<li>&#x795E;&#x7D93;&#x7DB2;&#x8DEF;&#xFF1A;80-10-10&#xFF05; &#x8A13;&#x7DF4;-&#x9A57;&#x8B49;-&#x6E2C;&#x8A66;&#x4E0B;&#xFF0C;&#x6E2C;&#x8CC7;&#x6B63;&#x78BA;&#x7387;&#x70BA; 77.8%&#x3002;</li>
</ul>
<p>&#x6B63;&#x78BA;&#x7387;&#x770B;&#x8D77;&#x4F86;&#x6709;&#x9EDE;&#x4F4E;&#x5566;&#xFF0C;&#x4E0D;&#x904E;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x672C;&#x4F86;&#x5C31;&#x4E0D;&#x662F;&#x4E00;&#x7BC7;&#x300C;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#x300D;&#x7684;&#x8AD6;&#x6587;&#xFF0C;&#x6240;&#x4EE5;&#x60C5;&#x6709;&#x53EF;&#x539F;&#x3002;</p>
<hr>
<p>&#x4E0D;&#x904E;&#x5373;&#x4F7F;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#x7684;&#x6548;&#x679C;&#x6C92;&#x6709;&#x5230;&#x975E;&#x5E38;&#x597D;&#xFF0C;&#x4F46;&#x662F;&#x62FF; MNR &#x7684;&#x7D50;&#x679C;&#x4F86;&#x548C;&#x539F;&#x672C;&#x7684; Servo &#x6BD4;&#x8D77;&#x4F86;&#xFF0C;&#x6700;&#x591A;&#x53EF;&#x4EE5;&#x7701;&#x5230; 94% &#x7684;&#x6548;&#x80FD;&#xFF0C;&#x4F8B;&#x5982; &quot;indeed.com&quot; &#x539F;&#x672C; Servo &#x9810;&#x8A2D;&#x7528; 4 &#x57F7;&#x884C;&#x7DD2;&#x8981;&#x8DD1; 45ms&#xFF0C;&#x4F46;&#x5176;&#x5BE6;&#x7528; 1 &#x57F7;&#x884C;&#x7DD2;&#x53EA;&#x8981; 2.48 ms&#xFF0C;&#x751A;&#x81F3;&#x6D88;&#x8017;&#x7684;&#x80FD;&#x91CF;&#x4E5F;&#x5C11;&#x4E86;&#x4E00;&#x534A;&#x3002;</p>
<p>&#x7E3D;&#x4E4B;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x6700;&#x6709;&#x8DA3;&#x7684;&#x5730;&#x65B9;&#x5C31;&#x662F;&#xFF0C;&#x7528;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#x4F86;&#x5224;&#x65B7;&#x8AAA;&#xFF0C;&#x73FE;&#x5728;&#x700F;&#x89BD;&#x7684;&#x9019;&#x500B;&#x7DB2;&#x7AD9;&#x8A72;&#x63A1;&#x7528;&#x5E7E;&#x500B;&#x57F7;&#x884C;&#x7DD2;&#x4F86;&#x8655;&#x7406;&#x6BD4;&#x8F03;&#x597D;&#x3002;&#x770B;&#x5B8C;&#x9019;&#x7BC7;&#x6709;&#x7D66;&#x6211;&#x4E00;&#x9EDE;&#x555F;&#x767C;&#xFF0C;&#x5982;&#x679C;&#x5C07;&#x985E;&#x4F3C;&#x7684;&#x6982;&#x5FF5;&#x5957;&#x5165;&#x5FEB;&#x53D6;&#x7684;&#x8655;&#x7406;&#x4E0A;&#x5462;&#xFF1F;</p>
<blockquote>
<p>&#x5EF6;&#x4F38;&#x95B1;&#x8B80;&#xFF1A;<a href="https://blog.servo.org/2015/09/11/timing-energy/" target="_blank">Fine-grained timing and energy profiling in Servo</a></p>
</blockquote>
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
                
