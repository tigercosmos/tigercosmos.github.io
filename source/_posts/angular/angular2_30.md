---
title: Angular 2 給初學者的學習指南
date: 2017-01-15 23:48:39
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x4E00;&#x500B;&#x6708;&#x524D;&#xFF0C;&#x6211;&#x958B;&#x59CB;&#x4E86;&#x4E00;&#x4EFD;&#x524D;&#x7AEF;&#x5DE5;&#x7A0B;&#x5E2B;&#x7684;&#x5DE5;&#x8B80;&#xFF0C;&#x90A3;&#x6642;&#x5019;&#x7684;&#x6211;&#x505A;&#x904E;&#x5E7E;&#x500B;&#x5C08;&#x6848;&#xFF0C;&#x4F46;&#x6C92;&#x4F7F;&#x7528;&#x904E; Anuglar 2&#xFF0C;&#x800C;&#x516C;&#x53F8;&#x898F;&#x5B9A;&#x524D;&#x7AEF;&#x4EE5; Angular 2 &#x958B;&#x767C;&#xFF0C;&#x65BC;&#x662F;&#x6211;&#x4FBF;&#x958B;&#x59CB;&#x63A2;&#x7D22;&#xFF0C;&#x9069;&#x9022; IT &#x90A6;&#x5E6B;&#x5FD9;&#x9435;&#x4EBA;&#x7684;&#x6D3B;&#x52D5;&#xFF0C;&#x60F3;&#x8AAA;&#x6709;&#x500B;&#x903C;&#x81EA;&#x5DF1;&#x5B78;&#x7FD2;&#x7684;&#x6D3B;&#x52D5;&#x53C3;&#x52A0;&#x4E5F;&#x883B;&#x597D;&#x7684;&#xFF0C;&#x5C31;&#x958B;&#x59CB;&#x4E86;&#x6211;&#x75DB;&#x82E6;&#x7684;&#x4E00;&#x500B;&#x6708;&#x3002;&#x9019;&#x4E00;&#x500B;&#x6708;&#x6BCF;&#x5929;&#x90FD;&#x82B1;&#x597D;&#x5E7E;&#x500B;&#x5C0F;&#x6642;&#x67E5;&#x8CC7;&#x6599;&#x6253;&#x6587;&#x7AE0;&#xFF0C;&#x9435;&#x4EBA;&#x8CFD;&#x9084;&#x7D93;&#x904E;&#x671F;&#x672B;&#x8003;&#xFF0C;&#x671F;&#x672B;&#x8003;&#x90A3;&#x9663;&#x5B50;&#x6211;&#x90FD;&#x662F;&#x5148;&#x6253;&#x5B8C;&#x6587;&#x7AE0;&#x6709;&#x5269;&#x4E0B;&#x6642;&#x9593;&#x624D;&#x53BB;&#x5FF5;&#x4E00;&#x9EDE;&#x66F8;&#xFF0C;&#x6211;&#x60F3;&#x65E2;&#x7136;&#x90FD;&#x6709;&#x6C7A;&#x5FC3;&#x8981;&#x53C3;&#x52A0;&#x9435;&#x4EBA;&#x8CFD;&#xFF0C;&#x90A3;&#x4E0D;&#x7BA1;&#x5982;&#x4F55;&#x90FD;&#x8981;&#x505A;&#x5230;&#x5E95;&#x3002;</p>
<p>&#x9019;&#x5E7E;&#x4E09;&#x5341;&#x7BC7;&#x7684;&#x6587;&#x7AE0;&#x662F;&#x6211;&#x4EE5;&#x521D;&#x5B78;&#x8005;&#x7684;&#x89D2;&#x5EA6;&#xFF0C;&#x5C07;&#x7DB2;&#x8DEF;&#x4E0A;&#x5404;&#x7A2E;&#x8CC7;&#x6E90;&#x91CD;&#x65B0;&#x4EE5;&#x81EA;&#x5DF1;&#x65B9;&#x5F0F;&#x7FFB;&#x8B6F;&#x548C;&#x8A6E;&#x91CB;&#xFF0C;&#x751A;&#x81F3;&#x597D;&#x5E7E;&#x7BC7;&#x7684;&#x7BC4;&#x4F8B;&#x5B8C;&#x5168;&#x662F;&#x6211;&#x81EA;&#x5DF1;&#x5BEB;&#x7684;&#xFF0C;&#x4E0D;&#x6562;&#x8AAA;&#x6709;&#x591A;&#x597D;&#xFF0C;&#x56E0;&#x70BA;&#x6253;&#x6587;&#x7AE0;&#x7684;&#x76EE;&#x7684;&#x662F;&#x8B93;&#x81EA;&#x5DF1;&#x5438;&#x6536;&#xFF0C;&#x800C;&#x4E0D;&#x662F;&#x5B8C;&#x5168;&#x4EE5;&#x6559;&#x5B78;&#x7684;&#x76EE;&#x7684;&#x800C;&#x5BEB;&#xFF0C;&#x56E0;&#x6B64;&#x5F88;&#x591A;&#x5167;&#x5BB9;&#x4E26;&#x4E0D;&#x662F;&#x5F88;&#x6F02;&#x4EAE;&#xFF0C;&#x4F46;&#x662F;&#x4ECD;&#x5C0D;&#x5176;&#x4ED6;&#x4EBA;&#x6709;&#x53C3;&#x8003;&#x50F9;&#x503C;&#x3002;&#x4E09;&#x5341;&#x5929;&#x7684;&#x6587;&#x7AE0;&#x4E5F;&#x4E0D;&#x662F;&#x7167;&#x9806;&#x5E8F;&#x8B80;&#x6700;&#x597D;&#xFF0C;&#x56E0;&#x70BA;&#x6211;&#x5728;&#x5BEB;&#x7684;&#x6642;&#x5019;&#x4E26;&#x6C92;&#x6709;&#x4E00;&#x5957;&#x5B8C;&#x6574;&#x7684;&#x67B6;&#x69CB;&#xFF0C;&#x800C;&#x662F;&#x4E00;&#x500B;&#x55AE;&#x5143;&#x4E00;&#x500B;&#x55AE;&#x5143;&#x7684;&#x4ECB;&#x7D39;&#x3002;</p>
<p>&#x4E00;&#x500B;&#x6708;&#x904E;&#x53BB;&#x4E86;&#xFF0C;&#x5373;&#x4F7F;&#x6211;&#x6C92;&#x6709;&#x4E00;&#x500B;&#x53EF;&#x4EE5;&#x7167;&#x9806;&#x5E8F;&#x5B78;&#x7FD2;&#x7684;&#x6B65;&#x9A5F;&#xFF0C;&#x6771;&#x6E4A;&#x897F;&#x6E4A;&#x4E5F;&#x62DA;&#x51FA;&#x5E7E;&#x4E4E;&#x5B8C;&#x6574;&#x7684; Angular 2 &#x5730;&#x5716;&#xFF0C;&#x5927;&#x90E8;&#x5206;&#x7684;&#x6587;&#x737B;&#x5167;&#x5BB9;&#x90FD;&#x8B80;&#x904E;&#x4E86;&#x3002;&#x7DB2;&#x8DEF;&#x4E0A;&#x6709;&#x95DC; Angular 2 &#x7684;&#x6280;&#x8853;&#x6587;&#x7AE0;&#x5176;&#x5BE6;&#x4E5F;&#x6C92;&#x6709;&#x5F88;&#x591A;&#xFF0C;&#x5373;&#x4F7F;&#x82F1;&#x6587;&#x4E5F;&#x4E00;&#x6A23;&#xFF0C;&#x6240;&#x8B02;&#x4E0D;&#x591A;&#x662F;&#x6307;&#x591A;&#x6A23;&#x6027;&#xFF0C;&#x4ECB;&#x7D39;&#x57FA;&#x790E;&#x7684;&#x5167;&#x5BB9;&#x6587;&#x7AE0;&#x975E;&#x5E38;&#x591A;&#xFF0C;&#x4F46;&#x90FD;&#x5728;&#x8B1B;&#x540C;&#x4E00;&#x4EF6;&#x4E8B;&#xFF0C;&#x6211;&#x5E0C;&#x671B;&#x770B;&#x5230;&#x7684;&#x662F;&#x591A;&#x5143;&#x5167;&#x5BB9;&#xFF0C;&#x4F46;&#x5176;&#x5BE6;&#x80FD;&#x8B1B;&#x7684;&#x4E5F;&#x5C31;&#x90A3;&#x4E9B;&#x3002;Angular 2 &#x8AAA;&#x7A7F;&#x4E86;&#x53EA;&#x662F;&#x4E00;&#x500B;&#x5F37;&#x5927;&#x7684;&#x6846;&#x67B6;&#xFF0C;&#x6700;&#x91CD;&#x8981;&#x7684;&#x4E0D;&#x662F;&#x628A;&#x64CD;&#x4F5C;&#x5B83;&#x7684;&#x6280;&#x8853;&#x5B78;&#x7684;&#x591A;&#x53B2;&#x5BB3;&#xFF0C;&#x800C;&#x662F;&#x61C2;&#x5F97;&#x4F7F;&#x7528;&#x4ED6;&#xFF0C;&#x7136;&#x5F8C;&#x5275;&#x9020;&#x5C6C;&#x65BC;&#x81EA;&#x5DF1;&#x7684;&#x50F9;&#x503C;&#x3002;</p>
<h2>&#x5B78;&#x7FD2;&#x9806;&#x5E8F;</h2>
<p>&#x6211;&#x7576;&#x521D;&#x5165;&#x9580;&#x6642;&#xFF0C;&#x7DB2;&#x8DEF;&#x4E0A;&#x5F88;&#x591A;&#x57FA;&#x790E;&#x6559;&#x5B78;&#xFF0C;&#x4F46;&#x770B;&#x5B8C;&#x4ECD;&#x662F;&#x4E00;&#x77E5;&#x534A;&#x89E3;&#xFF0C;&#x4E5F;&#x5F88;&#x591A;&#x7D30;&#x9805;&#x7684;&#x6280;&#x8853;&#x6587;&#xFF0C;&#x751A;&#x81F3;&#x770B;&#x5B98;&#x65B9;&#x6587;&#x4EF6;&#xFF0C;&#x770B;&#x90A3;&#x4E9B;&#x5C31;&#x50CF;&#x62FC;&#x62FC;&#x5716;&#xFF0C;&#x7576;&#x4F60;&#x5168;&#x90E8;&#x62FC;&#x5B8C;&#x4E4B;&#x5F8C;&#xFF0C;&#x5C31;&#x662F;&#x5B8C;&#x5168;&#x4E86;&#x89E3; Angular 2 &#x5728;&#x5E79;&#x561B;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x53EA;&#x662F;&#x9019;&#x6A23;&#x5B78;&#x7FD2;&#x6709;&#x9EDE;&#x50CF;&#x5728;&#x8D70;&#x8FF7;&#x5BAE;&#xFF0C;&#x6211;&#x9084;&#x662F;&#x89BA;&#x5F97;&#x80FD;&#x7167;&#x4E00;&#x500B;&#x9806;&#x5E8F;&#x5B78;&#x7FD2;&#xFF0C;&#x6703;&#x6BD4;&#x8F03;&#x6709;&#x6548;&#x7387;&#x3002;</p>
<p><strong>&#x4EE5;&#x4E0B;&#x7167;&#x9806;&#x5E8F;&#xFF0C;&#x662F;&#x6211;&#x8A8D;&#x70BA;&#x5B78;&#x597D; Angular 2 &#x7684;&#x6700;&#x4F73;&#x65B9;&#x5F0F;&#xFF0C;&#x6709;&#x6A19;&#x793A;&#x300C;Day XX&#x300D;&#x7684;&#x5C31;&#x662F;&#x672C;&#x7CFB;&#x5217; <a href="https://ithelp.ithome.com.tw/users/20103745/ironman/1160" target="_blank">Angular 2 &#x4E4B; 30 &#x5929;&#x9081;&#x5411;&#x795E;&#x4E4E;&#x5176;&#x6280;&#x4E4B;&#x8DEF;</a> &#x7684;&#x6587;&#x7AE0;&#x3002;</strong></p>
<p><strong>&#x5728;&#x958B;&#x59CB;&#x4E4B;&#x524D;</strong></p>
<ul>
<li>&#x57FA;&#x790E;&#x77E5;&#x8B58;<br>
&#x57FA;&#x672C;&#x7684;&#x7DB2;&#x9801;&#x77E5;&#x8B58;&#x548C;&#x64CD;&#x4F5C;&#x5148;&#x6709;&#x4E00;&#x5B9A;&#x6C34;&#x6E96;&#xFF0C;&#x4E5F;&#x5C31;&#x662F; html, js, css &#x719F;&#x6089;&#x4E4B;&#x5F8C;&#x518D;&#x63A5;&#x89F8;&#x6846;&#x67B6;&#x3002;</li>
<li>&#x7269;&#x4EF6;&#x5C0E;&#x5411;<br>
&#x7DB2;&#x9801;&#x7A0B;&#x5F0F;&#x672C;&#x8EAB;&#x5C31;&#x662F;&#x4E00;&#x500B;&#x975E;&#x5E38;&#x7269;&#x4EF6;&#x5C0E;&#x5411;&#x7684;&#x64CD;&#x4F5C;&#xFF0C;&#x5C0D;&#x65BC;&#x7269;&#x4EF6;&#x5C0E;&#x5411;&#x6709;&#x591A;&#x4E00;&#x9EDE;&#x4E86;&#x89E3;&#x5728;&#x4F86;&#x4F7F;&#x7528; Angular 2 &#x6216; React &#x9019;&#x985E;&#x4EE5;&#x7D44;&#x4EF6;&#x70BA;&#x6982;&#x5FF5;&#x7684;&#x6846;&#x67B6;&#x6703;&#x5F88;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x4E14;&#x80FD;&#x6F02;&#x4EAE;&#x4F7F;&#x7528;&#x7269;&#x4EF6;&#x5C0E;&#x5411;&#x5C0D;&#x65BC;&#x7A0B;&#x5F0F;&#x958B;&#x767C;&#x672C;&#x4F86;&#x5C31;&#x6709;&#x5F88;&#x5927;&#x5E6B;&#x52A9;&#x3002;</li>
</ul>
<p><strong>&#x958B;&#x59CB;&#x63A5;&#x89F8;</strong></p>
<ul>
<li>&#x5148;&#x6709;&#x6982;&#x5FF5;<br>
&#x81F3;&#x5C11;&#x77E5;&#x9053;&#x70BA;&#x5565;&#x8981;&#x7528; Angular 2<br>
<a href="https://ithelp.ithome.com.tw/articles/10185829" target="_blank">[Day 01] Angular 2 &#x7C21;&#x4ECB;</a><br>
<a href="https://medium.com/javascript-scene/angular-2-vs-react-the-ultimate-dance-off-60e7dfbc379c#.44o9mf7el" target="_blank">Angular 2 vs React: The Ultimate Dance Off</a>
</li>
<li>TypeScipt<br>
&#x7531;&#x65BC;&#x63A8;&#x8350;&#x662F;&#x4F7F;&#x7528; TS &#x505A;&#x958B;&#x767C;&#xFF0C;&#x61C2; TS &#x7576;&#x7136;&#x91CD;&#x8981;&#x3002;&#x56E0;&#x70BA;&#x7528;&#x6CD5;&#x8DDF; JS &#x5F88;&#x50CF;&#xFF0C;&#x5176;&#x5BE6;&#x591A;&#x770B;&#x5E7E;&#x500B;&#x7BC4;&#x4F8B;&#x5C31;&#x53EF;&#x4EE5;&#x958B;&#x59CB;&#x5BEB;&#x4E86;&#x3002;<br>
<a href="https://ithelp.ithome.com.tw/articles/10186280" target="_blank">[Day 02] TypeScript -- Angular 2 &#x7684;&#x5BEB;&#x4F5C;&#x9748;&#x9B42;</a><br>
<a href="https://www.typescriptlang.org/docs/tutorial.html" target="_blank">TypeScript &#x5B98;&#x65B9;&#x6587;&#x4EF6;</a><br>
<a href="https://www.cnblogs.com/SLchuck/p/5217622.html" target="_blank">TS &#x521D;&#x63A2;</a>
</li>
<li>Angular 2 &#x7684;&#x67B6;&#x69CB;<br>
<a href="https://ithelp.ithome.com.tw/articles/10186561" target="_blank">[Day 03] &#x7576;&#x500B;&#x597D;&#x7684;&#x5EFA;&#x7BC9;&#x5E2B;&#x4E4B; Angular 2 &#x67B6;&#x69CB;</a><br>
<a href="https://angular.io/docs/ts/latest/guide/architecture.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;: Architecture</a>
</li>
<li>&#x6CE8;&#x5165;&#x4F9D;&#x8CF4; (DI)<br>
&#x9019;&#x662F;&#x975E;&#x5E38;&#x91CD;&#x8981;&#x7684;&#x6280;&#x5DE7;&#xFF0C;Angular 2 &#x8655;&#x8655;&#x6709; DI &#x7684;&#x5F71;&#x5B50;<br>
<a href="https://ithelp.ithome.com.tw/articles/10186702" target="_blank">[Day 04] Dependency Injection In Angular 2</a><br>
<a href="https://asdfblog.com/angular2-dependency-injection.html" target="_blank">[&#x57FA;&#x790E;&#x7CFB;&#x5217;] Angular2 &#x4F9D;&#x8CF4;&#x6CE8;&#x5165;</a><br>
<a href="https://angular.io/docs/ts/latest/guide/dependency-injection.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;: DI</a>
</li>
<li>&#x5148;&#x770B;&#x770B; Angular 2 &#x5C0F;&#x7A0B;&#x5F0F;&#x5427;<br>
<a href="https://angular.io/docs/ts/latest/quickstart.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;&#xFF1A; Quick Start</a>
</li>
<li>&#x7D44;&#x4EF6; (Component)<br>
&#x7D44;&#x4EF6;&#x662F; Angular 2 &#x4E2D;&#x6700;&#x5E38;&#x7528;&#x5230;&#x7684;&#x6771;&#x897F;&#xFF0C;&#x4E5F;&#x5982;&#x540C;&#x6211;&#x7CFB;&#x5217;&#x6587;&#x7AE0;&#x63D0;&#x5230;&#x7684;&#xFF0C;&#x5979;&#x6490;&#x8D77;&#x6574;&#x500B;&#x7CFB;&#x7D71;<br>
<a href="https://learnangular2.com/components/" target="_blank">Learn Angular2: COMPONENTS</a>
</li>
<li>&#x6A21;&#x7D44; (Moudule)<br>
<a href="https://ithelp.ithome.com.tw/articles/10188095" target="_blank">[Day 15] Angular 2 Module ( 1 )</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188188" target="_blank">[Day 16] Angular 2 Module ( 2 )</a>
</li>
<li>Bootstrap<br>
&#x61C2; Module &#x548C; DI &#x662F;&#x751A;&#x9EBC;&#x4E4B;&#x5F8C;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x4E86;&#x89E3; Bootstrap (&#x555F;&#x52D5;) &#x662F;&#x5565;&#x73A9;&#x610F;<br>
<a href="https://angular.io/docs/ts/latest/guide/appmodule.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;&#xFF1A;THE ROOT MODULE</a>
</li>
<li>&#x6A21;&#x677F; (Template) &#x8207;&#x7D81;&#x5B9A; (Binding)<br>
<a href="https://ithelp.ithome.com.tw/articles/10186854" target="_blank">[Day 05] Angular2 &#x6A21;&#x677F;&#x8207;&#x7D81;&#x5B9A;&#xFF0D;&#xFF0D;&#x4E92;&#x52D5;&#x7684;&#x6839;&#x672C;</a><br>
<a href="https://angular.io/docs/ts/latest/guide/template-syntax.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;&#xFF1A; Template</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188383" target="_blank">[Day 19] Angular 2 Input(s) &amp; Output(s) &#x50BB;&#x50BB;&#x5206;&#x4E0D;&#x6E05;</a>
</li>
<li>&#x6A21;&#x677F;&#x5167;&#x5BB9;<br>
<a href="https://ithelp.ithome.com.tw/articles/10187991" target="_blank">[Day 14] Angular 2 + <code>&lt;ng-content&gt;</code> &#x5D4C;&#x5165;&#x5F0F;&#x8A2D;&#x8A08;&#x9748;&#x6D3B;&#x7D44;&#x7E54; HTML</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188796" target="_blank">[Day 26] Angular 2 &#x88DD;&#x98FE;&#x5668; @ContentChild</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188861" target="_blank">[Day 27] Angular 2 &#x88DD;&#x98FE;&#x5668; @ViewChild</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188912" target="_blank">[Day 28] Angular 2 &#x88FD;&#x4F5C; tab &#x5143;&#x4EF6;</a>
</li>
<li>Pipe<br>
<a href="https://ithelp.ithome.com.tw/articles/10187136" target="_blank">[Day 07] Angular 2 PIPES(&#x901A;&#x9053;)</a><br>
<a href="https://angular.io/docs/ts/latest/guide/pipes.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;&#xFF1A;Pipe</a>
</li>
<li>&#x8DEF;&#x7531; (Routing)<br>
<a href="https://ithelp.ithome.com.tw/articles/10186854" target="_blank">[Day 09] Angular 2 &#x8DEF;&#x7531;</a><br>
<a href="https://angular.io/docs/ts/latest/tutorial/toh-pt5.html" target="_blank">Angular &#x5B98;&#x65B9;&#x6587;&#x4EF6;&#xFF1A;Routing</a>
</li>
</ul>
<p><strong>&#x9032;&#x968E;&#x5B78;&#x7FD2;</strong><br>
<a href="https://ithelp.ithome.com.tw/articles/10188984" target="_blank">[Day 29] Angular 2 @Directive</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10187525" target="_blank">[Day 10] Angular 2 &#x52D5;&#x756B; (ANIMATIONS)</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188218" target="_blank">[Day 17] Angular 2 &#x66FF; Component &#x52A0;&#x4E0A; CSS &#x7684;&#x6240;&#x6709;&#x62DB;&#x6578;</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188252" target="_blank">[Day 18] Angular 2 &#x7D44;&#x4EF6;&#x7E7C;&#x627F; ( Component Inheritance )</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188399" target="_blank">[Day 20] Angular 2 &#x7D44;&#x4EF6;&#x76F8;&#x95DC;&#x7684;&#x8DEF;&#x5F91;</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188737" target="_blank">[Day 25] Angular 2 &#x4E8B;&#x5148;&#x7DE8;&#x8B6F; Ahead-of-Time (AoT)</a></p>
<p><strong>&#x5BE6;&#x969B;&#x61C9;&#x7528;</strong><br>
<a href="https://ithelp.ithome.com.tw/articles/10190065" target="_blank">&#x5982;&#x4F55;&#x5728; Angular 4 &#x4E2D;&#x52A0;&#x5165; jQuery</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10187011" target="_blank">[Day 06] Angular 2 &#x8868;&#x55AE;</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10187773" target="_blank">[Day 12] Angular 2 &#x591A;&#x8A9E;&#x8A00; ( 1 )</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10187865" target="_blank">[Day 13] Angular 2 &#x591A;&#x8A9E;&#x8A00; ( 2 )</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10187601" target="_blank">[Day 11] Angular 2 HTTP &#x65B9;&#x6CD5;&#xFF0D;&#xFF0D;&#x8B93;&#x6211; Call API</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10187200" target="_blank">[Day 08] Angular 2 Lazy Loading &#x5225;&#x8B93;&#x8F09;&#x5165;&#x901F;&#x5EA6;&#x62D6;&#x57AE;&#x4F60;&#xFF01;</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10189022" target="_blank">[Day 30] Angular 2 &#x55AE;&#x5143;&#x6E2C;&#x8A66; Unit Test</a></p>
<p><strong>&#x88FD;&#x4F5C; APP</strong><br>
<a href="https://ithelp.ithome.com.tw/articles/10188464" target="_blank">[Day 21] Angular 2 + Ionic = Mobile App ( 1 ) &#x4ECB;&#x7D39;</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188551" target="_blank">[Day 22] Angular 2 + Ionic = Mobile App ( 2 ) &#x5EFA;&#x69CB;</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188566" target="_blank">[Day 23] Angular 2 + Ionic = Mobile App ( 3 ) &#x5BE6;&#x4F5C; Todo List</a><br>
<a href="https://ithelp.ithome.com.tw/articles/10188678" target="_blank">[Day 24] Angular 2 + Ionic = Mobile App ( 4 ) &#x767C;&#x5E03; App</a></p>
<hr>
<p>&#x672C;&#x7CFB;&#x5217;&#x4E5F;&#x544A;&#x4E00;&#x6BB5;&#x843D;&#xFF0C;&#x4E0D;&#x80FD;&#x8AAA;&#x5B8C;&#x7F8E;&#xFF0C;&#x4F46;&#x81F3;&#x5C11;&#x4E5F;&#x6EFF;&#x5B8C;&#x6574;&#xFF0C;&#x5E0C;&#x671B;&#x5C0D;&#x6240;&#x6709;&#x50CF;&#x6211;&#x4E00;&#x6A23;&#x521D;&#x5B78; Angular 2 &#x7684;&#x5DE5;&#x7A0B;&#x5E2B;&#x6709;&#x6240;&#x5E6B;&#x52A9;&#xFF0C;&#x6709;&#x4EFB;&#x4F55;&#x554F;&#x984C;&#x4E5F;&#x6B61;&#x8FCE;&#x4F86;&#x4FE1;&#xFF0C;&#x6211;&#x5011;&#x672A;&#x4F86;&#x518D;&#x898B;&#xFF01;</p>
<hr>
<blockquote>
<p><em><strong>&#x95DC;&#x65BC;&#x4F5C;&#x8005;</strong></em><br>
<strong>&#x5289;&#x5B89;&#x9F4A;</strong><br>
&#x8EDF;&#x9AD4;&#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x71B1;&#x611B;&#x5BEB;&#x7A0B;&#x5F0F;&#xFF0C;&#x66F4;&#x559C;&#x6B61;&#x63A8;&#x5EE3;&#x7A0B;&#x5F0F;&#x8B93;&#x66F4;&#x591A;&#x4EBA;&#x5B78;&#x6703;&#x3002;&#x6B61;&#x8FCE;&#x8FFD;&#x8E64; <a href="https://www.facebook.com/CodingNeutrino/" target="_blank">&#x5FAE;&#x4E2D;&#x5B50;</a>&#xFF0C;&#x6211;&#x6703;&#x5728;&#x4E0A;&#x9762;&#x5206;&#x4EAB;&#x5404;&#x7A2E;&#x65B0;&#x77E5;&#x8207;&#x6700;&#x65B0;&#x4F5C;&#x54C1;&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x53BB;&#x901B;&#x901B;&#x6211;&#x7684; <a href="https://tigercosmos.xyz/" target="_blank">&#x500B;&#x4EBA;&#x7DB2;&#x7AD9;</a> &#x6216; <a href="https://github.com/tigercosmos/" target="_blank">Github</a>&#x3002;</p>
</blockquote>
 <br>
                                                    </div>
                    </div>
                
