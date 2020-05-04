---
title: Angular 2 組件相關的路徑
date: 2017-01-04 23:49:31
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x7D44;&#x4EF6;&#x88E1;&#x7684; URLs</h2>
<h3>&#x7D55;&#x5C0D;&#x8DEF;&#x5F91;</h3>
<p>&#x7D44;&#x4EF6;&#x5E38;&#x5E38;&#x6703;&#x8981;&#x4F7F;&#x7528;&#x5916;&#x90E8;&#x6A21;&#x677F;&#x8DDF;&#x98A8;&#x683C;&#x7684;&#x6A94;&#x6848;&#xFF0C;&#x6211;&#x5011;&#x5728; <code>templateUrl</code> &#x548C; <code>styleUrls</code> &#x7279;&#x6027;&#x4E2D;&#x7528; URL &#x5B9A;&#x7FA9;&#x9019;&#x4E9B;&#x6A94;&#x6848;&#xFF0C;&#x5C31;&#x50CF;&#x9019;&#x6A23;&#xFF1A;</p>
<pre><code>@Component({
  selector: &apos;absolute-path&apos;,
  templateUrl: &apos;app/some.component.html&apos;,
  styleUrls:  [&apos;app/some.component.css&apos;]
})
</code></pre>
<p>&#x9810;&#x8A2D;&#x4E2D;&#xFF0C;&#x6211;&#x5011;&#x5FC5;&#x9808;&#x586B;&#x4E0A;&#x7D55;&#x5C0D;&#x8DEF;&#x5F91;&#x7684; URL&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5B8C;&#x6574;&#x8DEF;&#x5F91;&#xFF0C;&#x4F46;&#x662F;&#x9019;&#x6A23;&#x5F88;&#x9EBB;&#x7169;&#xFF0C;&#x6A94;&#x6848;&#x898F;&#x6A21;&#x8B8A;&#x5F88;&#x5927;&#x6642;&#xFF0C;&#x4F60;&#x5927;&#x6982;&#x4E5F;&#x8A18;&#x4E0D;&#x8D77;&#x4F86;&#x5B8C;&#x6574;&#x8DEF;&#x5F91;&#x3002;&#x90A3;&#x6709;&#x6C92;&#x6709;&#x66F4;&#x597D;&#x7684;&#x65B9;&#x6CD5;&#xFF1F;</p>
<h3>&#x7D44;&#x4EF6;&#x76F8;&#x5C0D;&#x8DEF;&#x5F91; (Component-Relative Path)</h3>
<p>&#x7576;&#x7136;&#x6709;&#x3002;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x53EA;&#x8981;&#x8F38;&#x5165;&#x548C;&#x7D44;&#x4EF6;&#x540C;&#x4E00;&#x5C64;&#x7684;&#x76F8;&#x5C0D;&#x8DEF;&#x5F91; (Component-Relative Path)&#x3002;<br>
&#x9996;&#x5148;&#x6211;&#x5011;&#x8981;&#x628A;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x5EFA;&#x7ACB;&#x6210; <code>commonjs</code> &#x5F62;&#x5F0F;&#x7684; modules &#x4E26;&#x4E14;&#x7528; <code>systemjs</code> or <code>webpack</code> &#x9019;&#x985E;&#x7684; package loader &#x8F09;&#x5165;&#x5C31;&#x597D;&#x3002;</p>
<blockquote>
<p>Angular CLI &#x6216; Angular SEED &#x9019;&#x985E;&#x7684;&#x5957;&#x4EF6;&#x5DF2;&#x7D93;&#x5C07;&#x9019;&#x500B;&#x6280;&#x8853;&#x8A2D;&#x70BA;&#x9810;&#x8A2D;&#x3002;</p>
</blockquote>
<p>&#x597D;&#xFF0C;&#x6240;&#x4EE5;&#x73FE;&#x5728;&#x6211;&#x6709;&#x500B;&#x5C08;&#x6848;&#x9577;&#x9019;&#x6A23;&#x3002;&#x88E1;&#x9762;&#x6709;&#x500B; APP &#x8CC7;&#x6599;&#x593E;&#xFF0C;&#x5305;&#x542B;&#x4E86;&#x5E7E;&#x500B;&#x6A94;&#x6848;&#x3002;&#x5982;&#x679C;&#x8981;&#x63A1;&#x7528;&#x65B0;&#x65B9;&#x6CD5;&#x7684;&#x8A71;&#x61C9;&#x8A72;&#x8981;&#x9019;&#x6A23;&#xFF1A;</p>
<pre><code>app
&#x251C; some.component.css
&#x251C; some.component.html
&#x2514; some.component.ts
...
</code></pre>
<p>&#x4E00;&#x500B;&#x7D44;&#x4EF6;&#x7684;&#x5144;&#x5F1F;&#x59CA;&#x59B9;&#x5305;&#x542B;&#x6A21;&#x677F; (template) &#x8DDF;&#x98A8;&#x683C; (style)&#xFF0C;&#x61C9;&#x8A72;&#x8981;&#x6C38;&#x9060;&#x5728;&#x4E00;&#x8D77;&#x3002;<br>
&#x547D;&#x540D;&#x898F;&#x5247;&#x5247;&#x662F; <code>xxx.component</code> &#x52A0;&#x4E0A; <code>.html</code>&#x3001;<code>.css</code> &#x6216; <code>.ts</code>&#x3002;</p>
<h2>&#x8A2D;&#x5B9A; moduleId</h2>
<p>&#x4F9D;&#x7167;&#x7D50;&#x69CB;&#x6163;&#x4F8B;&#xFF0C;&#x5C31;&#x662F;&#x5144;&#x5F1F;&#x59CA;&#x59B9;&#x4E0D;&#x53EF;&#x5206;&#x96E2;&#x7684;&#x60C5;&#x6CC1;&#xFF0C;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x8F15;&#x6613;&#x5730;&#x627E;&#x5230;&#x6A21;&#x677F;&#x8DDF;&#x98A8;&#x683C;&#x7684;&#x6A94;&#x6848;&#xFF0C;&#x53EA;&#x8981;&#x6211;&#x5011;&#x5728; <code>@Component</code> &#x7684; metadata &#x4E2D;&#x52A0;&#x5165;<code>moduleId</code> &#x7279;&#x6027;&#x3002;</p>
<pre><code>moduleId: module.id,
</code></pre>
<p>&#x73FE;&#x5728;&#x6211;&#x5011;&#x53EA;&#x8981;&#x653E;&#x76F8;&#x5C0D;&#x8DEF;&#x5F91;&#x5C31;&#x597D;</p>
<pre><code>@Component({
  moduleId: module.id,
  templateUrl: &apos;some.component.html&apos;,
  styleUrls:  [&apos;some.component.css&apos;]
})
</code></pre>
<p>&#x9019;&#x6A23; Angular &#x5C31;&#x77E5;&#x9053;&#x81EA;&#x5DF1;&#x53BB;&#x627E;&#x5144;&#x5F1F;&#x59CA;&#x59B9;&#xFF0C;&#x6240;&#x4EE5;&#x4E0D;&#x7528;&#x8A2D;&#x5B9A;&#x7D55;&#x5C0D;&#x8DEF;&#x5F91;&#x3002;<br>
&#x4F46;&#x8A18;&#x4F4F;&#xFF0C;&#x524D;&#x63D0;&#x662F;&#x90FD;&#x653E;&#x5728;&#x540C;&#x4E00;&#x5C64;&#x8CC7;&#x6599;&#x593E;&#x4E2D;&#xFF0C;&#x4E14;&#x547D;&#x540D;&#x6CD5;&#x4E00;&#x6A23;&#x3002;</p>
<p>&#x53EF;&#x4EE5;&#x770B;&#x770B; <a href="https://embed.plnkr.co/onUAO7yNrqGR9Pn9uP10/" target="_blank">Plunker</a> &#x7684;&#x6548;&#x679C;&#x3002;</p>
<h2>&#x539F;&#x7406;</h2>
<p>Angular &#x53EA;&#x77E5;&#x9053;&#x7D55;&#x5C0D;&#x8DEF;&#x5F91;&#xFF0C;&#x800C; <code>index.html</code> &#x7684;&#x5730;&#x65B9;&#x70BA; root&#xFF0C;&#x6240;&#x4EE5;&#x5148;&#x524D;&#x6211;&#x5011;&#x90FD;&#x9700;&#x8981;&#x5728;&#x6A94;&#x540D;&#x524D;&#x9762;&#x52A0;&#x4E0A; <code>app/</code>&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x6211;&#x5011;&#x63A1;&#x7528; <code>commonjs</code> &#x7684;&#x5F62;&#x5F0F;&#xFF0C;&#x4E26;&#x4E14;&#x52A0;&#x4E0A; <code>moduleId</code>&#xFF0C;Angular &#x5C31;&#x6703;&#x5148;&#x627E;&#x5230;&#x7D44;&#x4EF6;&#x7684;&#x7D55;&#x5C0D;&#x4F4D;&#x7F6E;&#xFF0C;&#x7136;&#x5F8C;&#x5728;&#x628A;&#x5176;&#x4ED6;&#x6A94;&#x6848;&#x51A0;&#x4E0A;&#x7D44;&#x4EF6;&#x7684;&#x7D55;&#x5C0D;&#x4F4D;&#x7F6E;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x624D;&#x53EA;&#x9700;&#x8981;&#x8F38;&#x5165;&#x8207;&#x7D44;&#x4EF6;&#x76F8;&#x95DC;&#x7684;&#x76F8;&#x5C0D;&#x8DEF;&#x5F91;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
