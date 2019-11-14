---
title: Angular 2 + Ionic = Mobile App ( 4 ) 發布 App
date: 2017-01-08 23:55:34
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x6211;&#x5011;&#x5728;&#x96FB;&#x8166;&#x4E0A;&#x7528; ionic serve &#x6E2C;&#x8A66;&#x597D;&#x6211;&#x5011;&#x7684; App &#x4E4B;&#x5F8C;&#xFF0C;&#x6700;&#x5F8C;&#x4ECD;&#x7136;&#x9700;&#x8981;&#x62FF;&#x5230;&#x5BE6;&#x969B;&#x88DD;&#x7F6E;&#x4E0A;&#x6E2C;&#x8A66;&#xFF0C;&#x4E0D;&#x50C5;&#x662F;&#x56E0;&#x70BA;&#x5230;&#x6642;&#x5019;&#x672C;&#x4F86;&#x5C31;&#x662F;&#x8981;&#x7D66;&#x624B;&#x6A5F;&#x4F7F;&#x7528;&#x7684;&#xFF0C;&#x4E26;&#x4E14;&#x5F88;&#x591A;&#x7684; Native Plugin &#x53EA;&#x6709;&#x5728;&#x88DD;&#x7F6E;&#x4E0A;&#x624D;&#x80FD;&#x771F;&#x6B63;&#x7684;&#x4F7F;&#x7528;&#x3002;</p>
<p>&#x9019;&#x908A;&#x4EE5; IOS&#x3001;Android &#x70BA;&#x4F8B;&#x4F86;&#x793A;&#x7BC4;&#x5982;&#x4F55;&#x767C;&#x5E03; App&#x3002;</p>
<p>&#x6B64;&#x5916;&#x5B8C;&#x6210;&#x4E00;&#x500B; App &#x9084;&#x5305;&#x62EC;&#x4ED6;&#x7684;&#x5716;&#x793A;&#x4EE5;&#x53CA;&#x4ED6;&#x958B;&#x59CB;&#x756B;&#x9762;&#x3002;</p>
<h2>Build/Run the App</h2>
<h3>Android</h3>
<p>&#x8981;&#x5148;&#x5B89;&#x88DD; Android SDK &#x8DDF; Java&#xFF0C;&#x7D30;&#x7BC0;&#x53EF;&#x4EE5;&#x770B;<a href="http://ionicframework.com/docs/v2/resources/platform-setup/windows-setup.html" target="_blank">&#x9019;&#x908A;</a>&#x3002;</p>
<pre><code>ionic platform add android
</code></pre>
<p>&#x9019;&#x6A23;&#x6703;&#x5728; platforms &#x589E;&#x52A0;&#x4E00;&#x500B; android &#x8CC7;&#x6599;&#x593E;&#xFF0C;&#x4E26;&#x52A0;&#x5165;&#x4E00;&#x4E9B;&#x5EFA;&#x7ACB; android app &#x9700;&#x8981;&#x7684;&#x8CC7;&#x6E90;&#x3002;</p>
<pre><code>ionic build android
</code></pre>
<p>&#x7136;&#x5F8C;&#x5EFA;&#x7ACB;&#x4E00;&#x500B; APK&#xFF0C;&#x653E;&#x5728;<code>platforms/android/build/outputs</code></p>
<pre><code>ionic run android --device
</code></pre>
<p>&#x78BA;&#x5B9A;&#x4F60;&#x7684;&#x624B;&#x6A5F;&#x9023;&#x4E0A;&#x96FB;&#x8166;&#xFF0C;&#x958B;&#x767C;&#x8005;&#x4EBA;&#x54E1;&#x7684;&#x9664;&#x932F;&#x6A21;&#x5F0F;&#x8981;&#x6253;&#x958B;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x88DD;&#x4E0A;&#x624B;&#x6A5F;&#x4E86;&#x3002;&#x4E5F;&#x53EF;&#x4EE5;&#x8DF3;&#x904E; <code>build</code> &#x76F4;&#x63A5; <code>run</code>&#x3002;</p>
<h3>IOS</h3>
<p>&#x5FC5;&#x9808;&#x4F7F;&#x7528; Mac &#x4E14;&#x6709;&#x5B89;&#x88DD; Xcode</p>
<pre><code>npm install -g ios-deploy
npm install -g ios-sim version
</code></pre>
<p>&#x5148;&#x5B89;&#x88DD;&#x4E00;&#x4E9B;&#x5957;&#x4EF6;</p>
<pre><code>ionic platform add ios
ionic build ios
ionic run ios
</code></pre>
<p>&#x6B65;&#x9A5F;&#x8DDF; Andoird &#x4E00;&#x6A23;&#xFF0C;&#x6A94;&#x6848;&#x6703;&#x88AB;&#x8F38;&#x51FA;&#x5230; <code>platforms/ios/build/emulator</code>&#x3002;</p>
<p>&#x6210;&#x529F; Build &#x548C; Run &#x6703;&#x770B;&#x5230;&#x4EE5;&#x4E0B;&#x7D50;&#x679C;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/ionic-build-run-success.PNG" alt></p>
<h2>Icon</h2>
<p>&#x6211;&#x5011;&#x9084;&#x7F3A; App &#x5716;&#x793A;&#x8DDF;&#x958B;&#x59CB;&#x756B;&#x9762;</p>
<p>&#x6211;&#x7C21;&#x55AE;&#x756B;&#x4E86;&#x4E00;&#x4E0B;&#xFF0C;&#x5927;&#x6982;&#x9577;&#x9019;&#x6A23;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/todo-icon.png" alt></p>
<p>Icon &#x898F;&#x683C;&#x662F; <code>png</code>&#x3001;<code>ai</code> &#x6216; <code>psd</code> &#x6A94;&#x6848;&#xFF0C;&#x81F3;&#x5C11; 192*192 px&#xFF0C;&#x628A;&#x756B;&#x597D;&#x7684;&#x6A94;&#x6848;&#x540D;&#x7A31;&#x53D6;&#x70BA; <code>icon.png</code>&#x3001;<code>icon.ai</code> &#x6216; <code>icon.psd</code> &#x653E;&#x5165; <code>resources</code> &#x8CC7;&#x6599;&#x593E;&#xFF0C;&#x63A5;&#x8457;&#x8F38;&#x5165;</p>
<pre><code>ionic resources --icon
</code></pre>
<p>Ionic &#x5C31;&#x6703;&#x81EA;&#x52D5;&#x5E6B;&#x6211;&#x5011;&#x628A;&#x5404;&#x7A2E;&#x5927;&#x5C0F;&#x7684;&#x5716;&#x793A;&#x7522;&#x751F;&#x51FA;&#x4F86;&#xFF0C;&#x4E26;&#x5728; <code>config.xml</code> &#x6587;&#x4EF6;&#x81EA;&#x52D5;&#x66F4;&#x65B0;</p>
<h2>Splash</h2>
<p>&#x7A0B;&#x5F0F;&#x958B;&#x555F;&#x756B;&#x9762; (splash) &#x6700;&#x5F8C;&#x5927;&#x6982;&#x9577;&#x9019;&#x6A23;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/todo-splash.png" alt></p>
<p>Splash &#x898F;&#x683C;&#x662F; <code>png</code>&#x3001;<code>ai</code> &#x6216; <code>psd</code> &#x6A94;&#x6848;&#xFF0C;&#x81F3;&#x5C11; 2208*2208 px&#xFF0C;&#x628A;&#x756B;&#x597D;&#x7684;&#x6A94;&#x6848;&#x540D;&#x7A31;&#x53D6;&#x70BA; <code>splash.png</code>&#x3001;splash.ai &#x6216; <code>splash.psd</code> &#x653E;&#x5165; <code>resources</code> &#x8CC7;&#x6599;&#x593E;&#xFF0C;&#x63A5;&#x8457;&#x8F38;&#x5165;</p>
<pre><code>ionic resources --splash
</code></pre>
<p>Ionic &#x5C31;&#x6703;&#x81EA;&#x52D5;&#x5E6B;&#x6211;&#x5011;&#x628A;&#x5404;&#x7A2E;&#x5927;&#x5C0F;&#x7684;&#x958B;&#x59CB;&#x756B;&#x9762;(&#x5305;&#x62EC;&#x6A6B;&#x7684;&#x3001;&#x76F4;&#x7684;)&#x7522;&#x751F;&#x51FA;&#x4F86;&#xFF0C;&#x4E26;&#x5728; <code>config.xml</code> &#x6587;&#x4EF6;&#x81EA;&#x52D5;&#x66F4;&#x65B0;</p>
 <br>
                                                    </div>
                    </div>
                
