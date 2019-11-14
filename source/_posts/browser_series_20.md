---
title: 用網頁相似性來優化瀏覽器
date: 2017-12-31 23:38:34
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x524D;&#x5169;&#x5929;&#xFF08;<a href="https://ithelp.ithome.com.tw/articles/10194936?sc=hot" target="_blank">1</a>&#xFF06;<a href="https://ithelp.ithome.com.tw/articles/10194725?sc=hot" target="_blank">2</a>&#xFF09;&#x90FD;&#x627E;&#x4E86;&#x6BD4;&#x8F03;&#x6709;&#x8DA3;&#x7684;&#x8AD6;&#x6587;&#x4F86;&#x5BEB;&#xFF0C;&#x6C92;&#x610F;&#x5916;&#x90FD;&#x767B;&#x4E0A;&#x71B1;&#x9580;&#x4E86;&#x3002;&#x4E0D;&#x904E;&#x662F;&#x6642;&#x5019;&#x56DE;&#x4F86;&#x8B1B;&#x4E00;&#x4E9B;&#x6BD4;&#x8F03;&#x786C;&#x7684;&#x6771;&#x897F;&#x4E86;&#xFF01;</p>
<h2>&#x8AD6;&#x6587;</h2>
<p>&#x4ECA;&#x5929;&#x7814;&#x7A76;&#x7684;&#x8AD6;&#x6587;&#x662F;&#x300C; <a href="http://wwwconference.org/proceedings/www2014/proceedings/p575.pdf" target="_blank">Similarity-based Web Browser Optimization</a> &#x300D;&#xFF0C;&#x9867;&#x540D;&#x601D;&#x7FA9;&#x662F;&#x4F7F;&#x7528;&#x7DB2;&#x9801;&#x672C;&#x8EAB;&#x5F97;&#x76F8;&#x4F3C;&#x6027;&#xFF0C;&#x8B93;&#x700F;&#x89BD;&#x5668;&#x6E32;&#x67D3;&#x7684;&#x6548;&#x80FD;&#x53EF;&#x4EE5;&#x66F4;&#x512A;&#x5316;&#x3002;&#x9019;&#x908A;&#x53EA;&#x622A;&#x53D6;&#x91CD;&#x9EDE;&#x548C;&#x52A0;&#x5165;&#x6211;&#x4E00;&#x4E9B;&#x5FC3;&#x5F97;&#xFF0C;&#x5927;&#x5BB6;&#x6709;&#x8208;&#x8DA3;&#x53EF;&#x4EE5;&#x9EDE;&#x9023;&#x7D50;&#x53BB;&#x770B;&#x539F;&#x59CB;&#x8AD6;&#x6587;&#x3002;</p>
<p>&#x5728;&#x770B;&#x672C;&#x6587;&#x4E4B;&#x524D;&#xFF0C;&#x63A8;&#x85A6;&#x5927;&#x5BB6;&#x5148;&#x770B;&#x4E00;&#x7BC7;&#x6587;&#x7AE0;&#x300C;<a href="https://blog.techbridge.cc/2016/04/02/Browser-Rendering-Optimization/" target="_blank">Browser Rendering Optimization(&#x4E2D;&#x6587;)</a>&#x300D;&#xFF0C;&#x9019;&#x662F;&#x4EE5;&#x524D;&#x7AEF;&#x958B;&#x767C;&#x8005;&#x89D2;&#x5EA6;&#x63A2;&#x8A0E;&#x5982;&#x4F55;&#x8B93;&#x7DB2;&#x9801;&#x6E32;&#x67D3;&#x66F4;&#x512A;&#x5316;&#x3002;&#x5148;&#x4E86;&#x89E3;&#x5982;&#x4F55;&#x5728;&#x524D;&#x7AEF;&#x4E2D;&#x505A;&#x512A;&#x5316;&#xFF0C;&#x518D;&#x4F86;&#x770B;&#x5982;&#x4F55;&#x4EE5;&#x700F;&#x89BD;&#x5668;&#x67B6;&#x69CB;&#x672C;&#x8EAB;&#x9054;&#x5230;&#x512A;&#x5316;&#xFF0C;&#x76F8;&#x4FE1;&#x6703;&#x66F4;&#x6709;&#x6536;&#x7A6B;&#xFF01;</p>
<hr>
<h2>&#x7C21;&#x4ECB;</h2>
<p>&#x9996;&#x5148;&#x6211;&#x5011;&#x5F9E;&#x904E;&#x53BB;&#x7814;&#x7A76;&#x4E2D;&#x77E5;&#x9053;&#x5E7E;&#x4EF6;&#x4E8B;</p>
<ul>
<li>CSS &#x548C; layout &#x7684;&#x8655;&#x7406;&#x4F54;&#x8655;&#x7406;&#x9801;&#x9762;&#x7684; 50% &#x5DE6;&#x53F3;</li>
<li>&#x512A;&#x5316; javascript &#x7684;&#x904B;&#x7B97;&#x6700;&#x591A;&#x5C31;&#x5FEB; 7&#xFF05; &#x5DE6;&#x53F3;</li>
</ul>
<p>&#x6240;&#x4EE5;&#x5982;&#x679C;&#x6211;&#x5011;&#x60F3;&#x505A;&#x512A;&#x5316;&#x700F;&#x89BD;&#x5668;&#x6E32;&#x67D3;&#x7684;&#x901F;&#x5EA6;&#xFF0C;&#x770B;&#x8D77;&#x4F86;&#x8457;&#x91CD;&#x5728; CSS &#x4F3C;&#x4E4E;&#x5F71;&#x97FF;&#x6700;&#x5927;&#xFF01;<br>
&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x6CBF;&#x7528; Zhang et.al &#x63D0;&#x5021;&#x7684; Smart Caching &#x60F3;&#x6CD5;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5C07; style &#x7B97;&#x597D;&#x7684;&#x7D50;&#x679C;&#x66AB;&#x5B58;&#xFF0C;&#x6E1B;&#x5C11;&#x4E4B;&#x5F8C;&#x78B0;&#x5230;&#x4E00;&#x6A23;&#x7684; style &#x9084;&#x8981;&#x91CD;&#x8907;&#x8A08;&#x7B97;&#x3002;</p>
<p>&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x50CF;&#x7DAD;&#x57FA;&#x767E;&#x79D1;&#x4E0D;&#x540C;&#x9805;&#x76EE;&#x9801;&#x9762;&#xFF0C;&#x76F8;&#x4F3C;&#x5EA6;&#x5C31;&#x5F88;&#x9AD8;<br>
<img src="https://user-images.githubusercontent.com/18013815/34462183-fcc89040-ee78-11e7-8e6b-77ca8e27f05c.png" alt></p>
<p>&#x518D;&#x4F86;&#x770B;&#x770B;&#x5404;&#x5BB6;&#x7DB2;&#x7AD9;&#x7684;&#x5B50;&#x7DB2;&#x9801;&#x76F8;&#x4F3C;&#x5EA6;&#x5982;&#x4F55;&#xFF0C;&#x5305;&#x542B; HTML &#x548C; CSS<br>
<img src="https://user-images.githubusercontent.com/18013815/34462196-3b305b60-ee79-11e7-9ff8-d7fb26e8353f.png" alt><br>
&#x4E0D;&#x7BA1;&#x662F; HTML &#x9084;&#x662F; CSS &#x7684;&#x6709;&#x4E00;&#x5B9A;&#x7684;&#x76F8;&#x4F3C;&#x5EA6;&#xFF0C;&#x5176;&#x4E2D; CSS &#x7684;&#x76F8;&#x4F3C;&#x5EA6;&#x9AD8;&#x9054;&#x516B;&#x6210;&#xFF0C;&#x4E5F;&#x610F;&#x5473;&#x8457;&#x5982;&#x679C;&#x80FD;&#x6E1B;&#x5C11;&#x8A08;&#x7B97;&#x9019;&#x4E9B;&#x90E8;&#x5206;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x901F;&#x5EA6;&#x5C31;&#x53EF;&#x4EE5;&#x66F4;&#x5FEB;&#xFF01;</p>
<hr>
<h2>&#x6982;&#x5FF5;</h2>
<p>&#x6240;&#x4EE5;&#x9019;&#x908A;&#x4F5C;&#x8005;&#x63D0;&#x5021;&#x4E00;&#x7A2E;&#x300C;&#x518D;&#x5229;&#x7528;&#x300D;style &#x7684;&#x65B9;&#x6CD5;&#xFF0C;&#x770B;&#x6982;&#x5FF5;&#x5716;&#x4E0D;&#x96E3;&#x7406;&#x89E3;<br>
<img src="https://user-images.githubusercontent.com/18013815/34462233-22b9f0e0-ee7a-11e7-87a1-5bbfb6a3c423.png" alt></p>
<hr>
<p>&#x63A5;&#x4E0B;&#x4F86;&#x770B;&#x9019;&#x5F35;&#x5716;&#xFF0C;&#x662F;&#x91CD;&#x9EDE;&#x4E86;&#xFF01;<br>
<img src="https://user-images.githubusercontent.com/18013815/34462292-55f201b8-ee7b-11e7-909d-e8ed65e58501.png" alt><br>
&#x6839;&#x64DA;&#x7814;&#x7A76;&#xFF0C;70% &#x4F7F;&#x7528;&#x8005;&#x9032;&#x5165;&#x9996;&#x9801;&#x5F8C;&#x4E0D;&#x6703;&#x518D;&#x56DE;&#x4F86;&#xFF0C;&#x56E0;&#x6B64;&#x5C0D;&#x9996;&#x9801;&#x505A; cache &#x6C92;&#x610F;&#x7FA9;&#x3002;&#x4F46;&#x662F;&#x7D71;&#x8A08;&#x986F;&#x793A; 60% &#x7684;&#x700F;&#x89BD;&#x884C;&#x70BA;&#x6703;&#x958B;&#x555F;&#x76F8;&#x4F3C;&#x7684;&#x5B50;&#x7DB2;&#x9801;&#xFF0C;&#x610F;&#x601D;&#x662F;&#x540C;&#x6A23;&#x8DEF;&#x5F91;&#x4E0B;&#x7684;&#x7DB2;&#x9801;&#x5011;&#xFF08;&#x6BD4;&#x65B9;&#x8AAA;&#x90FD;&#x5728; <code>\products\</code> &#x9019;&#x500B;&#x8DEF;&#x5F91;&#x4E0B;&#xFF0C;&#x53EF;&#x80FD;&#x5C31;&#x6709;&#x597D;&#x5E7E;&#x6A23;&#x5546;&#x54C1;&#x7684;&#x500B;&#x5225;&#x7DB2;&#x9801;&#xFF09;&#xFF0C;&#x6709;&#x975E;&#x5E38;&#x5927;&#x7684;&#x6A5F;&#x7387;&#x91CD;&#x8907;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x5C31;&#x91DD;&#x5C0D;&#x9019;&#x4E9B;&#x7DB2;&#x9801;&#x5EFA;&#x7ACB;&#x4E00;&#x500B; cache tree&#x3002;&#x9084;&#x8A18;&#x5F97;&#x6211;&#x5011;&#x4E4B;&#x524D;&#x63D0;&#x5230;&#x7684; DOM tree&#x3001;Style tree &#x55CE;&#xFF1F;&#x9019;&#x908A;&#x4E5F;&#x985E;&#x4F3C;&#xFF0C;&#x4F7F;&#x7528; <code>&lt;TagName, ID, Class&gt;</code> &#x5EFA;&#x7ACB;&#x6A39;&#xFF0C;&#x4E26;&#x76F4;&#x63A5;&#x5C0D;&#x7167; Style tree&#xFF0C;&#x5982;&#x679C;&#x767C;&#x73FE;&#x6709;&#x4E00;&#x6A23;&#x7684;&#x5C31;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x63D0;&#x53D6; cache&#x3002;</p>
<hr>
<h2>&#x6F14;&#x7B97;&#x6CD5;</h2>
<p>&#x63A5;&#x8457;&#x662F;&#x6F14;&#x7B97;&#x6CD5;&#x7684;&#x90E8;&#x5206;&#x4E86;&#xFF0C;&#x6982;&#x5FF5;&#x662F;&#x5982;&#x679C;&#x540C;&#x76EE;&#x9304;&#x4E0B;&#x6709;&#x5176;&#x4ED6;&#x7DB2;&#x9801;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x63A1;&#x7528;&#x4ED6;&#x5011;&#x7684; cache&#xFF0C;&#x82E5;&#x662F;&#x6C92;&#x6709;&#x5247;&#x641C;&#x5C0B;&#x9130;&#x8FD1;&#x8DEF;&#x5F91;&#x5176;&#x4ED6;&#x7DB2;&#x9801;&#x6709;&#x6C92;&#x6709;&#x6A5F;&#x6703;&#x3002;</p>
<p>&#x9996;&#x5148;&#x662F;&#x641C;&#x5C0B;&#xFF0C;&#x5C07;&#x6240;&#x6709;&#x7DB2;&#x9801;&#x4EE5; graph &#x7684;&#x65B9;&#x5F0F;&#x8655;&#x7406;&#xFF0C;&#x5C31;&#x6709;&#x4E86;&#x300C;&#x7DB2;&#x9801;&#x8DDD;&#x96E2;&#x300D;&#x7684;&#x6982;&#x5FF5;&#x3002;&#x7531;&#x65BC;&#x6700;&#x76F8;&#x9130;&#x7684;&#x7DB2;&#x9801;&#xFF08;&#x4E5F;&#x5C31;&#x662F;&#x8DEF;&#x5F91;&#x63A5;&#x8FD1;&#xFF09;&#x8D8A;&#x5BB9;&#x6613;&#x6709;&#x76F8;&#x4F3C;&#x7684; style&#xFF0C;&#x6240;&#x4EE5;&#x8DDD;&#x96E2;&#x6700;&#x77ED;&#x7684;&#x4E5F;&#x5C31;&#x8D8A;&#x6709;&#x53EF;&#x80FD;&#xFF0C;&#x65BC;&#x662F;&#x6211;&#x5011;&#x63A1;&#x7528; <a href="http://www.csie.ntnu.edu.tw/~u91029/Graph.html#4" target="_blank">Breadth-first Search(BFS)</a>&#x4F86;&#x505A;&#x9019;&#x4EF6;&#x4E8B;&#x3002;&#x5982;&#x679C;&#x7576;&#x524D;&#x7DB2;&#x9801;&#x9084;&#x6C92;&#x5EFA;&#x7ACB;&#x597D; style tree&#xFF0C;&#x5C31;&#x63A1;&#x7528; BFS &#x627E;&#x6700;&#x9130;&#x8FD1;&#x7684;&#x7DB2;&#x9801;&#x7684; style tree &#x4F86;&#x7528;&#x3002;</p>
<p>&#x518D;&#x4F86;&#x662F; style &#x7684;&#x6BD4;&#x5C0D;<br>
<img src="https://user-images.githubusercontent.com/18013815/34462376-88c2690a-ee7d-11e7-9143-6b8401e62449.png" alt><br>
&#x6211;&#x5011;&#x77E5;&#x9053; child &#x6703;&#x7E7C;&#x627F; parent&#xFF0C;&#x6240;&#x4EE5;&#x5982;&#x679C; parent &#x672C;&#x8EAB;&#x5C31;&#x4E0D;&#x4E00;&#x6A23;&#x4E86;&#xFF0C;&#x4E5F;&#x5C31;&#x4EE3;&#x8868; child &#x901A;&#x901A;&#x6C92;&#x6A5F;&#x6703;&#x7528; cache&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x8981;&#x91CD;&#x7B97;&#x3002;&#x90A3;&#x5982;&#x679C; parent &#x4E00;&#x6A23;&#xFF0C;&#x5247;&#x5C0D; child &#x4E00;&#x500B;&#x4E00;&#x500B;&#x6AA2;&#x67E5;&#x3002;</p>
<p>&#x7576;&#x7136;&#x4E5F;&#x6709;&#x53EF;&#x80FD;&#x6703;&#x78B0;&#x5230;&#x4E0D;&#x540C;&#x9801;&#x9762;&#xFF0C;&#x96D6;&#x7136;&#x90FD;&#x662F;&#x540C;&#x500B; DOM &#x537B;&#x500B;&#x5225;&#x5BA2;&#x88FD;&#x5316;&#xFF0C;&#x6240;&#x4EE5;&#x6BCF;&#x7576;&#x60F3;&#x8981;&#x91CD;&#x65B0;&#x5229;&#x7528; style &#x7684;&#x6642;&#x5019;&#xFF0C;&#x8981;&#x5148;&#x6AA2;&#x67E5; style &#x7684;&#x5167;&#x5BB9;&#x3002;</p>
<hr>
<h2>&#x6210;&#x6548;</h2>
<p>&#x63A5;&#x8457;&#x5C31;&#x662F;&#x770B;&#x6709;&#x6C92;&#x6709;&#x6548;&#x4E86;:<br>
&#x9019;&#x5F35;&#x67F1;&#x72C0;&#x5716;&#x986F;&#x793A;&#x6709;&#x6C92;&#x6709;&#x63A1;&#x7528;&#x9019;&#x500B;&#x65B9;&#x6CD5;&#x524D;&#x5F8C;&#x6240;&#x9700;&#x8981;&#x7684;&#x6642;&#x9593;&#xFF0C;&#x6709;&#x660E;&#x986F;&#x5730;&#x7E2E;&#x77ED;&#x6642;&#x9593;&#xFF01;<br>
<img src="https://user-images.githubusercontent.com/18013815/34462515-98e6e7a4-ee80-11e7-9458-2d2006193fc8.png" alt><br>
&#x9019;&#x5F35;&#x8868;&#x683C;&#x986F;&#x793A;&#x9019;&#x500B;&#x65B9;&#x6CD5;&#x6E1B;&#x5C11;&#x7684;&#x300C;&#x91CD;&#x8907;&#x904B;&#x7B97;&#x300D;&#x7684;&#x6BD4;&#x4F8B;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5148;&#x524D;&#x63D0;&#x5230;&#x4E00;&#x6A23;&#x7684; style &#x4E0D;&#x9700;&#x8981;&#x518D;&#x7B97;&#x4E00;&#x6B21;&#xFF0C;&#x53EF;&#x4EE5;&#x767C;&#x73FE;&#x6E1B;&#x5C11;&#x4E0D;&#x5C11;&#x6BD4;&#x4F8B;&#xFF0C;&#x7279;&#x5225;&#x662F;&#x91CD;&#x8907;&#x300C;&#x7E41;&#x96DC;&#x300D;CSS &#x7684;&#x6642;&#x5019;&#x6548;&#x679C;&#x6700;&#x986F;&#x8457;&#xFF01;<br>
<img src="https://user-images.githubusercontent.com/18013815/34462517-99ae67b6-ee80-11e7-9f86-a93bdf3cee59.png" alt></p>
<hr>
<h2>&#x5FC3;&#x5F97;</h2>
<p>&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x770B;&#x4E0B;&#x4F86;&#x4F3C;&#x4E4E;&#x89BA;&#x5F97;&#x5F88;&#x53B2;&#x5BB3;&#xFF0C;&#x7684;&#x78BA;&#x4ED6;&#x5728;&#x67D0;&#x4E9B;&#x7DB2;&#x7AD9;&#x4E0A;&#x9054;&#x5230;&#x5F88;&#x597D;&#x7684;&#x6548;&#x679C;&#x3002;&#x4F46;&#x505A;&#x7814;&#x7A76;&#x6642;&#x6211;&#x5011;&#x8981;&#x77E5;&#x9053;&#x6C92;&#x6709;&#x7D55;&#x5C0D;&#x7684;&#x597D;&#xFF0C;&#x4E5F;&#x6C92;&#x6709;&#x7D55;&#x5C0D;&#x7684;&#x58DE;&#x3002;&#x4EE5;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x4F86;&#x8AAA;&#xFF0C;&#x53EF;&#x4EE5;&#x80AF;&#x5B9A;&#x4ED6;&#x5728;&#x300C;&#x975C;&#x614B;&#x300D;&#x4EE5;&#x53CA;&#x6709;&#x76F8;&#x4F3C;&#x300C;&#x6A21;&#x677F;&#x300D;&#x7684;&#x7DB2;&#x7AD9;&#x4E0A;&#x8655;&#x7406;&#x6548;&#x679C;&#x5F88;&#x4E0D;&#x932F;&#xFF0C;&#x4F46;&#x5982;&#x679C;&#x662F;&#x300C;&#x52D5;&#x614B;&#x300D;&#x7684;&#x7DB2;&#x7AD9;&#x5462;&#xFF1F;&#x6050;&#x6015; cache &#x7684;&#x6548;&#x76CA;&#x5C31;&#x5F88;&#x5C0F;&#x4E86;&#xFF0C;&#x56E0;&#x70BA;&#x5927;&#x591A;&#x6578;&#x6771;&#x897F;&#x90FD;&#x662F; JS &#x7B97;&#x51FA;&#x4F86;&#x7684;&#x3002;&#x6B64;&#x5916;&#x5982;&#x679C;&#x662F;&#x975E;&#x5E38;&#x5BA2;&#x88FD;&#x5316;&#x7684;&#x7DB2;&#x7AD9;&#xFF08;&#x6BCF;&#x500B; DOM &#x90FD;&#x7368;&#x4E00;&#x7121;&#x4E8C;&#xFF09;&#xFF0C;&#x6548;&#x679C;&#x4E00;&#x6A23;&#x4E5F;&#x4E0D;&#x986F;&#x8457;&#x3002;</p>
<p>&#x9019;&#x6642;&#x5019;&#x6211;&#x5011;&#x5C31;&#x8981;&#x53D6;&#x6368;&#xFF0C;&#x5982;&#x679C;&#x6709;&#x6548;&#x90A3;&#x4E8B;&#x5148;&#x57F7;&#x884C;&#x512A;&#x5316;&#x5C31;&#x5F88;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x4F46;&#x5982;&#x679C;&#x78B0;&#x5230;&#x6B64;&#x65B9;&#x6CD5;&#x6C92;&#x6548;&#x7684;&#x7DB2;&#x7AD9;&#xFF0C;&#x90A3;&#x53EA;&#x662F;&#x5F92;&#x52DE;&#x7121;&#x529F;&#x6D6A;&#x8CBB;&#x8A08;&#x7B97;&#x800C;&#x5DF2;&#x3002;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x662F; 2014 &#x5E74;&#x7684;&#xFF0C;&#x5176;&#x5BE6;&#x6211;&#x6EFF;&#x597D;&#x5947;&#x6700;&#x65B0;&#x7684;&#x700F;&#x89BD;&#x5668;&#x6709;&#x6C92;&#x6709;&#x63A1;&#x7528;&#x985E;&#x4F3C;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x7684;&#x65B9;&#x6CD5;&#x505A;&#x512A;&#x5316;&#xFF1F;&#x6211;&#x60F3;&#xFF0C;&#x5982;&#x679C;&#x8ABF;&#x67E5;&#x986F;&#x793A;&#x5927;&#x591A;&#x6578;&#x7DB2;&#x7AD9;&#x90FD;&#x662F;&#x975C;&#x614B;&#x3001;&#x6A21;&#x677F;&#x7684;&#x8A71;&#xFF0C;&#x90A3;&#x5C31;&#x5F88;&#x6709;&#x7406;&#x7531;&#x628A;&#x9019;&#x500B;&#x512A;&#x5316;&#x65B9;&#x6CD5;&#x63A1;&#x7D0D;&#x9032;&#x4F86;&#xFF01;</p>
<p>&#x5F8C;&#x8A18;&#xFF1A;<br>
&#x540C;&#x6A23;&#x6982;&#x5FF5;&#x4E0B;&#x7684;&#x5EF6;&#x4F38;&#x60F3;&#x6CD5;</p>
<ul>
<li>&#x5229;&#x7528;&#x7DB2;&#x9801;&#x76F8;&#x4F3C;&#x6027;&#x4F86;&#x4E8B;&#x5148;&#x6AA2;&#x67E5;&#x5FEB;&#x53D6;&#x6709;&#x6C92;&#x6709;&#x904E;&#x671F;&#xFF08;&#x5927;&#x91CF;&#x6E1B;&#x5C11; RTT&#xFF09;</li>
<li>&#x5229;&#x7528;&#x7DB2;&#x9801;&#x76F8;&#x4F3C;&#x6027;&#x4E8B;&#x5148;&#x9032;&#x884C;&#x9810;&#x5FEB;&#x53D6;&#xFF08;&#x6211;&#x8A18;&#x5F97; Chrome &#x4F3C;&#x4E4E;&#x6709;&#x9019;&#x6A23;&#x505A;&#xFF09;</li>
</ul>
<hr>
<p>&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x6211;&#x5011;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
