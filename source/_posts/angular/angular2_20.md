---
title: Angular 2 + Ionic = Mobile App ( 1 ) 介紹
date: 2017-01-05 23:52:38
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x6211;&#x662F;&#x4E00;&#x500B;&#x524D;&#x7AEF; (&#x4E5F;&#x8A31;&#x5168;&#x7AEF;) &#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x597D;&#x4E0D;&#x5BB9;&#x6613;&#x5B78;&#x6703;&#x5BEB; Angular 2 &#x4E86;&#x8036;&#xFF0C;&#x4F46;&#x96E3;&#x9053;&#x6211;&#x5C31;&#x4E00;&#x8F29;&#x5B50;&#x53EA;&#x80FD;&#x5BEB;&#x7DB2;&#x7AD9;&#x55CE;&#xFF1F;QQ &#x5982;&#x679C;&#x60F3;&#x8981;&#x5BEB;&#x624B;&#x6A5F;&#x7684; App&#xFF0C;&#x9084;&#x8981;&#x518D;&#x53BB;&#x5B78; Java &#x5BEB; Android App&#xFF0C;&#x53BB;&#x5B78; Swift &#x4F86;&#x5BEB; IOS App&#xFF0C;&#x9019;&#x6A23;&#x96D6;&#x7136;&#x4E5F;&#x4E0D;&#x662F;&#x4E0D;&#x53EF;&#x4EE5;&#xFF0C;&#x4F46;&#x662F;&#x6BCF;&#x5B78;&#x4E00;&#x500B;&#x6280;&#x8853;&#x5C31;&#x8981;&#x7D93;&#x6B77;&#x4E00;&#x500B;&#x5B78;&#x7FD2;&#x66F2;&#x7DDA;&#xFF0C;&#x591A;&#x75DB;&#x82E6;&#x554A;&#xFF01;&#xFF01;</p>
<p>&#x7576;&#x7136;&#x65E2;&#x7136;&#x662F;&#x524D;&#x7AEF;&#x5DE5;&#x7A0B;&#x5E2B;&#x5BEB;&#x500B; Web App &#x96E3;&#x4E0D;&#x5012;&#x6211;&#x5011;&#xFF0C;&#x53EF;&#x662F; Web App &#x9084;&#x662F;&#x6709;&#x5F88;&#x591A;&#x5730;&#x65B9;&#x6BD4;&#x4E0D;&#x4E0A; Native App&#xFF0C;&#x4F8B;&#x5982;&#x4E00;&#x5B9A;&#x8981;&#x9023;&#x4E0A;&#x7DB2;&#x3002;&#x53EF;&#x662F;&#x6211;&#x5011;&#x53C8;&#x4E0D;&#x60F3;&#x7279;&#x5730;&#x53BB;&#x5B78; Native Code &#x5462;&#xFF1F;&#x9019;&#x6642;&#x5019;&#x5C31;&#x53EF;&#x4EE5;&#x5BEB; Hybrid App &#x4E86;&#x3002;</p>
<blockquote>
<p>Hybrid App&#xFF1A; &#x6DF7;&#x5408;&#x8A9E;&#x8A00;&#x7A0B;&#x5F0F;&#x7684;&#x90E8;&#x4EFD;&#x4EE3;&#x78BC;&#x6703;&#x4EE5; Web &#x6280;&#x8853;&#x7DE8;&#x5BEB;&#xFF0C;&#x5982; HTML5&#x3001; CSS &#x548C; JavaScript&#x3002;&#x9019;&#x4E9B;&#x7A0B;&#x5F0F;&#x90FD;&#x662F;&#x88AB;&#x5305;&#x88F9;&#x5728;&#x539F;&#x751F;&#x5BB9;&#x5668; (Native Container) &#x548C;&#x900F;&#x904E;&#x624B;&#x6A5F;&#x4E0A;&#x7684;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;&#x4F86;&#x5448;&#x73FE; HTML &#x548C;&#x57F7;&#x884C; JavaScript&#x3002; Hybrid App &#x7684;&#x512A;&#x9EDE;&#x662F;&#x4E00;&#x500B;&#x7DE8;&#x78BC;&#x7A0B;&#x5F0F;&#x80FD;&#x5920;&#x8DE8;&#x8D8A;&#x4E0D;&#x540C;&#x7684;&#x4F5C;&#x696D;&#x5E73;&#x53F0;&#xFF0C;&#x4E0D;&#x9700;&#x8981;&#x70BA;&#x6BCF;&#x500B;&#x64CD;&#x4F5C;&#x7CFB;&#x7D71;&#x7DE8;&#x5BEB;&#x7279;&#x5B9A;&#x7684;&#x7DE8;&#x78BC;&#x3002;</p>
</blockquote>
<p>&#x6211;&#x73FE;&#x5728;&#x6703; Angular&#xFF0C;&#x518D;&#x4EE5; Hybrid App &#x65B9;&#x5F0F;&#x958B;&#x767C;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x7528;&#x5230;&#x6211;&#x7684;&#x5C08;&#x9577;&#x5566;&#xFF01;&#xFF01;<br>
&#x6211;&#x5011;&#x63A1;&#x7528; Cordova + Ionic + Angular 2 &#x4F86;&#x958B;&#x767C;&#x3002;</p>
<ul>
<li>Cordova &#x662F;&#x6DF7;&#x5408;&#x5F0F;&#x6846;&#x67B6;</li>
<li>Ionic &#x662F;&#x57FA;&#x65BC; Cordova &#x7684;&#x9AD8;&#x968E; UI &#x6846;&#x67B6;</li>
<li>Angular 2 &#x662F;&#x7DB2;&#x9801;&#x6280;&#x8853;&#x6846;&#x67B6;</li>
</ul>
<p><img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-2-ionic-2-home.jpg" alt></p>
<h2>Ionic 2</h2>
<p>Ionic &#x6F14;&#x8B8A;&#x81F3;&#x4ECA;&#x662F;&#x7B2C;&#x4E8C;&#x4EE3;&#xFF0C;&#x8DDF;&#x7B2C;&#x4E00;&#x4EE3;&#x5DEE;&#x5225;&#x5728;&#x54EA;&#x5462;&#xFF1F;&#x7B2C;&#x4E00;&#x4EE3;&#x662F;&#x642D;&#x914D; AngularJS(1.x)&#xFF0C;&#x800C;&#x96A8;&#x8457; Angular 2 &#x7684;&#x8A95;&#x751F;&#xFF0C;Ionic 2 &#x4E5F;&#x7522;&#x751F;&#x4E86;&#xFF0C;&#x7576;&#x7136;&#x4E00;&#x4E9B;&#x7D30;&#x7BC0;&#x529F;&#x80FD;&#x4E5F;&#x6709;&#x6539;&#x52D5;&#x3002;</p>
<p>&#x9644;&#x4E0A;&#x5B98;&#x7DB2;&#x7684;&#x4ECB;&#x7D39;&#xFF1A;</p>
<blockquote>
<p>Know how to build websites? Then you already know how to build mobile apps. Ionic Framework offers the best web and native app components for building highly interactive native and progressive web apps with Angular.</p>
</blockquote>
<p>Angular 2 &#x8DDF; React &#x5F7C;&#x6B64;&#x70BA;&#x7AF6;&#x722D;&#x5C0D;&#x624B;&#xFF0C;Ionic 2 &#x8DDF; React Native &#x63A1;&#x7528;&#x5169;&#x8005;&#x7684;&#x7DB2;&#x9801;&#x6846;&#x67B6;&#xFF0C;&#x6240;&#x4EE5;&#x540C;&#x6A23;&#x70BA;&#x5C0D;&#x624B;&#x3002;&#x5169;&#x8005;&#x6982;&#x5FF5;&#x5176;&#x5BE6;&#x90FD;&#x662F; Hybrid App &#x7684;&#x6846;&#x67B6;&#x3002;&#x56E0;&#x70BA;&#x63A1;&#x7528;&#x7684;&#x7DB2;&#x9801;&#x6846;&#x67B6;&#x5C31;&#x662F;&#x4E3B;&#x6D41;&#xFF0C;&#x6DF7;&#x5408;&#x6846;&#x67B6;&#x9019;&#x5169;&#x500B;&#x4E5F;&#x662F;&#x4E3B;&#x6D41;&#xFF0C;&#x81F3;&#x65BC;&#x9078;&#x751A;&#x9EBC;&#x597D;&#x5C31;&#x898B;&#x4EC1;&#x898B;&#x667A;&#x3002;</p>
<p><a href="http://showcase.ionicframework.com/apps/top" target="_blank">&#x9019;&#x908A;</a>&#x9644;&#x4E0A;&#x7528; Ionic &#x958B;&#x767C;&#x7684; APP&#xFF0C;&#x5927;&#x5BB6;&#x53EF;&#x4EE5;&#x9EDE;&#x9032;&#x53BB;&#x770B;&#x770B;</p>
<p>&#x958B;&#x767C;&#x6F02;&#x4EAE;&#x4ECB;&#x9762;&#x3001;&#x529F;&#x80FD;&#x5F37;&#x5927;&#x7684; App &#x6C7A;&#x4E0D;&#x662F;&#x554F;&#x984C;&#xFF01; :)</p>
<p>&#x4EE5;&#x4E0B;&#x70BA;&#x5176;&#x4E2D;&#x5E7E;&#x6B3E;&#x7684;&#x6A23;&#x8C8C;</p>
<p>chefsteps<br>
<img src="http://blog.ionic.io/wp-content/uploads/2015/12/chefsteps-header-2.jpg" alt></p>
<p>Pacifica<br>
<img src="http://ionicframework.com/img/blog/pacifica-header.jpg" alt></p>
<p>&#x660E;&#x5929;&#x7E7C;&#x7E8C;&#x4ECB;&#x7D39;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
