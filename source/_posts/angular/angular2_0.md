---
title: Angular 2 簡介
date: 2016-12-16 23:53:12
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<p><img src="https://udemy-images.udemy.com/course/750x422/500628_a962.jpg" alt></p>
<h2>&#x524D;&#x8A00;</h2>
<p>&#x6211;&#x76EE;&#x524D;&#x4ECD;&#x5728;&#x5C31;&#x5B78;&#xFF0C;&#x6BCF;&#x5468;&#x4E5F;&#x56FA;&#x5B9A;&#x82B1;&#x4E00;&#x4E9B;&#x6642;&#x9593;&#x53BB;&#x516C;&#x53F8;&#x5BE6;&#x7FD2;&#xFF0C;&#x800C;&#x4E14;&#x4E5F;&#x662F;&#x8FD1;&#x671F;&#x7684;&#x4E8B;&#x3002;&#x7576;&#x521D;&#x9762;&#x8A66;&#x7684;&#x6642;&#x5019;&#x662F;&#x4EE5;&#x524D;&#x7AEF;&#x3001;&#x5F8C;&#x7AEF;&#x90FD;&#x53EF;&#x4EE5;&#x7684;&#x8EAB;&#x5206;&#x53BB;&#xFF0C;&#x5C55;&#x793A;&#x4E86;&#x5E7E;&#x4EF6;&#x4F5C;&#x54C1;&#x4E4B;&#x5F8C;&#x516C;&#x53F8;&#x4E5F;&#x6C7A;&#x5B9A;&#x8058;&#x50F1;&#x6211;&#xFF0C;&#x516C;&#x53F8;&#x6700;&#x7D42;&#x6307;&#x6D3E;&#x6211;&#x505A;&#x524D;&#x7AEF;&#xFF0C;&#x76EE;&#x524D;&#x4E5F;&#x5E7E;&#x4E4E;&#x90FD;&#x5728;&#x8655;&#x7406;&#x524D;&#x7AEF;&#xFF0C;&#x6709;&#x6642;&#x5019;&#x5F8C;&#x7AEF;&#x7684;&#x4EBA;&#x5FD9;&#x4E0D;&#x904E;&#x4F86;&#x4E5F;&#x6703;&#x81EA;&#x5DF1;&#x5F04;&#x500B;&#x5F8C;&#x7AEF;&#x81E8;&#x6642;&#x61C9;&#x4ED8;&#x4E00;&#x4E0B;&#x3002;&#x516C;&#x53F8;&#x524D;&#x7AEF;&#x63A1;&#x7528; Angular 2 &#x6846;&#x67B6;&#xFF0C;&#x5C0D;&#x6211;&#x800C;&#x8A00;&#x662F;&#x975E;&#x5E38;&#x964C;&#x751F;&#x7684;&#xFF0C;&#x5728;&#x4E4B;&#x524D;&#x66FE;&#x7528;&#x904E; AngularJs &#x958B;&#x767C;&#x904E; Cordova Ionic&#xFF0C;&#x4E0D;&#x904E;&#x9084;&#x662F;&#x7FD2;&#x6163;&#x5BEB;&#x7D14; JS&#xFF0C;&#x6846;&#x67B6;&#x7684;&#x90E8;&#x5206;&#x90FD;&#x662F;&#x907F;&#x91CD;&#x5C31;&#x8F15;&#xFF0C;&#x4F3C;&#x4E4E;&#x53CD;&#x800C;&#x55AA;&#x5931;&#x6846;&#x67B6;&#x7684;&#x610F;&#x7FA9;&#x5462;&#x3002;&#x800C;&#x65E2;&#x7136;&#x9032;&#x516C;&#x53F8;&#x8981;&#x4F7F;&#x7528; Angular 2&#xFF0C;&#x7D22;&#x6027;&#x5C31;&#x628A;&#x9019;&#x500B;&#x6846;&#x67B6;&#x5FB9;&#x5E95;&#x5F04;&#x61C2;&#xFF0C;&#x5F9E;&#x61F5;&#x61F5;&#x61C2;&#x61C2;&#x9081;&#x5411;&#x795E;&#x4E4E;&#x5176;&#x6280;&#xFF01;</p>
<h2>Why Angular 2?</h2>
<p>&#x4ECA;&#x65E5;&#x524D;&#x7AEF; (front-end) &#x6846;&#x67B6;&#x7FA4;&#x96C4;&#x722D;&#x9738;&#xFF0C;&#x6BCF;&#x500B;&#x90FD;&#x6709;&#x81EA;&#x5DF1;&#x7684;&#x7279;&#x9EDE;&#xFF0C;Angular 2&#x3001;React&#x3001;Ember&#x3001;Vue &#x7B49;&#x7B49;&#xFF0C;Angular 2 &#x6709;&#x751A;&#x9EBC;&#x512A;&#x9EDE;&#x8B93;&#x5927;&#x5BB6;&#x9078;&#x64C7;&#x5B83;&#x5462;&#xFF1F;</p>
<blockquote>
<p>Angular2 &#x4E3B;&#x8981;&#x76EE;&#x7684;&#x662F;&#x70BA;&#x4E86;&#x6253;&#x9020;&#x4E00;&#x500B;&#x66F4;&#x7C21;&#x55AE;&#x958B;&#x767C;&#x7684; Web &#x6846;&#x67B6;&#xFF0C;&#x958B;&#x767C;&#x5718;&#x968A;&#x6DF1;&#x4FE1;&#x5BEB;&#x51FA;&#x6F02;&#x4EAE;&#x7684;&#x61C9;&#x7528;&#x662F;&#x6703;&#x8B93;&#x4EBA;&#x611F;&#x89BA;&#x5FEB;&#x6A02;&#x8207;&#x6709;&#x8DA3;</p>
</blockquote>
<h3>What</h3>
<p>&#x5148;&#x8AAA;&#x8AAA;&#x751A;&#x9EBC;&#x662F; Angular 2&#xFF0C;&#x5B83;&#x662F; Google&#x958B;&#x767C;&#x51FA;&#x4F86;&#x4E00;&#x6B3E;&#x958B;&#x6E90; JavaScript&#x6846;&#x67B6;&#xFF0C;&#x7528;&#x4F86;&#x5354;&#x52A9;&#x55AE;&#x4E00;&#x9801;&#x9762;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x904B;&#x884C;&#x7684;&#x3002;&#x5B83;&#x7684;&#x76EE;&#x6A19;&#x662F;&#x900F;&#x904E; MVC&#x6A21;&#x5F0F;&#xFF08;MVC&#xFF09;&#x529F;&#x80FD;&#x589E;&#x5F37;&#x700F;&#x89BD;&#x5668;&#x7684;&#x61C9;&#x7528;&#xFF0C;&#x4F7F;&#x958B;&#x767C;&#x548C;&#x6E2C;&#x8A66;&#x8B8A;&#x5F97;&#x66F4;&#x52A0;&#x5BB9;&#x6613;&#x3002;</p>
<h3>ALL-IN-ONE</h3>
<p>Angular &#x662F;&#x4E00;&#x500B; &#x201C;ALL-IN-ONE&#x201D; &#x7684;&#x6846;&#x67B6;&#xFF0C;&#x9019;&#x5C31;&#x610F;&#x5473;&#x8457;&#x4F60;&#x53EA;&#x8981;&#x638C;&#x63E1;&#x4E86; Angular &#x5C31;&#x53EF;&#x4EE5;&#x5B8C;&#x6210;&#x5927;&#x91CF;&#x7684;&#x524D;&#x7AEF;&#x5DE5;&#x4F5C;&#x4E86;&#x3002;&#x4E0D;&#x7BA1;&#x662F; 1&#x9084;&#x662F; 2&#xFF0C;Angular&#x6700;&#x986F;&#x8457;&#x7684;&#x7279;&#x5FB5;&#x5C31;&#x662F;&#x5176;&#x6574;&#x5408;&#x6027;&#x3002;&#x4E00;&#x9AD4;&#x5316;&#x6846;&#x67B6;&#x6DB5;&#x84CB;&#x4E86;M&#x3001;V&#x3001;C/VM&#x7B49;&#x5404;&#x500B;&#x5C64;&#x9762;&#xFF0C;&#x4E0D;&#x9700;&#x8981;&#x7D44;&#x5408;&#x3001;&#x8A55;&#x4F30;&#x5176;&#x5B83;&#x6280;&#x8853;&#x5C31;&#x80FD;&#x5B8C;&#x6210;&#x5927;&#x90E8;&#x5206;&#x524D;&#x7AEF;&#x958B;&#x767C;&#x4EFB;&#x52D9;&#x3002;&#x9019;&#x9996;&#x5148;&#x5F97;&#x76CA;&#x65BC;&#x5B83;&#x5C0D;&#x5404;&#x7A2E;&#x6280;&#x8853;&#x7684;&#x5C01;&#x88DD;&#xFF0C;&#x8B93;&#x4F60;&#x4E0D;&#x7528;&#x95DC;&#x5FC3;&#x5B83;&#x7684;&#x5BE6;&#x73FE;&#x7D30;&#x7BC0;&#x3002;Angular&#x9694;&#x96E2;&#x4E86;&#x700F;&#x89BD;&#x5668;&#x7684;&#x7D30;&#x7BC0;&#xFF0C;&#x5927;&#x591A;&#x6578;&#x5DE5;&#x4F5C;&#x4F60;&#x751A;&#x81F3;&#x90FD;&#x4E0D;&#x9700;&#x8981;&#x77E5;&#x9053; DOM&#x7B49;&#x524D;&#x7AEF;&#x77E5;&#x8B58;&#x5C31;&#x53EF;&#x4EE5;&#x5B8C;&#x6210;&#x3002;&#x9019;&#x6A23;&#x53EF;&#x4EE5;&#x6709;&#x6548;&#x964D;&#x4F4E;&#x6C7A;&#x7B56;&#x6210;&#x672C;&#xFF0C;&#x63D0;&#x9AD8;&#x958B;&#x767C;&#x901F;&#x5EA6;&#xFF0C;&#x5C0D;&#x9700;&#x8981;&#x5FEB;&#x901F;&#x8D77;&#x6B65;&#x7684;&#x5718;&#x968A;&#x662F;&#x975E;&#x5E38;&#x6709;&#x5E6B;&#x52A9;&#x7684;&#x3002;</p>
<h3>TypeScript</h3>
<p>Angular&#x9078;&#x64C7;&#x4E86; TypeScript&#x4F5C;&#x70BA;&#x4E3B;&#x8A9E;&#x8A00;&#x3002;&#x7C21;&#x55AE;&#x4F86;&#x8AAA; TypeScript&#x53EF;&#x4EE5;&#x8AAA;&#x662F; Super&#x7248;&#x7684; JavaScript&#xFF0C;&#x76EE;&#x7684;&#x662F;&#x6539;&#x7528;&#x4E00;&#x4E9B;&#x7D50;&#x69CB;&#x826F;&#x597D;&#x6216;&#x662F;&#x66F4;&#x8F15;&#x9B06;&#x7684;&#x8A9E;&#x8A00;&#x4F86;&#x958B;&#x767C;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#xFF0C;&#x958B;&#x767C;&#x5B8C;&#x5F8C;&#x518D;&#x7DE8;&#x8B6F;&#x56DE; JavaScript&#xFF0C;&#x66F4;&#x91CD;&#x8981;&#x7684;&#x662F; TypeScript&#x5B8C;&#x5168;&#x76F8;&#x5BB9; JavaScript&#x3002;&#x5982;&#x679C;&#x4F60;&#x662F;&#x500B; C#&#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x4E00;&#x5B9A;&#x6703;&#x5C0D;&#x5B83;&#x7684;&#x8A9E;&#x6CD5;&#x611F;&#x89BA;&#x4F3C;&#x66FE;&#x76F8;&#x8B58;&#x3002;TypeScript&#x3001;C#&#x3001;Delphi&#x90FD;&#x662F;&#x50B3;&#x5947;&#x4EBA;&#x7269; Anders Hejlsberg&#x5275;&#x5EFA;&#x3002;&#x5F37;&#x985E;&#x578B;&#x3001;&#x985E;&#x3001;&#x63A5;&#x53E3;&#x3001;&#x8A3B;&#x89E3;&#x7B49;&#x7B49;&#x3002;&#x7A0B;&#x5F0F;&#x8A9E;&#x8A00;&#x9818;&#x57DF;&#x8015;&#x8018;&#x591A;&#x5E74;&#x7684; Anders&#x592A;&#x719F;&#x6089;&#x512A;&#x79C0;&#x8A9E;&#x8A00;&#x7684;&#x5171;&#x6027;&#x4E86;&#xFF0C;&#x4ED6;&#x6240;&#x505A;&#x7684;&#x53D6;&#x6368;&#x503C;&#x5F97;&#x4F60;&#x4FE1;&#x8CF4;&#x3002;</p>
<h3>&#x4F9D;&#x8CF4;&#x6CE8;&#x5165;</h3>
<p>Angular&#x5728;&#x524D;&#x7AEF;&#x5BE6;&#x73FE;&#x4E86;&#x670D;&#x52D9;&#x8207;&#x4F9D;&#x8CF4;&#x6CE8;&#x5165;&#x7684;&#x6982;&#x5FF5;&#x3002;&#x4F9D;&#x8CF4;&#x6CE8;&#x5165;&#x7684;&#x89C0;&#x5FF5;&#x5C31;&#x662F;&#x5C07;&#x6240;&#x6709;&#x6771;&#x897F;&#x5148;&#x5728;&#x300C;&#x5916;&#x9762;&#x300D;&#x6E96;&#x5099;&#x597D;&#xFF0C;&#x7136;&#x5F8C;&#x518D;&#x5E36;&#x5165;&#x300C;&#x5167;&#x90E8;&#x300D;&#x7684;&#x7A0B;&#x5F0F;&#x4E2D;&#xFF0C;&#x5982;&#x6B64;&#x4E00;&#x4F86;&#x4F60;&#x5C31;&#x80FD;&#x5920;&#x5728;&#x6AA2;&#x8996;&#x7A0B;&#x5F0F;&#x78BC;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x4E00;&#x76EE;&#x4E86;&#x7136;&#x5730;&#x77E5;&#x9053;&#x9019;&#x500B;&#x7A0B;&#x5F0F;&#x4F9D;&#x8CF4;&#x8457;&#x54EA;&#x4E9B;&#x985E;&#x5225;&#x3002;</p>
<h3>&#x5718;&#x968A;&#x5408;&#x4F5C;</h3>
<p>Angular&#x5C0D;&#x5718;&#x968A;&#x4F5C;&#x6230;&#x63D0;&#x4F9B;&#x4E86;&#x826F;&#x597D;&#x7684;&#x652F;&#x6301;&#xFF0C;&#x6BD4;&#x5982;&#x6A21;&#x677F;&#x8207;&#x7A0B;&#x5F0F;&#x78BC;&#x7684;&#x5206;&#x96E2;&#x3001;&#x6A23;&#x5F0F;&#x8868;&#x7684;&#x5C40;&#x90E8;&#x5316;&#x3001;&#x7D44;&#x4EF6;&#x5316;&#x7684;&#x8A2D;&#x8A08;&#x3001;&#x670D;&#x52D9;&#x8207;&#x4F9D;&#x8CF4;&#x6CE8;&#x5165;&#x9AD4;&#x4FC2;&#x7B49;&#x3002;&#x9019;&#x4E9B;&#x7279;&#x6027;&#x8B93;&#x5DE5;&#x7A0B;&#x5E2B;&#x53EF;&#x4EE5;&#x5148;&#x5C08;&#x6CE8;&#x65BC;&#x53EF;&#x4EE5;&#x5148;&#x8655;&#x7406;&#x6A21;&#x578B;&#x3001;&#x4EA4;&#x4E92;&#x908F;&#x8F2F;&#x3001;&#x6A23;&#x5F0F;&#x3001;&#x6A21;&#x677F;&#x7B49;&#x7B49;&#x6280;&#x8853;&#x4E2D;&#x81EA;&#x5DF1;&#x64C5;&#x9577;&#x7684;&#x90E8;&#x4EFD;&#xFF0C;&#x81EA;&#x5DF1;&#x4E0D;&#x64C5;&#x9577;&#x7684;&#x90E8;&#x5206;&#x5247;&#x4EA4;&#x7D66;&#x968A;&#x53CB;&#x3002;</p>
<h2>&#x666E;&#x904D;&#x6027;</h2>
<p>Angular &#x56E0;&#x70BA;&#x5B83;&#x7684;&#x760B;&#x72C2;&#x53D7;&#x6B61;&#x8FCE;&#x7684;&#x7A0B;&#x5EA6;&#xFF0C;&#x67D0;&#x7A2E;&#x7A0B;&#x5EA6;&#x53EF;&#x4EE5;&#x7576;&#x4F5C;&#x662F;&#x4E3B;&#x6D41;&#xFF0C;&#x4E0D;&#x7BA1;&#x5B83;&#x5BE6;&#x969B;&#x4E0A;&#x5230;&#x5E95;&#x597D;&#x4E0D;&#x597D;&#xFF0C;&#x610F;&#x7FA9;&#x5C31;&#x5982;&#x540C;&#x6587;&#x66F8;&#x8EDF;&#x9AD4;&#x6709;&#x5F88;&#x591A;&#x7A2E;&#xFF0C;&#x4F46;&#x662F; Microsoft Offices&#x662F;&#x4E3B;&#x6D41;&#x3002;&#x6240;&#x4EE5;&#x5982;&#x679C;&#x6703; Angular&#x653E;&#x5728;&#x4F60;&#x7684;&#x5C65;&#x6B77;&#x4E0A;&#x6703;&#x5F88;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x5C31;&#x5982;&#x540C;&#x6211;&#x53BB;&#x516C;&#x53F8;&#x767C;&#x73FE;&#x898F;&#x5B9A;&#x8981;&#x4F7F;&#x7528; Angular&#x4E00;&#x6A23;&#x3002;<br>
&#x5F9E; Google Trends&#x4E5F;&#x53EF;&#x4EE5;&#x770B;&#x5230; Angular&#x5728;&#x5E02;&#x5834;&#x4E2D;&#x7D55;&#x5C0D;&#x7684;&#x5B9A;&#x4F4D;&#x3002;<br>
<img src="https://cdn-images-1.medium.com/max/800/1*5Mg5X-7ZuWh_mnhj16WZzQ.png" alt></p>
<h2>Angular 2 &#x4E3B;&#x8981;&#x6539;&#x8B8A;</h2>
<ul>
<li>&#x5F37;&#x5316;&#x6A21;&#x7D44;&#x5316;&#x6280;&#x8853;
<ul>
<li>&#x5BE6;&#x8E10;<a href="https://zh.wikipedia.org/wiki/%E5%BC%80%E9%97%AD%E5%8E%9F%E5%88%99" target="_blank">&#x958B;&#x9589;&#x539F;&#x5247;</a>&#x8207;<a href="https://zh.wikipedia.org/wiki/%E5%85%B3%E6%B3%A8%E7%82%B9%E5%88%86%E7%A6%BB" target="_blank">&#x95DC;&#x6CE8;&#x9EDE;&#x5206;&#x96E2;</a> &#x5169;&#x500B;&#x539F;&#x5247;</li>
<li>&#x66F4;&#x5BB9;&#x6613;&#x4F7F;&#x7528;&#x7B2C;&#x4E09;&#x65B9;&#x6846;&#x67B6;&#xFF0C;&#x5982; RxJS&#x3001;ImmutableJS&#x3001;CSS Module &#x7B49;</li>
</ul>
</li>
<li>&#x66F4;&#x597D;&#x7684;&#x6548;&#x80FD;</li>
<li>&#x5C0D;&#x672B;&#x4F86;&#x6A19;&#x6E96;&#x7684;&#x53CB;&#x597D;
<ul>
<li>&#x63A1;&#x7528; Web Worker&#x3001;Web Components&#x3001;CSS Scoping</li>
</ul>
</li>
<li>&#x8DE8;&#x5E73;&#x81FA;&#x7684;&#x652F;&#x63F4;
<ul>
<li>&#x9664;&#x4E86; Web &#x5916;&#xFF0C;&#x9084;&#x652F;&#x63F4;&#x624B;&#x6A5F; App &#x8207;&#x684C;&#x6A5F; App</li>
</ul>
</li>
</ul>
 <br>
                                                    </div>
                    </div>
                