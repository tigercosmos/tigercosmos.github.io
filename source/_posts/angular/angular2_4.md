---
title: Angular2 模板與綁定－－互動的根本
date: 2016-12-20 23:41:58
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<p>&#x5148;&#x524D;&#x5728;&#x8AAA;&#x660E; Angular 2 &#x7684;&#x67B6;&#x69CB;&#x6642;&#x6709;&#x7D04;&#x7565;&#x63D0;&#x5230;&#x6578;&#x64DA;&#x7D81;&#x5B9A;&#x7684;&#x65B9;&#x5F0F;&#xFF0C;&#x63A5;&#x8457;&#x5C31;&#x8B93;&#x6211;&#x5011;&#x5B78;&#x5B78;&#x5982;&#x4F55;&#x5BEB;&#x6A21;&#x677F; (template) &#xFF0C;&#x5982;&#x4F55;&#x986F;&#x793A;&#x6578;&#x64DA;&#x548C;&#x4E8B;&#x4EF6;&#x7D81;&#x5B9A;&#x3002;&#x90A3;&#x70BA;&#x751A;&#x9EBC;&#x8981;&#x5B78;&#x6A21;&#x677F;&#x7684;&#x5BEB;&#x6CD5;&#x5462;&#xFF1F;&#x4EE5;&#x53CA;&#x6A21;&#x677F;&#x5230;&#x5E95;&#x53EF;&#x4EE5;&#x5E79;&#x55CE;&#xFF1F;&#x6211;&#x5011;&#x770B;&#x5230;&#x7684;&#x7DB2;&#x7AD9;&#x90FD;&#x662F; HTML &#x7684;&#x986F;&#x793A;&#xFF0C;&#x4F46;&#x662F; HTML &#x662F;&#x6B7B;&#x7684;&#xFF0C;&#x8981;&#x505A;&#x51FA;&#x4E92;&#x52D5;&#x50B3;&#x7D71;&#x4E0A;&#x5FC5;&#x9808;&#x9760; JavaScript&#xFF0C;&#x4F46;&#x662F; JS &#x63A7;&#x5236; HTML</p>
<blockquote>
<h4>&#x6578;&#x64DA;&#x7D81;&#x5B9A;&#x5C0F;&#x8907;&#x7FD2;</h4>
<ul>
<li>Interpolation</li>
<li>One Way Binding</li>
<li>Two Way Binding</li>
<li>Event Binding</li>
</ul>
</blockquote>
<h2>&#x6982;&#x89C0;</h2>
<h3>&#x8A9E;&#x6CD5;</h3>
<p>&#x5728; Anugular 2 &#x4E2D;&#xFF1A;</p>
<ul>
<li>One Way Binding&#xFF1A;&#x5F9E;&#x770B;&#x5230;&#x7684;&#x76EE;&#x6A19;&#x7D81;&#x5B9A;&#x6578;&#x64DA;&#x4F86;&#x6E90;&#x7528;&#x7684;&#x662F;&#xFF1A;
<ul>
<li>(target) = &quot;statement&quot;</li>
<li>on-target = &quot;statement&quot;</li>
</ul>
</li>
<li>One Way Binding&#xFF1A;&#x5F9E;&#x6578;&#x64DA;&#x4F86;&#x6E90;&#x7D81;&#x5B9A;&#x770B;&#x5230;&#x7684;&#x76EE;&#x6A19;&#x7528;&#x7684;&#x662F;&#xFF1A;
<ul>
<li>{{expression}}</li>
<li>[target] = &quot;expression&quot;</li>
<li>bind-target = &quot;expression&quot;</li>
</ul>
</li>
<li>Two Way Binding&#xFF1A;&#x6578;&#x64DA;&#x7AEF;&#x8DDF;&#x8996;&#x89BA;&#x7AEF;&#x53EF;&#x4EE5;&#x4E92;&#x76F8;&#x7D81;&#x5B9A;&#x7528;&#x7684;&#x662F;&#xFF1A;
<ul>
<li>[(target)] = &quot;expression&quot;</li>
<li>bindon-target = &quot;expression&quot;</li>
</ul>
</li>
</ul>
<h3>&#x7BC4;&#x4F8B;</h3>
<p>&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x518D; Component &#x4E2D;&#x5BA3;&#x544A;&#x81EA;&#x5DF1;&#x7684;&#x6A19;&#x7C64;</p>
<pre><code>&lt;!-- Normal HTML --&gt;
&lt;div class=&quot;special&quot;&gt;Mental Model&lt;/div&gt;
&lt;!-- Wow! A new element! --&gt;
&lt;hero-detail&gt;&lt;/hero-detail&gt;
</code></pre>
<p>Component &#x4E2D;&#x7684; <code>isValid</code> &#x70BA; <code>false</code> &#x7684;&#x6642;&#x5019;&#x6309;&#x9215;&#x9396;&#x4F4F;&#x3002;</p>
<pre><code>&lt;!-- Bind button disabled state to `isValid` property --&gt;
&lt;button [disabled]=&quot;!isValid&quot;&gt;Save&lt;/button&gt;
</code></pre>
<p>&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x7D81;&#x5B9A;&#x9023;&#x7D50;</p>
<pre><code>&lt;img [src]=&quot;imageUrl&quot;&gt;
</code></pre>
<p>&#x53EF;&#x4EE5;&#x7D81;&#x5B9A;&#x7279;&#x6027;</p>
<pre><code>&lt;div [ngClass]=&quot;classes&quot;&gt;[ngClass] binding to the classes property&lt;/div&gt;
</code></pre>
<h2>&#x7D81;&#x5B9A; Attribute&#x3001;class&#x3001;style</h2>
<h3>&#x7528;&#x9014;</h3>
<p>&#x7576;&#x6211;&#x5011;&#x60F3;&#x91DD;&#x5C0D; HTML &#x7684;&#x5C6C;&#x6027;&#x3001;&#x985E;&#x5225;&#x3001;&#x98A8;&#x683C;&#x505A;&#x6539;&#x8B8A;&#x6642;&#xFF0C;&#x900F;&#x904E; Angular &#x7279;&#x6027; (property) &#x7D81;&#x5B9A;&#x7684;&#x65B9;&#x5F0F;&#xFF0C;&#x53EF;&#x4EE5;&#x8F15;&#x9B06;&#x4E00;&#x64DA;&#x7D81;&#x5B9A;&#x7684;&#x6578;&#x64DA;&#x505A;&#x6539;&#x8B8A;&#xFF0C;&#x6BD4;&#x65B9;&#x8AAA;&#x60F3;&#x8981;&#x9054;&#x6210;&#x6309;&#x4E0B;&#x6309;&#x9215;&#x984F;&#x8272;&#x6539;&#x8B8A;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x900F;&#x904E;&#x9019;&#x7A2E;&#x65B9;&#x5F0F;&#xFF0C;&#x6BD4;&#x8D77;&#x50B3;&#x7D71;&#x7684;&#x65B9;&#x5F0F;&#xFF0C;&#x589E;&#x52A0;&#x4E0D;&#x5C11;&#x4FBF;&#x5229;&#x6027;&#x3002;</p>
<h3>Attribute binding (&#x5C6C;&#x6027;&#x7D81;&#x5B9A;)</h3>
<p>&#x91DD;&#x5C0D; HTML &#x7269;&#x4EF6;&#x7684;&#x5C6C;&#x6027;&#x4F5C;&#x7D81;&#x5B9A;&#xFF0C;&#x53EF;&#x4EE5;&#x4F9D;&#x64DA;&#x7D81;&#x5B9A;&#x7684;&#x8B8A;&#x6578;&#x6578;&#x503C;&#x8B8A;&#x5316;&#x800C;&#x6539;&#x8B8A;&#x5C6C;&#x6027;&#x3002;</p>
<pre><code>&lt;table border=1&gt;
  &lt;!--  expression calculates colspan=2 --&gt;
  &lt;tr&gt;&lt;td [attr.colspan]=&quot;1 + 1&quot;&gt;One-Two&lt;/td&gt;&lt;/tr&gt;

  &lt;tr&gt;&lt;td&gt;Five&lt;/td&gt;&lt;td&gt;Six&lt;/td&gt;&lt;/tr&gt;
&lt;/table&gt;
</code></pre>
<h3>Class binding</h3>
<p>&#x7576;&#x7D81;&#x5B9A;&#x7684;&#x6578;&#x503C;&#x70BA; <code>true</code> &#x6642;&#x986F;&#x793A; <code>class</code>&#xFF0C;<code>false</code> &#x79FB;&#x9664; <code>class</code></p>
<pre><code>&lt;!-- toggle the &quot;special&quot; class on/off with a property --&gt;
&lt;div [class.special]=&quot;isSpecial&quot;&gt;The class binding is special&lt;/div&gt;

&lt;!-- binding to `class.special` trumps the class attribute --&gt;
&lt;div class=&quot;special&quot;
     [class.special]=&quot;!isSpecial&quot;&gt;This one is not so special&lt;/div&gt;
</code></pre>
<h3>Style binding</h3>
<p>&#x4E00;&#x6A23;&#x7684;&#x908F;&#x8F2F;&#x4E5F;&#x53EF;&#x4EE5;&#x7528;&#x5728; style</p>
<pre><code>&lt;button [style.color] = &quot;isSpecial ? &apos;red&apos;: &apos;green&apos;&quot;&gt;Red&lt;/button&gt;
&lt;button [style.background-color]=&quot;canSave ? &apos;cyan&apos;: &apos;grey&apos;&quot; &gt;Save&lt;/button&gt;
</code></pre>
<h2>&#x4E8B;&#x4EF6;&#x7D81;&#x5B9A; (Event binding)</h2>
<p>&#x4E00;&#x822C;&#x7684;&#x4E8B;&#x4EF6;&#x7D81;&#x5B9A;<br>
tempalte:</p>
<pre><code>&lt;button (click)=&quot;onSave()&quot;&gt;Save&lt;/button&gt;
</code></pre>
<p>Component:</p>
<pre><code>@Component({
    ...
})
export class AppComponent {
    onSave(): void{
        ...
    }
}
</code></pre>
<p>&#x9019;&#x7A2E;&#x4E00;&#x822C;&#x7684;&#x7528;&#x6CD5;&#xFF0C;&#x53EF;&#x4EE5;&#x62FF;&#x4F86;&#x505A;&#x6309;&#x9215;&#x547C;&#x53EB; API &#x63D0;&#x4EA4;&#x8868;&#x55AE;&#x7B49;&#x7B49;&#xFF0C;&#x4E0D;&#x9700;&#x8981;&#x505A; HTML Element &#x8B8A;&#x5316;&#x7684;&#x4E92;&#x52D5;&#x3002;</p>
<p>&#x4E5F;&#x53EF;&#x4EE5;&#x662F;&#x81EA;&#x8A02;&#x7684;&#x4E8B;&#x4EF6;&#x7D81;&#x5B9A;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x6211;&#x5011;&#x7528; Angular <code>EventEmitter</code><br>
&#x6211;&#x5011;&#x9019;&#x6A23;&#x5B9A;&#x7FA9;&#x89F8;&#x767C;&#x4E8B;&#x4EF6;&#xFF1A;</p>
<pre><code>deleteRequest = new EventEmitter&lt;Hero&gt;();

delete() {
  this.deleteRequest.emit(this.hero);
}
</code></pre>
<p>&#x6A21;&#x677F;&#xFF1A;</p>
<pre><code>&lt;div&gt;
      ...
  &lt;button (click)=&quot;delete()&quot;&gt;Delete&lt;/button&gt;
      ...
&lt;/div&gt;
&lt;hero-detail (deleteRequest)=&quot;deleteHero($event)&quot; [hero]=&quot;currentHero&quot;&gt;&lt;/hero-detail&gt;
</code></pre>
<p>&#x7576; <code>delete()</code> &#x57F7;&#x884C;&#xFF0C;&#x6703;&#x89F8;&#x767C; <code>deleteRequest</code> &#x7522;&#x751F;&#x7684; <code>EvevntEmitter</code> &#x7269;&#x4EF6;&#x88FD;&#x9020;&#x51FA; <code>Hero</code> &#xFF0C;&#x63A5;&#x8005; <code>&lt;hero-detail&gt;</code> &#x6703;&#x8DDF;&#x8457; <code>deleteRequest</code> &#x4E8B;&#x4EF6;&#x89F8;&#x767C;&#x7684;&#x6539;&#x8B8A;&#x800C;&#x6539;&#x8B8A;&#x3002;</p>
<h2>&#x6578;&#x64DA;&#x7D81;&#x5B9A;</h2>
<h3>Interpolation</h3>
<p>&#x57FA;&#x672C;&#x5C31;&#x662F;&#x5728; <code>html</code> template &#x88E1;&#x9762;&#x52A0;&#x4E0A; <code>{ { } }</code>&#xFF0C;&#x4E2D;&#x9593;&#x5305;&#x4F4F;&#x60F3;&#x8981;&#x986F;&#x793A;&#x7684;&#x8B8A;&#x6578;&#xFF0C;&#x800C;&#x8B8A;&#x6578;&#x5247;&#x662F;&#x5BA3;&#x544A;&#x5728; <code>app.component.ts</code> &#x88E1;&#x9762;&#x3002;<br>
&#x4F86;&#x770B;&#x770B;&#x7BC4;&#x4F8B;&#xFF1A;</p>
<pre><code>// app.component.ts
import {Component} from &apos;angular2/core&apos;;
@Component({
  selector: &apos;my-app&apos;,
  templateUrl: &apos;app.component.html&apos;,
  styleUrls: [&apos;app.component.css&apos;]
})
export class AppComponent {
  title = &apos;Tour of Heroes&apos;;
  myHero = &apos;Windstorm&apos;;
}
</code></pre>
<pre><code>// app.component.html
  &lt;h1&gt;{{title}}&lt;/h1&gt;
  &lt;h2&gt;My favorite hero is: {{myHero}}&lt;/h2&gt;
</code></pre>
<p>&#x6703;&#x986F;&#x793A;&#x6210;&#x9019;&#x6A23;&#xFF1A;<br>
<img src="https://angular.io/resources/images/devguide/displaying-data/title-and-hero.png" alt><br>
&#x56E0;&#x70BA;&#x662F;&#x5728;&#x540C;&#x500B; Component&#xFF0C;&#x7576; Angular &#x5728; Template &#x4E2D;&#x5075;&#x6E2C;&#x5230; <code>{ { } }</code> &#x7684;&#x6642;&#x5019;&#xFF0C; Class &#x88E1;&#x7684;&#x8B8A;&#x6578;&#x6703;&#x76F4;&#x63A5;&#x88AB;&#x653E;&#x5230; <code>{ { } }</code> &#x88E1;&#x9762;&#x3002;&#x7576;&#x8B8A;&#x6578;&#x503C;&#x767C;&#x751F;&#x6539;&#x8B8A;&#x6642;&#x4E5F;&#x6703;&#x8DDF;&#x8457;&#x66F4;&#x65B0;&#x986F;&#x793A;&#xFF0C;&#x6578;&#x503C;&#x91CD;&#x65B0;&#x6E32;&#x67D3;&#x986F;&#x793A;&#x662F;&#x767C;&#x751F;&#x5728;&#x8207;&#x8996;&#x5716;&#x76F8;&#x95DC;&#x7684;&#x67D0;&#x4E9B;&#x7570;&#x6B65;&#x4E8B;&#x4EF6;&#x4E4B;&#x5F8C;&#xFF0C;&#x4F8B;&#x5982;&#x9EDE;&#x64CA;&#x3001;&#x52FE;&#x9078;&#x3001;&#x547C;&#x53EB; XHR&#x3002;</p>
<p>&#x9084;&#x53EF;&#x4EE5;&#x62FF;&#x4F86;&#x9019;&#x6A23;&#x7528;&#xFF1A;</p>
<pre><code>&lt;!-- &quot;The sum of 1 + 1 is 2&quot; --&gt;
&lt;p&gt;The sum of 1 + 1 is {{1 + 1}}&lt;/p&gt;
</code></pre>
<h2>Two Way Binding</h2>
<p>&#x9867;&#x540D;&#x601D;&#x7FA9;&#xFF0C;&#x5C31;&#x662F;&#x524D;&#x5F8C;&#x90FD;&#x80FD;&#x5F7C;&#x6B64;&#x63A7;&#x5236;&#x5C0D;&#x65B9;&#xFF0C;&#x66F4;&#x767D;&#x8A71;&#x4E00;&#x9EDE;&#x5C31;&#x662F;&#x7A0B;&#x5F0F;&#x53EF;&#x4EE5;&#x63A7;&#x5236;&#x986F;&#x793A;&#xFF0C;&#x986F;&#x793A;&#x7684;&#x5730;&#x65B9;&#x4E5F;&#x53EF;&#x4EE5;&#x5229;&#x7528;&#x6309;&#x9215;&#x3001;&#x8F38;&#x5165;&#x7B49;&#x65B9;&#x5F0F;&#x6539;&#x8B8A;&#x6578;&#x64DA;&#x3002;<br>
&#x53EF;&#x80FD;&#x5C31;&#x6703;&#x9577;&#x5F97;&#x50CF;&#x9019;&#x6A23;&#xFF1B;</p>
<pre><code>&lt;my-sizer [(size)]=&quot;fontSizePx&quot;&gt;&lt;/my-sizer&gt;
&lt;div [style.font-size.px]=&quot;fontSizePx&quot;&gt;Resizable Text&lt;/div&gt;
</code></pre>
<p><code>my-sizer</code> &#x96D9;&#x5411;&#x7D81;&#x5B9A;&#xFF0C;&#x4E0D;&#x7BA1;&#x662F;&#x6578;&#x64DA;&#x4F86;&#x6E90;&#x6539;&#x8B8A;&#x9084;&#x662F;&#x4ECB;&#x9762;&#x7531;&#x4F7F;&#x7528;&#x8005;&#x6539;&#x8B8A;&#xFF0C;&#x800C;&#x4E0B;&#x9762;&#x7684;&#x7684; <code>div</code> &#x5247;&#x6703;&#x53D7;&#x5230;&#x6539;&#x8B8A;&#x3002;</p>
<h3>NgModal</h3>
<p>&#x7576;&#x6709; <code>Input</code>&#x3001;<code>Select</code> &#x7684;&#x6642;&#x5019; <code>NgModal</code> &#x53EF;&#x4EE5;&#x6709;&#x6548;&#x9023;&#x7D50;&#x7D81;&#x5B9A; Component &#x7684;&#x6578;&#x64DA;&#x3002;<br>
&#x76F4;&#x63A5;&#x4F86;&#x770B;&#x770B;&#x7BC4;&#x4F8B;&#x5427;&#xFF1A;</p>
<pre><code>&lt;div&gt;
  &lt;h4&gt;Select Account&lt;/h4&gt;
  &lt;select [(ngModel)]=&quot;selectedAccount&quot; (ngModelChange)=&quot;selectAccount()&quot;&gt;
    &lt;option *ngFor=&quot;let account of accounts&quot; [ngValue]=&quot;account&quot;&gt;{{account.name}}&lt;/option&gt;
  &lt;/select&gt;
&lt;/div&gt;
</code></pre>
<p><code>*ngFor</code> &#x6703;&#x986F;&#x793A; <code>accounts: array</code> &#x4E2D;&#x6240;&#x6709;&#x7684; <code>account</code>&#xFF0C;&#x88AB;&#x9078;&#x53D6;&#x7684;&#x9078;&#x9805;&#xFF0C;&#x900F;&#x904E; <code>[ngValue]</code> &#x56DE;&#x50B3;&#x503C;&#xFF0C;&#x56E0;&#x70BA;<code>&lt;select&gt;</code> &#x5DF2;&#x7D93;&#x548C; <code>[(ngModal)]</code> &#x7D81;&#x5B9A;&#xFF0C;&#x6240;&#x4EE5; <code>[(ngModal)]</code> &#x5F97;&#x5230; <code>[ngValue]</code> &#x7684;&#x503C;&#xFF0C;&#x4E26;&#x548C; Component &#x4E2D;&#x7684; <code>selectedAccount</code> &#x505A;&#x96D9;&#x5411;&#x7D81;&#x5B9A;&#x3002;<br>
&#x751A;&#x9EBC;&#x610F;&#x601D;&#x5462;&#xFF0C;&#x5C31;&#x662F;&#x8AAA;&#x4F60;&#x62C9;&#x4E0B;&#x9078;&#x55AE;&#x9078;&#x67D0;&#x500B;&#x9078;&#x9805;&#x6642;&#x5019;&#xFF0C; Component &#x4E2D;&#x7684; <code>selectedAccount</code> &#x4E5F;&#x8DDF;&#x8457;&#x9078;&#x9805;&#x6539;&#x8B8A;&#x4ED6;&#x7684;&#x503C;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
