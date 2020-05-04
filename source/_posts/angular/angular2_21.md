---
title: Angular 2 + Ionic = Mobile App ( 2 ) 建構
date: 2017-01-06 23:16:47
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<p><a href="https://ithelp.ithome.com.tw/articles/10188464" target="_blank">&#x4E0A;&#x4E00;&#x7BC7;</a>&#x5DF2;&#x7D93;&#x4ECB;&#x7D39; Ionic &#x642D;&#x914D; Angular 2 &#x662F;&#x751A;&#x9EBC;&#x4E86;&#xFF0C;&#x63A5;&#x4E0B;&#x4F86;&#x5C31;&#x4F86;&#x4ECB;&#x7D39;&#x5982;&#x4F55;&#x5EFA;&#x69CB;&#x4E00;&#x500B; App&#x3002;</p>
<h2>&#x5B89;&#x88DD;</h2>
<p>&#x9996;&#x5148;&#x8981;&#x78BA;&#x5B9A; <a href="https://nodejs.org/en/" target="_blank">Node.js</a> &#x6709;&#x5B89;&#x88DD;</p>
<p>&#x63A5;&#x8005;&#x5B89;&#x88DD; Cordova&#xFF0C;Cordova &#x662F;&#x8DE8;&#x5E73;&#x53F0;&#x5E95;&#x5C64;&#x7684;&#x67B6;&#x69CB;</p>
<pre><code>npm install -g cordova
</code></pre>
<p>&#x5982;&#x679C;&#x662F; Linux &#x8A18;&#x5F97;&#x52A0;&#x4E0A; <code>sudo</code></p>
<p>&#x5B89;&#x88DD; Ionic CLI</p>
<pre><code>npm install -g ionic
</code></pre>
<p>&#x5982;&#x679C;&#x4E4B;&#x524D;&#x6709;&#x5931;&#x6557;&#x6216;&#x662F;&#x6709;&#x5B89;&#x88DD;&#x904E;&#x4E4B;&#x524D;&#x7684;&#x7248;&#x672C;&#xFF0C;&#x53EF;&#x4EE5; <code>npm uninstall -g ionic</code> &#x7136;&#x5F8C;&#x518D;&#x91CD;&#x88DD;&#x4E00;&#x6B21;&#x3002;&#x5B89;&#x88DD;&#x5230;&#x6700;&#x65B0;&#x7248;&#x4E4B;&#x5F8C;&#xFF0C;&#x5982;&#x679C;&#x4EE5;&#x524D;&#x6709;&#x7528; Ionic V1 &#x4ECD;&#x7136;&#x53EF;&#x4EE5;&#x6B63;&#x5E38;&#x904B;&#x4F5C;&#x5594;&#xFF01;&#x5169;&#x500B;&#x7248;&#x672C;&#x517C;&#x5BB9;&#x7684;&#x6982;&#x5FF5;&#x3002;</p>
<p>&#x63A5;&#x8457;&#x53EF;&#x4EE5;&#x6AA2;&#x67E5;&#x4E00;&#x4E0B;&#x5B89;&#x88DD;&#x7D50;&#x679C;</p>
<pre><code>ionic info
</code></pre>
<p>&#x56E0;&#x70BA; Angular 2 &#x662F;&#x7528; TypeScipt &#x4F86;&#x958B;&#x767C;&#xFF0C;&#x6240;&#x4EE5;&#x4E5F;&#x8981;&#x5B89;&#x88DD; TypeScript</p>
<pre><code>npm install -g typescript
</code></pre>
<h2>Hello Ionic</h2>
<p>Ionic 2 &#x63D0;&#x4F9B;&#x4E00;&#x500B;&#x5FEB;&#x901F;&#x5EFA;&#x7ACB;&#x5C08;&#x6848;&#x7684;&#x7BC4;&#x672C;&#xFF0C;&#x7576;&#x7136;&#x4E5F;&#x53EF;&#x4EE5;&#x4E0A;&#x7DB2;&#x627E;&#x5176;&#x4ED6;&#x4EBA;&#x7684;&#x7BC4;&#x672C;&#x7684;&#x4F86;&#x4F7F;&#x7528;&#x3002;</p>
<pre><code>ionic start myIonic2App tutorial --v2
</code></pre>
<ul>
<li>
<code>start</code>&#xFF1A;&#x5EFA;&#x7ACB;&#x65B0;&#x5C08;&#x6848;</li>
<li>
<code>myIonic2App</code>&#xFF1A;&#x5C08;&#x6848;&#x540D;&#x7A31;&#xFF0C;&#x53EF;&#x81EA;&#x8A02;</li>
<li>
<code>tutorial</code>&#xFF1A;&#x958B;&#x59CB;&#x7528;&#x7684;&#x7BC4;&#x672C;&#xFF0C;&#x53EF;&#x4EE5;&#x5728;&#x9019;&#x908A;<a href="https://market.ionic.io/starters/" target="_blank">&#x53C3;&#x8003;</a>&#x5176;&#x4ED6;&#x6A21;&#x677F;</li>
<li>
<code>--v2</code>&#xFF1A;&#x4EE3;&#x8868;&#x7528; V2 &#x958B;&#x767C;&#xFF0C;&#x5982;&#x679C;&#x4F60;&#x60F3;&#x7528; Angular 1 &#x958B;&#x767C;&#x5C31;&#x4E0D;&#x7528;&#x52A0;&#x3002;<br>
&#x9019;&#x6A23; App &#x7684;&#x57FA;&#x790E;&#x5EFA;&#x7F6E;&#x5C31;&#x5B8C;&#x6210;&#x56C9;&#xFF0C;&#x7576;&#x7136;&#x4E4B;&#x5F8C;&#x9084;&#x8981;&#x518D;&#x52A0;&#x5165;&#x5F88;&#x591A;&#x6771;&#x897F;&#x624D;&#x7B97;&#x662F;&#x5B8C;&#x6574;&#x7684; App&#x3002;</li>
</ul>
<p>&#x63A5;&#x8457;&#x5148;&#x9032;&#x5165;&#x8CC7;&#x6599;&#x593E;&#xFF0C;&#x7136;&#x5F8C;&#x555F;&#x52D5;&#x865B;&#x64EC;&#x4F3A;&#x670D;&#x5668;&#xFF0C;&#x4F86;&#x57F7;&#x884C;&#x770B;&#x770B;&#x6211;&#x5011;&#x7684; App&#xFF0C;&#x6211;&#x5011;&#x6703;&#x5148;&#x7528;&#x700F;&#x89BD;&#x5668;&#x6A21;&#x64EC; App &#x756B;&#x9762;&#xFF0C;&#x6BD4;&#x8D77;&#x624B;&#x6A5F;&#x6A21;&#x64EC;&#x5668;&#x4F86;&#x8AAA;&#x5FEB;&#x591A;&#x4E86;&#xFF0C;&#x4E0D;&#x7528;&#x50CF;&#x958B;&#x767C; Native App &#x4E00;&#x6A23;&#xFF0C;&#x6BCF;&#x6539;&#x52D5;&#x4E00;&#x6B21;&#x90FD;&#x8981;&#x7DE8;&#x8B6F;&#x7B49;&#x597D;&#x4E45;&#x3002;</p>
<pre><code>cd myIonic2App
ionic serve
</code></pre>
<p>&#x4F60;&#x6703;&#x88AB;&#x554F;&#x5982;&#x4F55; serve&#xFF0C;&#x9078; <code>localhost:8100</code>&#xFF0C;&#x7136;&#x5F8C;&#x61C9;&#x8A72;&#x6703;&#x81EA;&#x52D5;&#x8D77;&#x52D5;&#x700F;&#x89BD;&#x5668;&#x5230; <code>https://localhost:8100</code>&#xFF0C;&#x5982;&#x679C;&#x6C92;&#x6709;&#x5C31;&#x624B;&#x52D5;&#x8F38;&#x5165;&#x3002;</p>
<p>&#x5982;&#x679C;&#x662F;&#x7528; Chrome&#xFF0C;&#x6309; <code>F12</code> &#x958B;&#x555F;&#x958B;&#x767C;&#x8005;&#x5DE5;&#x5177;&#xFF0C;&#x53EF;&#x4EE5;&#x5207;&#x63DB;&#x6210;&#x624B;&#x6A5F;&#x700F;&#x89BD;&#x6A21;&#x5F0F;&#xFF0C;&#x9084;&#x53EF;&#x4EE5;&#x9078;&#x64C7;&#x6A5F;&#x6B3E;&#x6A21;&#x64EC;&#xFF0C;&#x50CF;&#x9019;&#x908A;&#x5C31;&#x9078; iPhone6<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/devtool.PNG" alt></p>
<p>Chrome &#x958B;&#x767C;&#x6A21;&#x5F0F;&#x4E0B;&#x770B;&#x5230;&#x7684;&#x6A23;&#x5B50;&#x6703;&#x9577;&#x9019;&#x6A23;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/ionic-serve.PNG" alt></p>
<p>&#x5982;&#x679C;&#x60F3;&#x4E00;&#x6B21;&#x770B;&#x6240;&#x6709;&#x5E73;&#x53F0;&#x4E0A;&#x7684; App &#x6A21;&#x6A23;&#xFF0C;&#x53EF;&#x4EE5;&#x8F38;&#x5165;</p>
<pre><code>ionic serve -l
</code></pre>
<p>&#x5C31;&#x6703;&#x9577;&#x9019;&#x6A23;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/ionicserve2.PNG" alt></p>
<p>&#x597D;&#x56C9;&#xFF0C;&#x6240;&#x4EE5;&#x9810;&#x5099;&#x52D5;&#x4F5C;&#x90FD;&#x5B8C;&#x6210;&#x5566;&#xFF01;&#x9019;&#x6A23;&#x5C31;&#x53EF;&#x4EE5;&#x4F86;&#x958B;&#x767C;&#x4E86; :)</p>
<h2>Ionic 2 &#x5C08;&#x6848;&#x67B6;&#x69CB;</h2>
<p>&#x5148;&#x4F86;&#x770B;&#x770B; Ionic 2 &#x7684;&#x5C08;&#x6848;&#x67B6;&#x69CB;</p>
<pre><code>&#x251C;&#x2500;&#x2500; config.xml
&#x251C;&#x2500;&#x2500; hooks
&#x251C;&#x2500;&#x2500; ionic.config.json
&#x251C;&#x2500;&#x2500; node_modules
&#x251C;&#x2500;&#x2500; package.json
&#x251C;&#x2500;&#x2500; platforms
&#x251C;&#x2500;&#x2500; plugins
&#x251C;&#x2500;&#x2500; resources
&#x251C;&#x2500;&#x2500; src
&#x251C;&#x2500;&#x2500; tsconfig.json
&#x251C;&#x2500;&#x2500; tslint.json
</code></pre>
<ul>
<li>
<code>config.xml</code>: App &#x540D;&#x7A31;&#x3001;App &#x7248;&#x672C;&#x3001;&#x4E00;&#x4E9B;&#x8A2D;&#x5B9A;&#x503C;&#x7B49;&#x7B49;</li>
<li>
<code>hooks</code>: &#x52A0;&#x5165;&#x81EA;&#x5DF1;&#x5BEB;&#x7684; Native Code</li>
<li>
<code>platforms</code>: &#x5EFA;&#x7ACB; Android&#x3001;IOS &#x8F38;&#x51FA;&#x5E73;&#x53F0;</li>
<li>
<code>plugins</code>: Cordova &#x53EF;&#x4EE5;&#x52A0;&#x5165; Native Code &#x7684; Plugin</li>
<li>
<code>resources</code>: &#x5305;&#x542B;&#x4E00;&#x4E9B;&#x8CC7;&#x6E90;&#xFF0C;&#x50CF;&#x662F; App &#x5716;&#x793A;&#x3001;&#x555F;&#x52D5;&#x5716;&#x7247;&#x4E4B;&#x985E;&#x7684;</li>
<li>
<code>src</code>: &#x6211;&#x5011;&#x5BEB;&#x7684;&#x6240;&#x6709; code &#x5E7E;&#x4E4E;&#x90FD;&#x6703;&#x5728;&#x9019;&#x88E1;&#xFF0C;&#x6982;&#x5FF5;&#x8DDF; Angular CLI &#x5F88;&#x50CF;&#xFF0C;&#x4E4B;&#x5F8C;&#x6703;&#x88AB;&#x8F38;&#x51FA;&#x5230; <code>WWW</code> &#x8CC7;&#x6599;&#x593E;</li>
</ul>
<p>Ionic App &#x5EFA;&#x69CB;&#x7684;&#x90E8;&#x5206;&#x5C31;&#x5230;&#x9019;&#x908A;&#x5566;&#xFF01;<br>
&#x660E;&#x5929;&#x8981;&#x8A0E;&#x8AD6;&#x5982;&#x4F55;&#x958B;&#x59CB;&#x7528; Angular 2 &#x4F86;&#x505A;&#x958B;&#x767C;&#x56C9;&#xFF01;</p>
 <br>
                                                    </div>
                    </div>
                
