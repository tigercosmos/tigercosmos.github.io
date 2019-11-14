---
title: <論文> 網頁瀏覽器在異質運算多核心處理器平台上電量管理的工作量描述
date: 2018-04-10 22:56:34
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x6700;&#x8FD1;&#x53C8;&#x770B;&#x4E86;&#x4E00;&#x7BC7;&#x8AD6;&#x6587;&#xFF0C;&#x89BA;&#x5F97;&#x5BEB;&#x5F97;&#x5F88;&#x7CBE;&#x5F69;&#x6240;&#x4EE5;&#x6C7A;&#x5B9A;&#x4F86;&#x5206;&#x4EAB;&#x4E00;&#x4E0B;</p>
<ul>
<li>&#x539F;&#x6587;&#x6A19;&#x984C;&#xFF1A;Web browser workload characterization for power management on HMP platforms</li>
<li>&#x4F5C;&#x8005;&#xFF1A; Nadja Peters(1), Sangyoung Park(1), Samarjit Chakraborty(1), Benedikt Meurer(2), Hannes Payer(2), Daniel Clifford(2). (1)Technical University of Munich, (2)Google Inc</li>
<li>&#x767C;&#x8868;&#xFF1A; Hardware/Software Codesign and System Synthesis (CODES+ISSS), 2016 International Conference on</li>
</ul>
<hr>
<h2>&#x7C21;&#x4ECB;</h2>
<p>&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x5728;&#x7814;&#x7A76; Google &#x7684; Chrome &#x700F;&#x89BD;&#x5668;&#x5728;&#x7570;&#x8CEA;&#x904B;&#x7B97;&#x591A;&#x6838;&#x5FC3;&#x8655;&#x7406;&#x5668;&#xFF08;heterogeneous multi-processing, HMP&#xFF09;&#xFF0C;&#x6216;&#x662F;&#x6240;&#x8B02; <a href="https://zh.wikipedia.org/wiki/Big.LITTLE" target="_blank">big.LITTLE</a> &#x67B6;&#x69CB;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x8655;&#x7406;&#x5668;&#x4F7F;&#x7528;&#x65B9;&#x5F0F;&#x5C0D;&#x65BC;&#x700F;&#x89BD;&#x5668;&#x7684;&#x6548;&#x80FD;&#x4EE5;&#x53CA;&#x8017;&#x96FB;&#x6709;&#x600E;&#x6A23;&#x7684;&#x5F71;&#x97FF;&#x3002;</p>
<p>big.LITTLE &#x662F; ARM &#x63D0;&#x51FA;&#x7684;&#x8655;&#x7406;&#x5668;&#x67B6;&#x69CB;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x7531;&#x5E7E;&#x500B;&#x300C;&#x9AD8;&#x6548;&#x80FD;&#x300D;&#x8655;&#x7406;&#x5668;&#x642D;&#x914D;&#x5E7E;&#x500B;&#x300C;&#x4F4E;&#x529F;&#x8017;&#x300D;&#x8655;&#x7406;&#x5668;&#xFF0C;&#x6240;&#x7D44;&#x6210;&#x7684;&#x8655;&#x7406;&#x5668;&#x53E2;&#x96C6;&#x3002;&#x81F3;&#x65BC;&#x6240;&#x8B02;&#x7570;&#x8CEA;&#x904B;&#x7B97;&#x591A;&#x6838;&#x5FC3;&#x8655;&#x7406;&#x5668;&#xFF0C;&#x7BC0;&#x9304;&#x81EA; Wiki&#xFF1A;</p>
<blockquote>
<p>&#x7570;&#x8CEA;&#x591A;&#x8655;&#x7406;&#xFF08;heterogeneous multi-processing&#xFF0C;HMP&#xFF09;&#x662F;big.LITTLE&#x7D44;&#x614B;&#x4E2D;&#x6700;&#x9748;&#x6D3B;&#x4E5F;&#x662F;&#x6548;&#x80FD;&#x6700;&#x5F37;&#x52C1;&#x7684;&#x4F7F;&#x7528;&#x6A21;&#x5F0F;&#xFF0C;&#x5728;&#x9019;&#x7A2E;&#x7D44;&#x614B;&#x4E2D;&#xFF0C;&#x540C;&#x4E00;&#x6642;&#x9593;&#x9EDE;&#x4E0A;&#x6240;&#x6709;&#x7684;&#x7269;&#x7406;CPU&#x6838;&#x5FC3;&#x90FD;&#x662F;&#x53EF;&#x7528;&#x7684;&#x4E26;&#x4E14;&#x53EF;&#x4EE5;&#x540C;&#x6642;&#x5168;&#x90E8;&#x958B;&#x555F;&#x4F7F;&#x7528;&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x5C07;&#x9AD8;&#x6548;&#x80FD;CPU&#x6838;&#x5FC3;&#x5168;&#x6578;&#x95DC;&#x9589;&#x800C;&#x53EA;&#x4F7F;&#x7528;&#x4F4E;&#x529F;&#x8017;CPU&#x6838;&#x5FC3;&#x3002;&#x9AD8;&#x512A;&#x5148;&#x7D1A;&#x6216;&#x8005;&#x5C0D;&#x904B;&#x7B97;&#x901F;&#x5EA6;&#x5403;&#x91CD;&#x7684;&#x57F7;&#x884C;&#x7DD2;&#x53EF;&#x4EE5;&#x88AB;&#x5206;&#x6D3E;&#x81F3;&#x9AD8;&#x6548;&#x80FD;CPU&#x6838;&#x5FC3;&#x4E0A;&#xFF0C;&#x800C;&#x4F4E;&#x512A;&#x5148;&#x7D1A;&#x6216;&#x5C0D;&#x904B;&#x7B97;&#x901F;&#x5EA6;&#x8981;&#x6C42;&#x4E0D;&#x9AD8;&#x7684;&#x57F7;&#x884C;&#x7DD2;&#xFF08;&#x5982;&#x80CC;&#x666F;&#x4EFB;&#x52D9;&#xFF09;&#xFF0C;&#x5247;&#x662F;&#x7531;&#x4F4E;&#x529F;&#x8017;CPU&#x6838;&#x5FC3;&#x8CA0;&#x8CAC;&#x5B8C;&#x6210;&#x3002;</p>
</blockquote>
<p>&#x800C;&#x4F5C;&#x8005;&#x767C;&#x73FE;&#x8655;&#x7406;&#x5668;&#x9810;&#x8A2D;&#x7684; schedulers &#x5C0D;&#x65BC; CPU &#x7684;&#x63A7;&#x5236;&#x904E;&#x65BC;&#x7C21;&#x55AE;&#xFF0C;&#x6240;&#x4EE5;&#x63D0;&#x51FA;&#x4E09;&#x7A2E;&#x69CB;&#x60F3;&#x4E26;&#x52A0;&#x4EE5;&#x5BE6;&#x9A57;&#x3002;</p>
<ul>
<li>&#x63A7;&#x5236;&#x8655;&#x7406;&#x5668;&#x57F7;&#x884C;&#x6578;&#x91CF;&#xFF08;Constraints for Core Allocation&#xFF09;</li>
<li>&#x96FB;&#x6E90;&#x9580;&#x63A7;&#x529F;&#x8017;&#x8A2D;&#x8A08;&#xFF08;Power Gating&#xFF09;</li>
<li>&#x52D5;&#x614B;&#x8ABF;&#x6574;&#x96FB;&#x58D3;&#x548C;&#x983B;&#x7387;&#xFF08;dynamic voltage and frequency scaling, DVFS&#xFF09;</li>
</ul>
<p>&#x4EE5;&#x4E0A;&#x5E7E;&#x500B;&#x5C08;&#x6709;&#x540D;&#x8A5E;&#x5F8C;&#x9762;&#x9084;&#x6703;&#x7528;&#x5230;&#x3002;</p>
<p>&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5982;&#x679C;&#x60F3;&#x8981;&#x6700;&#x9AD8;&#x6548;&#x80FD;&#x7684;&#x8A71;&#xFF0C;&#x628A; CPU &#x5F9E;&#x7D1A;&#x7684;&#x6240;&#x6709;&#x6838;&#x5FC3;&#x90FD;&#x5168;&#x958B;&#x6548;&#x80FD;&#x4E00;&#x5B9A;&#x6700;&#x597D;&#xFF0C;&#x4F46;&#x5982;&#x679C;&#x60F3;&#x8981;&#x9054;&#x5230;&#x6548;&#x80FD;&#x8207;&#x529F;&#x8017;&#x7684;&#x6700;&#x4F73;&#x5E73;&#x8861;&#xFF0C;&#x9019;&#x4E09;&#x7A2E;&#x65B9;&#x6CD5;&#x90FD;&#x503C;&#x5F97;&#x8003;&#x616E;&#xFF0C;&#x56E0;&#x70BA;&#x90FD;&#x80FD;&#x505A;&#x5230;&#x964D;&#x4F4E;&#x6548;&#x80FD;&#xFF0C;&#x537B;&#x7701;&#x4E0B;&#x529F;&#x8017;&#x3002;&#x90A3;&#x63A5;&#x8457;&#x5C31;&#x662F;&#x770B;&#xFF0C;&#x6211;&#x5011;&#x8981;&#x600E;&#x9EBC;&#x6A23;&#x53D6;&#x6368;&#xFF0C;&#x4E5F;&#x8A31;&#x662F;&#x770B;&#x300C;&#x7BC0;&#x7701;&#x529F;&#x8017;&#x7684;&#x6BD4;&#x4F8B;&#x300D;&#x8207;&#x300C;&#x8B8A;&#x5DEE;&#x6548;&#x80FD;&#x7684;&#x6BD4;&#x4F8B;&#x300D;&#x7684;&#x6BD4;&#x503C;&#xFF0C;&#x54EA;&#x4E00;&#x500B;&#x65B9;&#x6CD5;&#x8B93;&#x6BD4;&#x503C;&#x6700;&#x9AD8;&#xFF0C;&#x610F;&#x5473;&#x8457;&#x7701;&#x6BD4;&#x8F03;&#x591A;&#x96FB;&#xFF0C;&#x537B;&#x72A7;&#x7272;&#x6BD4;&#x8F03;&#x5C11;&#x6548;&#x80FD;&#x3002;&#x4F46;&#x5982;&#x4F55;&#x6289;&#x64C7;&#x6C92;&#x6709;&#x7D55;&#x5C0D;&#xFF0C;&#x91CD;&#x9EDE;&#x662F;&#x6211;&#x5011;&#x6CE8;&#x610F;&#x5230;&#x5728;&#x8003;&#x616E;&#x6548;&#x80FD;&#x8207;&#x529F;&#x8017;&#x5E73;&#x8861;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x8655;&#x7406;&#x5668;&#x672C;&#x8EAB;&#x7684;&#x63A7;&#x5236;&#x9084;&#x6709;&#x9032;&#x6B65;&#x7A7A;&#x9593;&#x3002;</p>
<h2>&#x700F;&#x89BD;&#x5668;&#x67B6;&#x69CB;</h2>
<p>&#x5728;&#x672C;&#x7CFB;&#x5217;&#x8A0E;&#x8AD6;&#x700F;&#x89BD;&#x5668;&#x67B6;&#x69CB;&#x5DF2;&#x7D93;&#x662F;&#x8001;&#x751F;&#x5E38;&#x8AC7;&#x4E86;<br>
<img src="https://user-images.githubusercontent.com/18013815/38518906-d3f81bf4-3c70-11e8-8824-15da5b480f5b.png" alt="&#x700F;&#x89BD;&#x5668;&#x67B6;&#x69CB;"><br>
&#x4F5C;&#x8005;&#x5728;&#x9019;&#x908A;&#x63D0;&#x5230;&#x8AAA;&#xFF0C;&#x958B;&#x555F;&#x7DB2;&#x7AD9;&#x7684;&#x904E;&#x7A0B;&#x4E2D;&#xFF0C;70&#xFF05;&#x6D88;&#x8017;&#x7684;&#x529F;&#x4F86;&#x81EA;&#x65BC;&#x7DB2;&#x9801;&#x6E32;&#x67D3;&#xFF0C;&#x5176;&#x4E2D;&#x53C8;&#x6709;60&#xFF05;&#x4F86;&#x81EA;&#x65BC; JS &#x904B;&#x7B97;&#x7684;&#x6D88;&#x8017;&#x3002;</p>
<h2>&#x5BE6;&#x9A57;&#x5668;&#x6750;</h2>
<p>Samsung Galaxy S5 &#x624B;&#x6A5F;&#x7684; Odroid-XU3 board&#xFF0C;&#x7279;&#x8272;&#x662F;&#x6709; Exynos5422 &#x7CFB;&#x7D71;&#x55AE;&#x6676;&#x7247;&#xFF08;SoC&#xFF09;&#x3002;&#x5176;&#x4E2D;&#x7684;&#x7570;&#x8CEA;&#x8655;&#x7406;&#x5668;&#x6676;&#x7247; (heterogeneous multiprocessor system-on-chip) &#x4E5F;&#x662F;&#x7167;&#x8457; ARM &#x7684; big.LITTLE &#x67B6;&#x69CB;&#x8A2D;&#x8A08;&#x3002;&#x6240;&#x4EE5;&#x53E2;&#x96C6;&#x5171;&#x6709; 4 &#x500B;&#x529F;&#x8017;&#x512A;&#x5316; Cortex-A7 &#x8655;&#x7406;&#x5668;&#x548C; 4 &#x500B;&#x6548;&#x80FD;&#x512A;&#x5316;&#x7684; Cortex-A15 &#x8655;&#x7406;&#x5668;&#x3002;</p>
<p>&#x700F;&#x89BD;&#x5668;&#x5247;&#x662F;&#x7528; Chrome &#x7684;&#x7CBE;&#x7C21;&#x7248;&#xFF0C;Content Shell&#x3002;</p>
<h2>HMP &#x5E73;&#x53F0;&#x96FB;&#x6E90;&#x63A7;&#x5236;</h2>
<p><img src="https://user-images.githubusercontent.com/18013815/38518804-8f3d27c0-3c70-11e8-9b34-b76855d4cd5e.png" alt="A7-A15&#x67B6;&#x69CB;"><br>
Android &#x672C;&#x8EAB;&#x662F;&#x57FA;&#x65BC; Linux &#x6838;&#x5FC3;&#xFF0C;&#x5176;&#x4E2D;&#x63A7;&#x5236; CPU &#x7684;&#x90E8;&#x5206;&#x6709;&#x4E09;&#x500B;&#xFF0C;(1) the scheduler (2) the frequency governor (3) the wakelock mechanism&#x3002;scheduler &#x662F;&#x7528;&#x4F86;&#x5206;&#x914D;&#x5DE5;&#x4F5C;&#x7D66;&#x6838;&#x5FC3;&#xFF0C;governor &#x8CA0;&#x8CAC;&#x63A7;&#x5236;&#x983B;&#x7387;&#xFF0C;&#x901A;&#x5E38; linux &#x90FD;&#x662F;&#x63A1;&#x7528; ondemand &#x548C; interactive&#xFF0C;&#x5176;&#x4E2D; interactive governor &#x662F;&#x7279;&#x5730;&#x8A2D;&#x8A08;&#x7D66;&#x884C;&#x52D5;&#x88DD;&#x7F6E;&#x7684;&#x3002;&#x800C; wakelock &#x662F; Android &#x7279;&#x6709;&#x7684;&#xFF0C;&#x8CA0;&#x8CAC;&#x8B93;&#x57F7;&#x884C;&#x4E2D;&#x7684;&#x7A0B;&#x5F0F;&#x4E00;&#x76F4;&#x8655;&#x65BC;&#x300C;&#x9192;&#x8457;&#x300D;&#x72C0;&#x614B;&#x3002;</p>
<p><img src="https://user-images.githubusercontent.com/18013815/38519534-b4aeee56-3c72-11e8-94ac-6d0e23fb6b4e.png" alt="ebay &#x7D50;&#x679C;&#xFF0C;&#x63A1;&#x7528;&#x539F;&#x8A2D;&#x5B9A;"><br>
&#x5716;&#x56DB;&#x662F;&#x63A1;&#x7528; Android &#x539F;&#x751F;&#x8A2D;&#x5B9A;&#xFF0C;&#x53BB;&#x700F;&#x89BD; ebay &#x7684;&#x7D50;&#x679C;&#x3002;&#x6211;&#x5011;&#x770B;&#x5230;&#x5E7E;&#x500B;&#x554F;&#x984C;&#xFF1A;</p>
<ol>
<li>&#x524D;&#x5169;&#x79D2; A15 &#x90FD;&#x6C92;&#x88AB;&#x4F7F;&#x7528;&#xFF0C;&#x983B;&#x7387;&#x537B;&#x885D;&#x5230;&#x6700;&#x9AD8;</li>
<li>&#x5F8C;&#x4F86; CPU &#x4F7F;&#x7528;&#x7387;&#x4F4E;&#x65BC; 100%&#xFF0C;&#x4EE3;&#x8868;&#x55AE;&#x4E00;&#x6838;&#x5FC3;&#x5C31;&#x5920;&#x4E86;&#xFF0C;&#x4F46; CPU &#x4ECD;&#x7DAD;&#x6301;&#x9AD8;&#x983B;&#x7387;</li>
<li>&#x5C31;&#x7B97; A15 &#x6C92;&#x88AB;&#x4F7F;&#x7528;&#xFF0C;&#x4F9D;&#x820A;&#x7DAD;&#x6301; 50% &#x7684;&#x983B;&#x7387;</li>
</ol>
<p>&#x5F9E;&#x4EE5;&#x4E0A;&#x5E7E;&#x9EDE;&#xFF0C;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x6539;&#x9032;&#x5F88;&#x591A;&#x5730;&#x65B9;&#xFF0C;&#x4F8B;&#x5982;&#x7B2C;&#x4E00;&#x9EDE;&#x53EF;&#x4EE5;&#x900F;&#x904E;&#x52D5;&#x614B;&#x96FB;&#x58D3;&#x6642;&#x8108;&#xFF08;DVFS&#xFF09;&#x6539;&#x5584;&#xFF0C;&#x7B2C;&#x4E8C;&#x9EDE;&#x53EF;&#x4EE5;&#x900F;&#x904E;&#x9650;&#x5236;&#x6838;&#x5FC3;&#x4F86;&#x8FA6;&#x5230;&#xFF0C;&#x7B2C;&#x4E09;&#x9EDE;&#x53EF;&#x4EE5;&#x7528;&#x96FB;&#x6E90;&#x9580;&#x63A7;&#x529F;&#x8017;&#x8A2D;&#x8A08;&#x4F86;&#x6539;&#x5584;&#x3002;</p>
<h2>&#x6AA2;&#x6E2C;&#x6A5F;&#x5236;</h2>
<p><img src="https://user-images.githubusercontent.com/18013815/38532455-82643430-3ca7-11e8-808c-2ccf1ab3e3a6.png" alt="Exynos5422-based measurement setup"><br>
&#x5728; CPU &#x524D;&#x9762;&#x6709; Shunt &#x662F;&#x96FB;&#x963B; &#x548C; INA231 &#x96FB;&#x58D3;&#x96FB;&#x6D41;&#x611F;&#x6E2C;&#x5668;&#x3002;<br>
<img src="https://user-images.githubusercontent.com/18013815/38532452-81ecbcfc-3ca7-11e8-9a70-e078ade49c11.png" alt="Software setup for data acquirement"><br>
&#x85C9;&#x7531;&#x529F;&#x8017;&#x7D00;&#x9304;&#x3001;&#x5DE5;&#x4F5C;&#x6392;&#x7A0B;&#x7D00;&#x9304;&#x3001;&#x700F;&#x89BD;&#x5668;&#x5806;&#x758A;&#x7D00;&#x9304;&#xFF0C;&#x53EF;&#x4EE5;&#x5206;&#x6790;&#x700F;&#x89BD;&#x7DB2;&#x7AD9;&#x7684;&#x529F;&#x8017;</p>
<h2>&#x700F;&#x89BD;&#x5668;&#x57F7;&#x884C;&#x7DD2;</h2>
<p><img src="https://user-images.githubusercontent.com/18013815/38533062-271ba22c-3caa-11e8-8bfc-205eb804df4d.png" alt="Relative CPU time of web browser threads for representative websites per A15 and A7 cluster"><br>
&#x5F9E;&#x5716; 7 &#x548C; 8 &#x53EF;&#x4EE5;&#x767C;&#x73FE;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x5728;&#x6E32;&#x67D3;&#x7684;&#x6642;&#x5019;&#xFF0C;CrRendererMain&#xFF08;&#x6E32;&#x67D3;&#x4E3B;&#x7A0B;&#x5F0F;&#xFF09; &#x548C; CompositorTileW&#xFF08;&#x8655;&#x7406;&#x5408;&#x6210;&#xFF09;&#x4F54;&#x4E86;&#x5927;&#x90E8;&#x5206;&#x7684;&#x6D88;&#x8017;&#xFF0C;&#x800C;&#x53C8;&#x9019;&#x5169;&#x500B;&#x7A0B;&#x5E8F;&#x53EA;&#x8981;&#x53C8;&#x662F;&#x4EE5; A15 &#x4F86;&#x8655;&#x7406;&#xFF0C;&#x5E7E;&#x4E4E;&#x662F; 80-90% &#x7684;&#x5DE5;&#x4F5C;&#x91CF;&#x3002;</p>
<p><img src="https://user-images.githubusercontent.com/18013815/38535603-d8dec65e-3cb6-11e8-8ef0-4a435c5e878d.png" alt="Figure 9: Relative energy distribution of the web page com- ponents HTML, CSS and JavaScript."><br>
<img src="https://user-images.githubusercontent.com/18013815/38535720-7aa49d7e-3cb7-11e8-8717-d2692c7bca58.png" alt="Figure 10: Relative time distribution of V8-related function calls by category."><br>
&#x5F9E;&#x5716; 9 &#x548C; 10 &#xFF0C;V8 &#x82B1;&#x4E86; 40%&#x5728;&#x89E3;&#x6790;&#xFF0C;50% &#x5728;&#x57F7;&#x884C;&#x3002;&#x53C8;&#x767C;&#x73FE; V8 &#x5728;&#x4E3B;&#x6E32;&#x67D3;&#x57F7;&#x884C;&#x7DD2;&#x82B1;&#x4E86; 83-96%&#xFF0C;&#x4F46;&#x53EA;&#x6709; 1-13% &#x7684;&#x57F7;&#x884C;&#x7DD2;&#x6642;&#x9593;&#x662F;&#x7528;&#x5728; ScriptStreamerThread&#xFF08;&#x89E3;&#x6790;JS&#xFF09;&#x3002;&#x610F;&#x5473;&#x8457;&#x4E5F;&#x8A31;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x628A;&#x89E3;&#x6790;&#x7684;&#x90E8;&#x4EFD;&#x4EA4;&#x7D66; A7 &#x8655;&#x7406;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x4E0D;&#x600E;&#x82B1;&#x8CC7;&#x6E90;&#x7684;&#x90E8;&#x4EFD;&#x4EA4;&#x7D66;&#x529F;&#x8017;&#x512A;&#x5316;&#x7684;&#x8655;&#x7406;&#x5668;&#x8CA0;&#x8CAC;&#xFF0C;&#x9019;&#x6A23;&#x6703;&#x66F4;&#x7701;&#x529F;&#x8017;&#xFF01;</p>
<h2>&#x5BE6;&#x9A57;&#x56C9;&#xFF01;</h2>
<h3>&#x9650;&#x5236;&#x6548;&#x80FD;&#x5206;&#x6790;&#xFF08;Power-Performance Trade-off Analysis&#xFF09;</h3>
<p>&#x76F4;&#x63A5;&#x9650;&#x5236; A15 &#x53EF;&#x4EE5;&#x7528;&#x7684;&#x6700;&#x9AD8;&#x6642;&#x8108;<br>
<img src="https://user-images.githubusercontent.com/18013815/38539109-4ad61548-3cc9-11e8-82a7-9f81e7ae3426.png" alt="figure 11 12"><br>
eBay &#x7684;&#x4F8B;&#x5B50;&#x4E2D;&#xFF0C;&#x5C07;&#x6700;&#x9AD8;&#x6642;&#x8108;&#x9650;&#x5236;&#x5728; 1.2GHz&#xFF0C;&#x6D88;&#x8017;&#x7684;&#x529F;&#x6E1B;&#x5C11; 34.6% &#xFF0C;&#x4F46;&#x8655;&#x7406;&#x6642;&#x9593;&#x53EA;&#x589E;&#x52A0; 16.7% (0.6 s)<br>
&#x5176;&#x4ED6;&#x7DB2;&#x7AD9;&#x4E5F;&#x90FD;&#x5DEE;&#x4E0D;&#x591A;&#xFF0C;&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F;&#x6548;&#x80FD;&#x63DB;&#x53D6;&#x6642;&#x9593;&#x3002;&#x9019;&#x500B;&#x65B9;&#x6CD5;&#x8207;&#x662F;&#x5426;&#x70BA;&#x7570;&#x8CEA;&#x8655;&#x7406;&#x5668;&#x7121;&#x95DC;&#xFF0C;&#x5C31;&#x7B97;&#x662F;&#x55AE;&#x6838;&#x5FC3;&#x4E5F;&#x6703;&#x662F;&#x4E00;&#x6A23;&#x7684;&#x7D50;&#x679C;&#xFF0C;&#x6EFF;&#x76F4;&#x89C0;&#x7684;&#x7D50;&#x679C;&#x3002;</p>
<h3>&#x9650;&#x5236;&#x4F7F;&#x7528;&#x6838;&#x5FC3;&#xFF08;Constraints for Core Allocation&#xFF09;</h3>
<p>&#x5728;&#x525B;&#x525B;&#x8A0E;&#x8AD6;&#x700F;&#x89BD;&#x5668;&#x57F7;&#x884C;&#x7DD2;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x6211;&#x5011;&#x77E5;&#x9053;&#x628A;&#x5DE5;&#x4F5C;&#x5206;&#x4E00;&#x4E9B;&#x7D66;&#x6548;&#x80FD;&#x5C0E;&#x5411;&#x7684;&#x8655;&#x7406;&#x5668;&#x662F;&#x6BD4;&#x8F03;&#x6709;&#x6548;&#x7387;&#x7684;&#x3002;<br>
&#x6E2C;&#x8A66;&#x4E09;&#x7A2E;&#x6A21;&#x5F0F;&#xFF0C;&#x9650;&#x5236;&#x53EF;&#x4EE5;&#x7528;&#x7684;&#x8655;&#x7406;&#x5668;&#x6838;&#x5FC3;&#x6578;&#xFF1A;</p>
<ol>
<li>4 &#x500B; A7 + 4 &#x500B; A15</li>
<li>4 &#x500B; A7 + 1 &#x500B; A15</li>
<li>4 &#x500B; A7<br>
<img src="https://user-images.githubusercontent.com/18013815/38562563-75b2ee28-3d0d-11e8-872f-3a6ed9f2bc53.png" alt="figure13"><br>
&#x5728; eBay &#x7684;&#x4F8B;&#x5B50;&#x4E2D;&#xFF0C;&#x7B2C;&#x4E00;&#x7A2E;&#xFF08;&#x5168;&#x958B;&#xFF09;&#x8DDF;&#x7B2C;&#x4E8C;&#x7A2E;&#xFF08;&#x534A;&#x958B;&#xFF09;&#x76F8;&#x6BD4;&#xFF0C;&#x534A;&#x958B;&#x80FD;&#x91CF;&#x7701;&#x4E86; 13%&#xFF0C;&#x57F7;&#x884C;&#x6642;&#x9593;&#x53EA;&#x591A;&#x4E86; 5%&#x3002;&#x9019;&#x6A23;&#x7684;&#x4EA4;&#x63DB;&#x5176;&#x5BE6;&#x6EFF;&#x503C;&#x5F97;&#x7684;&#xFF01;<br>
<img src="https://user-images.githubusercontent.com/18013815/38562751-dc7dcccc-3d0d-11e8-9d2d-c71a9c7d7d30.png" alt="figure14"><br>
&#x4F46;&#x5728; Wikipedia &#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x7B2C;&#x4E00;&#x7A2E;&#x548C;&#x7B2C;&#x4E8C;&#x7A2E;&#x6548;&#x80FD;&#x548C;&#x529F;&#x8017;&#x5247;&#x5E7E;&#x4E4E;&#x6C92;&#x6539;&#x8B8A;&#x3002;&#x4F46;&#x9019;&#x4E5F;&#x8AAA;&#x660E;&#x4E86;&#xFF0C;&#x591A;&#x6578;&#x6642;&#x5019;&#x6211;&#x5011;&#x5176;&#x5BE6;&#x53EF;&#x4EE5;&#x9078;&#x64C7;&#x534A;&#x958B;&#x5C31;&#x597D;&#xFF0C;&#x6700;&#x58DE;&#x7D50;&#x679C;&#x5C31;&#x662F;&#x6C92;&#x8B8A;&#xFF0C;&#x6BD4;&#x8F03;&#x597D;&#x7D50;&#x679C;&#x5C31;&#x662F;&#x72A7;&#x7272;&#x4E00;&#x9EDE;&#x9EDE;&#x6642;&#x9593;&#x63DB;&#x53D6;&#x66F4;&#x591A;&#x7684;&#x80FD;&#x91CF;&#x3002;</li>
</ol>
<p>&#x81F3;&#x65BC;&#x7B2C;&#x4E09;&#x7A2E;&#xFF0C;&#x53EA;&#x4F7F;&#x7528; A7 &#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x57F7;&#x884C;&#x6642;&#x9593;&#x5E7E;&#x4E4E;&#x662F;&#x5169;&#x500D;&#xFF0C;&#x4F46;&#x7701;&#x96FB;&#x91CF;&#x537B;&#x5F88;&#x53EF;&#x89C0;&#xFF0C;&#x56E0;&#x70BA;&#x672C;&#x8EAB;&#x5C31;&#x662F;&#x529F;&#x8017;&#x512A;&#x5316;&#x5C0E;&#x5411;&#x3002;<br>
&#x8A73;&#x7D30;&#x6BD4;&#x8F03;&#x53EF;&#x4EE5;&#x770B;&#x9019;&#x5F35;&#x8868;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/38563072-9a17a5dc-3d0e-11e8-8685-1356404ee9e2.png" alt="&#x6BD4;&#x8F03;"></p>
<h3>&#x63A1;&#x7528;&#x52D5;&#x614B;&#x6642;&#x8108;&#x96FB;&#x58D3;&#xFF08;Power Savings by DVFS without Perfor- mance Compromise&#xFF09;</h3>
<p>oracle predictor &#x662F;&#x4EE5;&#x4E0A;&#x5E1D;&#x8996;&#x89D2;&#x4F86;&#x770B;&#xFF0C;&#x5047;&#x8A2D;&#x6211;&#x5011;&#x90FD;&#x77E5;&#x9053;&#x600E;&#x6A23;&#x505A;&#x6700;&#x597D;&#x4E86;&#x3002;&#x4ED6;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x6A21;&#x578B;&#x8B93;&#x6211;&#x5011;&#x5728;&#x52D5;&#x614B;&#x8ABF;&#x6574;&#x6642;&#x8108;&#x548C;&#x96FB;&#x58D3;&#x7684;&#x904E;&#x7A0B;&#x4E2D;&#xFF0C;&#x53EF;&#x4EE5;&#x8B93;&#x6548;&#x80FD;&#x5E7E;&#x4E4E;&#x6C92;&#x6709;&#x6539;&#x8B8A;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6700;&#x512A;&#x5316;&#x6240;&#x9700;&#x7684;&#x6642;&#x8108;&#x96FB;&#x58D3;&#x3002;</p>
<p>&#x900F;&#x904E;&#x4EE5;&#x4E0B;&#x6A21;&#x578B;&#x9810;&#x6E2C;&#x6240;&#x9700;&#x7684;&#x529F;&#x7387;&#xFF0C;&#x53C3;&#x6578;&#x89E3;&#x91CB;&#x4E5F;&#x5728;&#x5716;&#x4E2D;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/38563769-3a17b486-3d10-11e8-930e-a7188a5d33a1.png" alt="&#x65B9;&#x7A0B;&#x5F0F;"></p>
<p>&#x5F9E;&#x4E0B;&#x5716;&#x4E2D;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#xFF0C;&#x9ED1;&#x7DDA;&#x70BA;&#x7406;&#x8AD6;&#x9810;&#x6E2C;&#xFF0C;&#x7070;&#x7DDA;&#x70BA;&#x5BE6;&#x969B;&#x5BE6;&#x9A57;&#xFF0C;&#x63A1;&#x7528;&#x6A21;&#x578B;&#x6642;&#xFF0C;&#x660E;&#x986F;&#x53EF;&#x4EE5;&#x6E1B;&#x5C11;&#x529F;&#x8017;&#x6D88;&#x8017;&#x3002;<br>
&#x9019;&#x908A;&#x4E5F;&#x4EE3;&#x8868;&#x7406;&#x8AD6;&#x4E0A;&#x80FD;&#x9054;&#x5230;&#x7684;&#x6700;&#x4F73;&#x503C;&#xFF0C;&#x4E0D;&#x7BA1;&#x600E;&#x6A23;&#x512A;&#x5316;&#xFF0C;&#x5373;&#x4FBF;&#x662F;&#x4E0A;&#x5E1D;&#x4E5F;&#x53EA;&#x80FD;&#x505A;&#x5230;&#x9019;&#x6A23;&#x597D;&#x800C;&#x5DF2;&#x3002;<br>
<img src="https://user-images.githubusercontent.com/18013815/38563848-75874a2c-3d10-11e8-89d7-7e6217e671d3.png" alt="&#x7406;&#x8AD6;&#x6BD4;&#x8F03;"></p>
<h3>&#x524D;&#x968E;&#x6BB5;&#x96FB;&#x9580;&#x63A7;&#x5236;&#xFF08;Post-Loading Phase Power Gating&#xFF09;</h3>
<p>&#x5728;&#x4E00;&#x958B;&#x59CB;&#x6211;&#x5011;&#x8A0E;&#x8AD6;&#x5230;&#xFF0C;&#x4E00;&#x958B;&#x59CB;&#x6700;&#x521D;&#x7684;&#x6642;&#x5019; A15 &#x4E26;&#x6C92;&#x6709;&#x505A;&#x4E8B;&#xFF0C;&#x537B;&#x7DAD;&#x6301;&#x9AD8;&#x983B;&#x7387;&#x3002;<br>
&#x6240;&#x4EE5;&#x4F5C;&#x8005;&#x8B93;&#x96FB;&#x9580;&#x95DC;&#x9589; A15 &#x76F4;&#x5230; A7 &#x4F7F;&#x7528;&#x7387;&#x9054;&#x5230; 110% &#x518D;&#x958B;&#x555F;&#x3002;&#xFF08;&#x9078;&#x64C7; 110% &#x662F;&#x56E0;&#x70BA;&#x524D;&#x968E;&#x6BB5;&#x8655;&#x7406;&#x5E7E;&#x4E4E;&#x90FD;&#x662F; A7 &#x55AE;&#x6838;&#x5FC3;&#x57F7;&#x884C;&#xFF09;<br>
&#x6BD4;&#x8F03;&#x5F8C;&#x767C;&#x73FE;&#xFF0C;&#x7D04;&#x83AB;&#x53EF;&#x4EE5;&#x7701;&#x4E0B; 10% &#x7684;&#x80FD;&#x6E90;&#x3002;</p>
<h2>&#x7D50;&#x8AD6;</h2>
<p>&#x700F;&#x89BD;&#x5668;&#x8655;&#x7406;&#x904E;&#x7A0B;&#x4E2D;&#xFF0C;&#x6709;&#x5F88;&#x591A;&#x968E;&#x6BB5;&#xFF0C;&#x85C9;&#x7531;&#x5DE7;&#x5999;&#x63A7;&#x5236;&#x7570;&#x8CEA;&#x8655;&#x7406;&#x5668;&#x7684;&#x4F7F;&#x7528;&#xFF0C;&#x53EF;&#x4EE5;&#x5728;&#x6BD4;&#x706B;&#x529B;&#x5168;&#x958B;&#x4E0B;&#x53EA;&#x7A0D;&#x5FAE;&#x6162;&#x4E00;&#x9EDE;&#xFF0C;&#x537B;&#x7701;&#x4E0B;&#x66F4;&#x591A;&#x96FB;&#x91CF;&#x3002;&#x800C;&#x9019;&#x6A23;&#x7684;&#x505A;&#x6CD5;&#x540C;&#x6A23;&#x4E5F;&#x53EF;&#x4EE5;&#x7528;&#x5728;&#x904A;&#x6232;&#x4E4B;&#x985E;&#x7684;&#x61C9;&#x7528;&#x8EDF;&#x9AD4;&#x4E0A;&#xFF0C;&#x4E5F;&#x662F;&#x7531;&#x8A31;&#x591A;&#x4E0D;&#x540C;&#x968E;&#x6BB5;&#x8655;&#x7406;&#x7A0B;&#x5E8F;&#x7D44;&#x6210;&#x3002;</p>
<p>&#x6700;&#x5F8C;&#x9664;&#x4E86;&#x4F5C;&#x8005;&#x5BE6;&#x9A57;&#x7528;&#x7684;&#x4E09;&#x661F;&#x624B;&#x6A5F;&#x4E4B;&#x5916;&#xFF0C;Apple &#x7684; iPhone &#x73FE;&#x5728;&#x4E5F;&#x90FD;&#x662F;&#x63A1;&#x7528; big.LITTLE &#x4E86;&#xFF0C;&#x800C;&#x76EE;&#x524D;&#x624B;&#x6A5F;&#x90FD;&#x662F;&#x63A1;&#x7528;&#x9810;&#x8A2D;&#x7684;&#x6700;&#x7C21;&#x55AE;&#x63A7;&#x5236;&#x6A21;&#x578B;&#xFF0C;&#x4E00;&#x500B;&#x7A69;&#x5B9A;&#x512A;&#x79C0;&#x7684;&#x65B0;&#x6A21;&#x578B;&#xFF0C;&#x53EF;&#x4EE5;&#x8B93;&#x624B;&#x6A5F;&#x63A1;&#x7528;&#x66F4;&#x7BC0;&#x80FD;&#x53C8;&#x6709;&#x6548;&#x7387;&#x7684;&#x4F7F;&#x7528;&#x9AD4;&#x9A57;&#x3002;&#x4F7F;&#x7528;&#x8005;&#x751A;&#x81F3;&#x53EF;&#x4EE5;&#x81EA;&#x7531;&#x6C7A;&#x5B9A;&#x662F;&#x5426;&#x8981;&#x7528;&#x300C;&#x706B;&#x529B;&#x5168;&#x958B;&#x300D;&#x6A21;&#x5F0F;&#xFF0C;&#x6216;&#x662F;&#x7528;&#x300C;&#x6700;&#x4F73;&#x5E73;&#x8861;&#x300D;&#x6A21;&#x5F0F;&#x3002;</p>
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
                
