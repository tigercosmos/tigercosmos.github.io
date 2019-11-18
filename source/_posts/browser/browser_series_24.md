---
title: Cache 並不會讓手機的瀏覽器更快？
date: 2018-01-04 23:49:02
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

<h2>&#x524D;&#x8A00;</h2>
<p>&#x770B;&#x5230;&#x4E00;&#x7BC7;&#x5F88;&#x795E;&#x5947;&#x7684;&#x8AD6;&#x6587;&#xFF1A;<a href="https://www.usenix.org/system/files/conference/atc16/atc16-paper-vesuna.pdf" target="_blank">Caching Doesn&#x2019;t Improve Mobile Web  Performance (Much)</a>&#xFF0C;&#x7FFB;&#x8B6F;&#x4E00;&#x4E0B;&#x5C31;&#x662F;&#xFF0C;&#x5728;&#x624B;&#x6A5F;&#x4E0A;&#x7684;&#x700F;&#x89BD;&#x5668;&#x63A1;&#x7528; Cache &#x6A5F;&#x5236;&#x4E26;&#x4E0D;&#x6703;&#x8B93;&#x700F;&#x89BD;&#x5668;&#x5FEB;&#x591A;&#x5C11;&#x3002;&#x4E8B;&#x5BE6;&#x4E0A;&#x662F;&#x6703;&#x5FEB;&#x4E00;&#x9EDE;&#xFF0C;&#x4F46;&#x771F;&#x7684;&#x53EA;&#x662F;&#x4E00;&#x9EDE;&#x9EDE;&#x3002;</p>
<p>&#x4E00;&#x500B;&#x5305;&#x542B; Google &#x5DE5;&#x7A0B;&#x5E2B;&#x7684;&#x7814;&#x7A76;&#x5718;&#x968A;&#x767C;&#x73FE;&#xFF0C;Cache &#x6A5F;&#x5236;&#x5728;&#x684C;&#x9762;&#x4E0A;&#x700F;&#x89BD;&#x5668;&#x53BB;&#x4EE5;&#x8B93;&#x901F;&#x5EA6;&#x9032;&#x6B65; 34 %&#xFF0C;&#x4F46;&#x5728;&#x624B;&#x6A5F;&#x4E0A;&#x700F;&#x89BD;&#x5668;&#x537B;&#x50C5;&#x50C5; 13 %&#x3002;&#x9019;&#x5F88;&#x5947;&#x602A;&#xFF0C;&#x771F;&#x7684;&#x5F88;&#x602A;&#xFF0C;Google &#x5DE5;&#x7A0B;&#x5E2B;&#x5FC3;&#x60F3;&#x300C;&#x6211;&#x5011;&#x5BB6;&#x7684; Chrome &#x61C9;&#x8A72;&#x5927;&#x5C0F;&#x901A;&#x5403;&#x554A;&#xFF1F;!&#x300D;&#x56DE;&#x9867;&#x4E00;&#x4E0B;&#x6211;&#x5011;&#x5728;&#x300C;<a href="https://ithelp.ithome.com.tw/articles/10194725" target="_blank">&#x70BA;&#x4EC0;&#x9EBC;&#x624B;&#x6A5F;&#x4E0A;&#x7DB2;&#x901F;&#x5EA6;&#x6BD4;&#x8F03;&#x6162;&#x5462;&#xFF1F;</a>&#x300D;&#x9019;&#x7BC7;&#x6587;&#x7AE0;&#x4E2D;&#x63D0;&#x5230;&#x7684;&#xFF0C;&#x7DB2;&#x8DEF;&#x5EF6;&#x9072;&#x4EE5;&#x53CA;&#x8F09;&#x5165;&#x76F8;&#x95DC;&#x6A94;&#x6848;&#x6703;&#x4F7F;&#x5F97;&#x4F7F;&#x7528;&#x8005;&#x611F;&#x53D7;&#x5230;&#x700F;&#x89BD;&#x5668;&#x5F88;&#x5361;&#x3002;&#x800C; Cache &#x662F;&#x6307;&#x700F;&#x89BD;&#x5668;&#x5C07;&#x4E00;&#x4E9B;&#x8CC7;&#x6E90;&#x66AB;&#x5B58;&#x8D77;&#x4F86;&#xFF0C;&#x4E0B;&#x6B21;&#x8981;&#x7528;&#x6642;&#x5C31;&#x4E0D;&#x9700;&#x8981;&#x518D;&#x4E0B;&#x8F09;&#xFF0C;&#x7406;&#x8AD6;&#x4E0A;&#x61C9;&#x8A72;&#x5F88;&#x5FEB;&#x554A;&#xFF1F;&#x5C24;&#x5176;&#x7DB2;&#x8DEF;&#x662F;&#x95DC;&#x9375;&#x7684;&#x7684;&#x6642;&#x5019;&#x66F4;&#x8A72;&#x662F;&#x5982;&#x6B64;&#xFF1F;</p>
<p>&#x63A5;&#x4E0B;&#x4F86;&#x6211;&#x5011;&#x4F86;&#x770B;&#x770B;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x505A;&#x4E86;&#x751A;&#x9EBC;&#x7814;&#x7A76;&#x4F86;&#x89E3;&#x91CB;&#x9019;&#x500B;&#x795E;&#x5947;&#x7684;&#x73FE;&#x8C61;&#xFF01;</p>
<blockquote>
<p>&#x8A3B;: &#x4EE5;&#x4E0B;&#x7684;&#x5716;&#x7247;&#x7686;&#x4F86;&#x81EA;&#x539F;&#x59CB;&#x8AD6;&#x6587;</p>
</blockquote>
<hr>
<h2>&#x4E00;&#x4E9B;&#x5148;&#x5099;&#x77E5;&#x8B58;</h2>
<p>&#x700F;&#x89BD;&#x5668;&#x7684;&#x6D41;&#x7A0B;&#x5716;&#x6211;&#x5011;&#x5DF2;&#x7D93;&#x770B;&#x5F88;&#x591A;&#x4E86;&#xFF0C;&#x4E0D;&#x904E;&#x4ECA;&#x5929;&#x7684;&#x591A;&#x4E86;&#x4E00;&#x500B; cache<br>
<img src="https://user-images.githubusercontent.com/18013815/34571132-ada1c72e-f1a8-11e7-98e4-44e8c0649bb6.png" alt><br>
&#x8F09;&#x4E0B;&#x4F86;&#x7684;&#x8CC7;&#x6E90;&#x6703;&#x5B58;&#x5728; cache &#x4EE5;&#x4FBF;&#x4E0D;&#x6642;&#x4E4B;&#x9700;&#x3002;</p>
<hr>
<p>&#x518D;&#x4F86;&#x6211;&#x5011;&#x770B;&#x4E00;&#x4E0B;&#x8F09;&#x5165;&#x8CC7;&#x6E90;&#x7684;&#x6642;&#x7A0B;&#x5716;<br>
<img src="https://user-images.githubusercontent.com/18013815/34571304-1359ecea-f1a9-11e7-8d45-12dda2b88a7c.png" alt><br>
&#x9019;&#x908A;&#x6211;&#x5011;&#x5B9A;&#x7FA9;&#x5169;&#x500B;&#x540D;&#x8A5E; Page Load Time&#xFF08;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x6642;&#x9593;&#xFF09;&#x548C; Critical Path&#xFF08;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#xFF09;&#x3002;<br>
&#x6240;&#x8B02;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x6642;&#x9593;&#x5C31;&#x662F;&#x7576;&#x700F;&#x89BD;&#x5668;&#x958B;&#x59CB;&#x4E0B;&#x8F09;&#x5230;&#x4E00;&#x5207;&#x5C31;&#x7DD2;&#x7684;&#x6642;&#x9593;&#xFF0C;&#x901A;&#x5E38;&#x5C31;&#x662F;&#x5F9E;&#x958B;&#x59CB;&#x8DD1;&#x5230; js &#x7684; <code>onload</code> &#x88AB;&#x547C;&#x53EB;&#x7684;&#x6642;&#x5019;&#x3002;<br>
&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x5247;&#x662F;&#x8F09;&#x5165;&#x904E;&#x7A0B;&#x4E2D;&#x6240;&#x9700;&#x8981;&#x7684;&#x6700;&#x9577;&#x8DEF;&#x5F91;&#x3002;&#x600E;&#x9EBC;&#x8AAA;&#x5462;&#xFF1F;&#x56E0;&#x70BA;&#x4E0D;&#x76F8;&#x5E72;&#x7684;&#x6771;&#x897F;&#x53EF;&#x4EE5;&#x540C;&#x6642;&#x4E00;&#x8D77;&#x8F09;&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x6709;&#x95DC;&#x806F;&#x6027;&#x7684;&#x6771;&#x897F;&#xFF0C;&#x5C31;&#x5FC5;&#x7136;&#x6703;&#x6709;&#x5148;&#x5F8C;&#x9806;&#x5E8F;&#x4E86;&#xFF0C;&#x53EF;&#x80FD;&#x662F;&#xFF21;&#x88E1;&#x9762;&#x547C;&#x53EB;&#xFF22;&#xFF0C;&#xFF22;&#x518D;&#x4E4E;&#x53EB;&#xFF23;&#x3002;</p>
<p>&#x6211;&#x5011;&#x5C07;&#x6703;&#x4F7F;&#x7528;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x5206;&#x6790;&#xFF08;critical path analysis&#xFF09;&#x975E;&#x5E38;&#x9069;&#x5408;&#x7528;&#x5728;&#x5E73;&#x884C;&#x5316;&#x8655;&#x7406;&#x7684;&#x670D;&#x52D9;&#x4E0A;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x5C31;&#x975E;&#x5E38;&#x9069;&#x5408;&#xFF0C;&#x4EFB;&#x4F55;&#x4E0D;&#x662F;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x4E0A;&#x7684;&#x512A;&#x5316;&#x90FD;&#x4E0D;&#x6703;&#x8B93;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x6642;&#x9593;&#x8B8A;&#x77ED;&#xFF0C;&#x5982;&#x540C;&#x4E0A;&#x5716;&#x4E2D; png &#x7684;&#x6642;&#x9593;&#x8B8A;&#x77ED;&#x4E5F;&#x4E0D;&#x6703;&#x5F71;&#x97FF;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x3002;</p>
<hr>
<h2>&#x5EFA;&#x7ACB;&#x6A21;&#x578B;</h2>
<p>&#x4EE5;&#x4E0A;&#x7684;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x53EF;&#x4EE5;&#x7528;&#x4E00;&#x500B;&#x6578;&#x5B78;&#x6A21;&#x578B;&#x8868;&#x793A;&#x3002;</p>
<pre><code>X: &#x5FEB;&#x53D6;&#x518D;&#x6B21;&#x88AB;&#x4F7F;&#x7528;&#x7684;&#x6BD4;&#x4F8B;&#xFF08;cache hit ratio&#xFF09;
K: &#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x4E0A;&#x53EF;&#x4EE5;&#x88AB;&#x5FEB;&#x53D6;&#x7684;&#x7269;&#x4EF6;&#x6BD4;&#x4F8B;
N: &#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x7684;&#x7DB2;&#x8DEF;&#x5EF6;&#x9072;
C: &#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x4E0A;&#x7684;&#x8A08;&#x7B97;&#x5EF6;&#x9072;
f(x): N &#x548C; C &#x6709;&#x91CD;&#x758A;&#x7684;&#x6642;&#x9593;&#xFF08;&#x6975;&#x5C11;&#x6578;&#x72C0;&#x6CC1;&#x525B;&#x597D;&#xFF2E;&#x548C;&#xFF23;&#x4E26;&#x884C;&#xFF0C;&#x901A;&#x5E38;&#x5FFD;&#x7565;&#xFF09;
</code></pre>
<p>&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x4E0A;&#x7684;&#x7269;&#x4EF6;&#x5C0E;&#x81F4;&#x7DB2;&#x8DEF;&#x5EF6;&#x9072;&#x7684;&#x6A5F;&#x7387;&#xFF08;Pr&#xFF09;&#xFF1A;<br>
<code>1&#x2212;Pr(&#x53EF;&#x5FEB;&#x53D6;)&#xB7;Pr(&#x5FEB;&#x53D6;&#x53EF;&#x518D;&#x5229;&#x7528;|&#x53EF;&#x5FEB;&#x53D6;)</code><br>
&#x9810;&#x671F;&#x7684;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x6642;&#x9593;&#xFF08;E&#xFF09;&#x53EF;&#x4EE5;&#x8868;&#x793A;&#x6210;&#xFF1A;<br>
<code>E[X]=C+(1&#x2212;K&#xB7;X)&#xB7;N&#x2212;f(X)</code></p>
<p>&#x6709;&#x6C92;&#x6709;&#x5F88;&#x795E;&#x5947;&#xFF01;</p>
<hr>
<h2>&#x4F30;&#x8A08;&#x6A21;&#x578B;</h2>
<p>&#x9996;&#x5148;&#x4F86;&#x770B;&#xFF2E;&#x548C;&#xFF23;&#xFF0C;&#x6211;&#x5011;&#x7528;&#x4EE5;&#x4E0B;&#x9019;&#x5F35;&#x5716;&#x7684;&#x6578;&#x64DA;&#x4F86;&#x4F30;&#x7B97;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34572981-e376b56c-f1ad-11e7-83a1-34f0894b339b.png" alt><br>
comp &#x6578;&#x5B57;&#x8D8A;&#x5927;&#x4EE3;&#x8868; CPU &#x8D8A;&#x6162;&#xFF0C;&#x53EF;&#x4EE5;&#x767C;&#x73FE; CPU &#x8D8A;&#x5DEE;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x6642;&#x9593;&#x8D8A;&#x9577;&#xFF0C;&#x6EFF;&#x5408;&#x7406;&#x7684;&#x3002;<br>
&#x518D;&#x4F86; x &#x8EF8;&#x662F;&#x7DB2;&#x8DEF;&#x901F;&#x5EA6;&#xFF0C;&#x901F;&#x5EA6;&#x8D8A;&#x6162;&#x8F09;&#x5165;&#x6642;&#x9593;&#x8D8A;&#x9577;&#xFF0C;&#x4E5F;&#x5F88;&#x5408;&#x7406;&#x3002;</p>
<p>&#x518D;&#x4F86;&#x662F;&#xFF2B;&#xFF0C;&#x4E00;&#x822C;&#x800C;&#x8A00;&#x6709; 65&#xFF05;&#x7684;&#x7269;&#x4EF6;&#x53EF;&#x4EE5;&#x88AB;&#x5FEB;&#x53D6;&#xFF0C;&#x4F46;&#x53EA;&#x6709; 20&#xFF05;&#x7684;&#x7269;&#x4EF6;&#x6703;&#x518D;&#x6B21;&#x88AB;&#x4F7F;&#x7528;&#x3002;&#x6240;&#x4EE5;&#xFF2B;&#x5C31;&#x662F; 0.2&#x3002;</p>
<p>f(X)&#x901A;&#x5E38;&#x53EF;&#x4EE5;&#x6975;&#x5C0F;&#xFF0C;&#x6240;&#x4EE5;&#x5728;&#x6A21;&#x578B;&#x4E2D;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x5FFD;&#x8996;&#x3002;</p>
<p>&#x81F3;&#x65BC;&#xFF38;&#x5247;&#x662F;&#x6211;&#x5011;&#x7684;&#x64CD;&#x7E31;&#x8B8A;&#x56E0;&#xFF0C;&#x4E5F;&#x662F;&#x6574;&#x500B;&#x547D;&#x984C;&#x7684;&#x6838;&#x5FC3;&#xFF0C;&#x7A76;&#x7ADF; Cache &#x5230;&#x5E95;&#x6709;&#x6C92;&#x6709;&#x6548;&#xFF1F;</p>
<hr>
<h2>&#x5BE6;&#x9A57;</h2>
<p>&#x6709;&#x4E86;&#x6A21;&#x578B;&#x4E4B;&#x5F8C;&#xFF0C;&#x7576;&#x7136;&#x5C31;&#x662F;&#x505A;&#x5BE6;&#x9A57;&#x554A;&#xFF01;<br>
<img src="https://user-images.githubusercontent.com/18013815/34573610-a97e68e4-f1af-11e7-81fa-bf6bb0973991.png" alt><br>
Web Page Replay(WPR) &#x662F;&#x4E00;&#x500B;&#x7D00;&#x9304;&#x9023;&#x7DDA;&#x4E00;&#x500B; URL &#x6240;&#x6709; request &#x548C; reponse &#x7684;&#x88DD;&#x7F6E;&#xFF0C;&#x9019;&#x500B;&#x6771;&#x897F;&#x7684;&#x76EE;&#x7684;&#x662F;&#x88FD;&#x9020;&#x4E00;&#x500B;&#x7A69;&#x5B9A;&#x7684;&#x5047;&#x60F3;&#x9023;&#x7DDA;&#x3002;&#x4F7F;&#x7528;&#x65B9;&#x5F0F;&#x5C31;&#x662F;&#x6211;&#x5148;&#x7528; WPR &#x9023;&#x4E00;&#x500B;&#x7DB2;&#x7AD9;&#xFF0C;&#x8A18;&#x4E0B;&#x6240;&#x6709;&#x6D41;&#x7A0B;&#xFF0C;&#x4E4B;&#x5F8C;&#x5BE6;&#x9A57;&#x90FD;&#x7528; WPR &#x7684;&#x7D00;&#x9304;&#x4F86;&#x6E2C;&#x8A66;&#x3002;</p>
<p>&#x800C; telemetry &#x5C31;&#x662F;&#x4E00;&#x500B;&#x8A18;&#x9304;&#x6642;&#x9593;&#x7684;&#x8EDF;&#x9AD4;&#xFF0C;&#x85C9;&#x7531; WPR &#x7684;&#x7D00;&#x9304;&#x4F86;&#x5C0D;&#x684C;&#x9762;&#x4EE5;&#x53CA;&#x884C;&#x52D5;&#x88DD;&#x7F6E;&#x7684;&#x700F;&#x89BD;&#x5668;&#x505A;&#x6E2C;&#x8A66;&#x3002;</p>
<hr>
<h2>&#x5BE6;&#x9A57;&#x7D50;&#x679C;</h2>
<p>&#x6E2C;&#x8A66;&#x6578;&#x64DA;&#x4E2D;&#x8D85;&#x904E; 90% &#x7684;&#x7DB2;&#x9801;&#x53EF;&#x4EE5;&#x6709;&#x8D85;&#x904E; 90%&#x7684;&#x7269;&#x4EF6;&#x88AB;&#x5FEB;&#x53D6;&#x3002;&#x7406;&#x8AD6;&#x4E0A;&#x9019;&#x9EBC;&#x9AD8;&#x7684;&#x6BD4;&#x4F8B;&#xFF0C;&#x5982;&#x679C;&#x8B93;&#x5FEB;&#x53D6;&#x91CF;&#x589E;&#x52A0;&#xFF0C;&#x901F;&#x5EA6;&#x61C9;&#x8A72;&#x66F4;&#x5FEB;&#x5427;&#xFF0C;&#x56E0;&#x70BA;&#x7DB2;&#x8DEF;&#x6642;&#x9593;&#x662F;&#x4E00;&#x5927;&#x56E0;&#x5B50;&#x3002;</p>
<p>&#x4F46;&#x7D50;&#x679C;&#x5F88;&#x4E0D;&#x5E78;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34574485-7e005792-f1b2-11e7-9dba-bec219d09550.png" alt><br>
&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x770B;&#x5230; 20% &#x8DDF; 30% &#x5FEB;&#x53D6;&#x91CF;&#x7684;&#x8F09;&#x5165;&#x6642;&#x9593;&#x7ADF;&#x7136;&#x4E00;&#x6A23;&#x3002;&#x9019;&#x908A; 30% &#x6709;&#x88AB;&#x63A7;&#x5236;&#x5FC5;&#x5B9A;&#x5305;&#x542B; 20% &#x7684;&#x5FEB;&#x53D6;&#x3002;<br>
&#x5B8C;&#x5168;&#x6253;&#x7834;&#x6211;&#x5011;&#x7684;&#x60F3;&#x50CF;&#x3002;</p>
<p>&#x518D;&#x4F86;&#x770B;&#x5982;&#x679C;&#x662F;&#x300C;&#x5B8C;&#x7F8E;&#x300D;&#x7684; Cache &#x60C5;&#x6CC1;&#x4E0B;&#x5462;&#xFF1F;<br>
<img src="https://user-images.githubusercontent.com/18013815/34574658-07348402-f1b3-11e7-8209-44c421c27fc4.png" alt><br>
&#x7E31;&#x8EF8;&#x662F;&#x6240;&#x6709;&#x6E2C;&#x8A66;&#x7684;&#x7DB2;&#x7AD9;&#x6240;&#x4F54;&#x7684;&#x6BD4;&#x4F8B;&#xFF0C;&#x6A6B;&#x8EF8;&#x662F;&#x7E2E;&#x77ED;&#x6642;&#x9593;&#x6BD4;&#x4F8B;&#x3002;&#x7D50;&#x679C;&#x5C31;&#x5982;&#x540C;&#x672C;&#x6587;&#x958B;&#x982D;&#x8AAA;&#x7684;&#xFF0C;&#x684C;&#x9762;&#x7248;&#x9032;&#x6B65; 34&#xFF05;&#xFF0C;&#x884C;&#x52D5;&#x7248;&#x537B;&#x53EA;&#x6709; 13&#xFF05;&#x3002;</p>
<p>&#x540C;&#x4E00;&#x5F35;&#x5716;&#x9084;&#x6709;&#x53E6;&#x5916;&#x5169;&#x500B;&#x5BE6;&#x9A57;&#xFF0C;&#x6211;&#x5011;&#x5C07;&#x684C;&#x9762;&#x7684; CPU &#x548C; RAM &#x88AB;&#x9650;&#x5236;&#x3002;<br>
&#x7D50;&#x679C;&#x6211;&#x5011;&#x767C;&#x73FE; RAM &#x88AB;&#x9650;&#x5236;&#x4E0D;&#x5F71;&#x97FF;&#x7D50;&#x679C;&#x3002;<br>
&#x4F46;&#x88AB;&#x9650;&#x5236;&#x7684; CPU &#x537B;&#x975E;&#x5E38;&#x63A5;&#x8FD1;&#x884C;&#x52D5;&#x88DD;&#x7F6E;&#x7684;&#x5BE6;&#x9A57;&#x7D50;&#x679C;&#x3002;</p>
<p>&#x65BC;&#x662F;&#x6211;&#x5011;&#x518D;&#x4F86;&#x770B;&#x9019;&#x5F35;&#x5716;&#xFF1A;<br>
<img src="https://user-images.githubusercontent.com/18013815/34574894-c8ba6588-f1b3-11e7-9d03-4722cf893b41.png" alt><br>
CPU &#x8D8A;&#x6162;&#x771F;&#x7684;&#x5C0E;&#x81F4;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x6642;&#x9593;&#x8B8A;&#x6162;&#x3002;&#x5982;&#x540C;&#x5148;&#x524D;&#x5047;&#x8A2D;&#x7684;&#x3002;</p>
<p>&#x5982;&#x679C;&#x6211;&#x5011;&#x8B93; Cache &#x589E;&#x52A0; 10%&#x770B;&#x770B;&#x7D50;&#x679C;&#x5462;&#xFF1F;<br>
<img src="https://user-images.githubusercontent.com/18013815/34575149-a474ee90-f1b4-11e7-94ea-255d19e2a546.png" alt><br>
&#x4E0D;&#x5E78;&#x7684;&#xFF0C;&#x55AE;&#x9801;&#x8F09;&#x5165;&#x901F;&#x5EA6;&#x53EA;&#x5FEB;&#x4E86; 1%&#x3002;&#x8B49;&#x660E;&#x8AAA; Cache &#x5E7E;&#x4E4E;&#x4E0D;&#x6703;&#x5F71;&#x97FF;&#x3002;</p>
<p>&#x9019;&#x6642;&#x5019;&#x6211;&#x5011;&#x56DE;&#x5230;&#x6211;&#x5011;&#x4E00;&#x958B;&#x59CB;&#x7684;&#x6578;&#x5B78;&#x6A21;&#x578B;&#xFF0C;&#xFF38;&#x4EE3;&#x8868;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x7684;&#x5FEB;&#x53D6;&#x518D;&#x6B21;&#x88AB;&#x5229;&#x7528;&#x7684;&#x6A5F;&#x7387;&#xFF0C;&#x800C;&#x5BE6;&#x9A57;&#x4E5F;&#x8B49;&#x660E;&#x6A21;&#x578B;&#x662F;&#x6709;&#x9053;&#x7406;&#x7684;&#xFF0C;&#x5FEB;&#x53D6;&#x91CF;&#x589E;&#x52A0;&#x5C0D;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x4E0A;&#x7684;&#x7269;&#x4EF6;&#x5F71;&#x97FF;&#x5FAE;&#x4E4E;&#x5176;&#x5FAE;&#x3002;&#x81EA;&#x7136;&#x6642;&#x9593;&#x4E5F;&#x4E0D;&#x6703;&#x7E2E;&#x77ED;&#x3002;</p>
<blockquote>
<p><code>E[X]=C+(1&#x2212;K&#xB7;X)&#xB7;N&#x2212;f(X)</code>&#xFF1A;&#xFF38;&#x975E;&#x5E38;&#x5C0F;&#x7684;&#x8A71;&#xFF0C;&#x90A3;&#x9EBC;<code>(1-K&#xB7;X)</code> &#x5E7E;&#x4E4E;&#x9084;&#x662F; 1&#x3002;</p>
</blockquote>
<hr>
<h2>&#x7D50;&#x8AD6;</h2>
<p>&#x6240;&#x4EE5;&#x70BA;&#x4EC0;&#x9EBC; Cache &#x6C92;&#x6548;&#x5462;&#xFF1F;</p>
<p>&#x6211;&#x5011;&#x7684;&#x6A21;&#x578B;&#x662F; <code>E[X]=C+(1&#x2212;K&#xB7;X)&#xB7;N&#x2212;f(X)</code>&#xFF0C;&#x6CE8;&#x610F;&#x9019;&#x908A;&#xFF23;(CPU)&#x548C;&#xFF38;(Cache)&#x540C;&#x6642;&#x5F71;&#x97FF;&#x4E86;&#x9019;&#x689D;&#x5F0F;&#x5B50;&#x3002;&#x7576;&#xFF23;&#x7684;&#x5F71;&#x97FF;&#x88AB;&#x653E;&#x5927;&#x7684;&#x6642;&#x5019;&#xFF0C;&#xFF38;&#x7684;&#x5F71;&#x97FF;&#x5C31;&#x6703;&#x88AB;&#x5F31;&#x5316;&#x3002;&#x9019;&#x4E5F;&#x662F;&#x70BA;&#x4EC0;&#x9EBC;&#x684C;&#x9762;&#x7248;&#x700F;&#x89BD;&#x5668;&#x6709;&#x660E;&#x986F;&#x9032;&#x6B65;&#xFF0C;&#x884C;&#x52D5;&#x7248;&#x537B;&#x6C92;&#x6709;&#x3002;&#x5176;&#x5BE6;&#x884C;&#x52D5;&#x7248;&#x7684; Cache &#x4E5F;&#x6709;&#x8CA2;&#x737B;&#xFF0C;&#x53EA;&#x662F;&#x88AB; CPU &#x5403;&#x6389;&#x4E86;&#x3002;</p>
<p>&#x6B64;&#x5916; Cache &#x4E5F;&#x4E0D;&#x898B;&#x5F97;&#x4E00;&#x5B9A;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x6211;&#x5011;&#x5728;&#x4E4E;&#x7684;&#x662F;&#x300C;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x300D;&#xFF0C;&#x8981;&#x662F;&#x8DEF;&#x5F91;&#x6578;&#x91CF;&#x5F88;&#x591A;&#xFF0C;Cache &#x88AB;&#x5E73;&#x5206;&#x5230;&#x5404;&#x500B;&#x8DEF;&#x5F91;&#x4E0A;&#xFF0C;&#x90A3;&#x9EBC;&#x95DC;&#x9375;&#x8DEF;&#x5F91;&#x53D7;&#x60E0;&#x7684;&#x7A0B;&#x5EA6;&#x4E5F;&#x5C31;&#x5F88;&#x5C0F;&#x3002;</p>
<p>&#x6700;&#x5F8C;&#x5C31;&#x662F; CPU &#x7684;&#x6280;&#x8853;&#x65E5;&#x65B0;&#x6708;&#x7570;&#xFF0C;&#x90A3;&#x672A;&#x4F86;&#x7684;&#x8A71;&#xFF0C;&#x5982;&#x4F55;&#x8B93; Cache &#x66F4;&#x6709;&#x6548;&#x5C31;&#x6703;&#x662F;&#x95DC;&#x9375;&#x4E86;&#xFF01;</p>
<p>&#x5F8C;&#x8A18;&#xFF1A;<br>
&#x9019;&#x7BC7;&#x7528;&#x7684;&#x624B;&#x6A5F;&#x6642;&#x8108;&#x5F88;&#x4F4E;&#xFF0C;&#x800C;&#x6700;&#x65B0;&#x7684; iPhone A11 &#x6642;&#x8108;&#x903C;&#x8FD1; Macbook Pro &#x4E86;&#xFF0C;&#x5728;&#x6700;&#x9AD8;&#x6548;&#x80FD;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;CPU &#x7684;&#x5F71;&#x97FF;&#x56E0;&#x5B50;&#x53EF;&#x7528;&#x53C8;&#x6703;&#x8B8A;&#x5C0F;&#xFF0C;&#x90A3;&#x9019;&#x908A;&#x7684;&#x7D50;&#x8AD6;&#x5C31;&#x6703;&#x622A;&#x7136;&#x4E0D;&#x540C;&#x3002;&#x6240;&#x4EE5;&#x53EF;&#x4EE5;&#x8AAA;&#x9019;&#x7BC7;&#x7684;&#x7D50;&#x8AD6;&#x662F;&#x7528;&#x300C;&#x4E2D;&#x968E;&#x300D;&#x6B3E;&#x624B;&#x6A5F;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x4E00;&#x822C;&#x5E02;&#x9762;&#x4E0A;&#x7684;&#x666E;&#x904D;&#x72C0;&#x6CC1;&#x3002;</p>
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
                
