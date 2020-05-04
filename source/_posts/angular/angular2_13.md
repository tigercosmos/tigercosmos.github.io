---
title: Angular 2 + <ng-content> 嵌入式設計靈活組織 HTML
date: 2016-12-29 23:49:13
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x5D4C;&#x5165;&#x5F0F;&#x8A2D;&#x8A08;&#x5C31;&#x662F;&#x5C07; B &#x7684;&#x5167;&#x5BB9;&#x5D4C;&#x5165;&#x9032;&#x53BB; A &#xFF0C;A &#x6587;&#x4EF6;&#x4E2D;&#x9810;&#x7559;&#x4E00;&#x500B;&#x7A7A;&#x9593;&#x5C31;&#x662F;&#x7559;&#x7D66; B &#x653E;&#x6771;&#x897F;&#x7528;&#x7684;&#x3002;&#x5927;&#x6982;&#x5C31;&#x9577;&#x9019;&#x6A23;&#xFF1A;<br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/59/Transclusion_simple.svg/250px-Transclusion_simple.svg.png" alt><br>
&#x597D;&#x8655;&#x8DDF;&#x6A21;&#x677F;&#x985E;&#x4F3C;&#xFF0C;&#x53EF;&#x4EE5;&#x5728;&#x505A;&#x8A2D;&#x8A08;&#x6642;&#x6709;&#x66F4;&#x660E;&#x78BA;&#x7684;&#x908F;&#x8F2F;&#xFF0C;&#x6709;&#x4E9B;&#x5730;&#x65B9;&#x6211;&#x5011;&#x4E0D;&#x6703;&#x53BB;&#x66F4;&#x52D5;&#xFF0C;&#x800C;&#x8981;&#x66F4;&#x52D5;&#x7684;&#x5730;&#x65B9;&#x5C31;&#x7528;&#x5D4C;&#x5165;&#x7684;&#x65B9;&#x5F0F;&#x653E;&#x9032;&#x53BB;&#xFF0C;&#x5982;&#x6B64;&#x4E00;&#x4F86;&#x6574;&#x9AD4;&#x6587;&#x4EF6;&#x770B;&#x8D77;&#x4F86;&#x81EA;&#x7136;&#x6703;&#x6BD4;&#x8F03;&#x7C21;&#x6F54;&#xFF0C;&#x800C;&#x5D4C;&#x5165;&#x7684;&#x90E8;&#x5206;&#x7368;&#x7ACB;&#x51FA;&#x4F86;&#x4E4B;&#x5F8C;&#x4E5F;&#x597D;&#x7DAD;&#x8B77;&#x3002;</p>
<h2>&#x85CD;&#x5716;</h2>
<p>&#x6211;&#x5011;&#x5C07;&#x8A2D;&#x8A08;&#x4E00;&#x500B;&#x4E2D;&#x9593;&#x5167;&#x5BB9;&#x53EF;&#x4EE5;&#x5D4C;&#x5165;&#x7684;&#x5361;&#x7247; Component &#x4F86;&#x5C55;&#x793A;&#x5D4C;&#x5165;&#x7684;&#x6548;&#x679C;&#xFF0C;&#x53EF;&#x4EE5;&#x5148;&#x770B;&#x770B;&#x6210;&#x679C;&#xFF1A; <a href="https://plnkr.co/edit/65ppwcouDS7IL762lduG?p=preview" target="_blank">Plunker</a></p>
<pre><code>|- app/
    |- app.component.html
    |- app.component.ts
    |- app.module.ts
    |- card.component.ts
    |- card.component.html
    |- main.ts
|- index.html
|- systemjs.config.js
|- tsconfig.json
</code></pre>
<h2>&#x52D5;&#x5DE5;&#x56C9;</h2>
<h3>&#x5361;&#x7247;&#x7D44;&#x4EF6;</h3>
<p>&#x4E00;&#x500B;&#x5361;&#x7247;&#x5206;&#x70BA;&#xFF1A;&#x982D;&#x3001;&#x8EAB;&#x9AD4;&#x3001;&#x8173;&#x3002;&#x6211;&#x5011;&#x5C07;&#x628A;&#x8EAB;&#x9AD4;&#x8B8A;&#x6210;&#x5D4C;&#x5165;&#x7684;&#x3002;</p>
<pre><code>// card.component.ts

import { Component, Input, Output } from &apos;@angular/core&apos;;
@Component({
  selector: &apos;card&apos;,
  templateUrl: &apos;card.component.html&apos;,
})
export class CardComponent {
    @Input() header: string = &apos;this is header&apos;;   
    @Input() footer: string = &apos;this is footer&apos;;
}
</code></pre>
<p><code>@Input()</code>&#x4EE3;&#x8868;&#x53EF;&#x4EE5;&#x5F9E; parent &#x50B3;&#x7D66; child&#x3002;</p>
<h3>&#x5361;&#x7247;&#x6A21;&#x677F;</h3>
<pre><code>&lt;!-- card.component.html --&gt;

&lt;div class=&quot;card&quot;&gt;
    &lt;div class=&quot;card-header&quot;&gt;
        {{ header }}
    &lt;/div&gt;

    &lt;!-- &#x55AE;&#x4E00;&#x5D4C;&#x5165;&#x9EDE; --&gt;
    &lt;ng-content&gt;&lt;/ng-content&gt;

    &lt;div class=&quot;card-footer&quot;&gt;
        {{ footer }}
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>
<p><code>&lt;ng-content&gt;</code>&#x5C31;&#x662F;&#x6211;&#x5011;&#x5D4C;&#x5165;&#x6771;&#x897F;&#x7684;&#x5730;&#x65B9;&#x3002;</p>
<h2>&#x4F7F;&#x7528;</h2>
<p>&#x63A5;&#x8457;&#x6211;&#x5011;&#x5C31;&#x53EF;&#x4EE5;&#x5728;&#x5176;&#x4ED6;&#x5730;&#x65B9;&#x4F7F;&#x7528;&#x5361;&#x7247;&#x4E86;</p>
<pre><code>&lt;!-- app.component.html --&gt;

&lt;h1&gt;Single slot transclusion&lt;/h1&gt;
&lt;card header=&quot;my header&quot; footer=&quot;my footer&quot;&gt;
  &lt;!-- &#x653E;&#x5165;&#x8981;&#x5D4C;&#x5165;&#x7684;&#x52D5;&#x614B;&#x5167;&#x5BB9; --&gt;
  &lt;div class=&quot;card-block&quot;&gt;
    &lt;h4 class=&quot;card-title&quot;&gt;You can put any content here&lt;/h4&gt;
    &lt;p class=&quot;card-text&quot;&gt;For example this line of text and&lt;/p&gt;
    &lt;a href=&quot;#&quot; class=&quot;btn btn-primary&quot;&gt;This button&lt;/a&gt;
  &lt;/div&gt;
  &lt;!-- &#x7D50;&#x675F; --&gt;
&lt;card&gt;
</code></pre>
<p>&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x5728; <code>AppComponent</code> &#x76F4;&#x63A5;&#x4F7F;&#x7528; <code>card</code>&#x3002;<code>&lt;card&gt;</code> &#x88E1;&#x9762;&#x653E;&#x5165;&#x6211;&#x5011;&#x8981;&#x7684;&#x5167;&#x5BB9;&#xFF0C;&#x5C31;&#x6703;&#x81EA;&#x5DF1;&#x5D4C;&#x5165;&#x9032; <code>card</code> &#x4E86;&#x3002;</p>
<h3>App Module</h3>
<p>&#x8A18;&#x5F97;&#x8A2D;&#x5B9A; app module</p>
<pre><code>import { NgModule }      from &apos;@angular/core&apos;;
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { AppComponent }   from &apos;./app.component&apos;;
import { CardComponent } from &apos;./card.component&apos;; // &#x8A18;&#x5F97;&#x52A0;&#x5165;

@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent, CardComponent ], // &#x6CE8;&#x5165;
  bootstrap:    [ AppComponent ],
})

export class AppModule { }
</code></pre>
<h2>&#x5176;&#x4ED6;&#x65B9;&#x6CD5;</h2>
<ul>
<li>&#x53EF;&#x4EE5;&#x900F;&#x904E; Atrribute</li>
</ul>
<pre><code>&lt;!-- card.component.html --&gt;
...
&lt;!--  ng-content &#x4E2D;&#x52A0;&#x5165; select attribute  --&gt;
&lt;ng-content select=&quot;[card-body]&quot;&gt;&lt;/ng-content&gt;
...
</code></pre>
<pre><code>&lt;!-- app.component.html --&gt;
&lt;card header=&quot;my header&quot; footer=&quot;my footer&quot;&gt;
    &lt;div class=&quot;card-block&quot; card-body&gt;&lt;!--  &#x589E;&#x52A0; card-body &#x5C6C;&#x6027; --&gt;
    ...
    &lt;/div&gt;
&lt;card&gt;
</code></pre>
<ul>
<li>&#x53EF;&#x4EE5;&#x900F;&#x904E; attribute with value</li>
</ul>
<pre><code>&lt;!-- card.component.html --&gt;
...
&lt;ng-content select=&quot;[card-type=body]&quot;&gt;&lt;/ng-content&gt;
...
</code></pre>
<pre><code>&lt;!-- app.component.html --&gt;
...
&lt;div class=&quot;card-block&quot; card-type=&quot;body&quot;&gt;...&lt;div&gt;
...
</code></pre>
<ul>
<li>&#x4E5F;&#x53EF;&#x4EE5;&#x900F;&#x904E; class</li>
</ul>
<pre><code>&lt;!-- card.component.html --&gt;
...
&lt;ng-content select=&quot;.card-body&quot;&gt;&lt;/ng-content&gt;
...
</code></pre>
<pre><code>&lt;!-- app.component.html --&gt;
...
&lt;div class=&quot;card-block card-body&quot;&gt;...&lt;/div&gt;
...
</code></pre>
<ul>
<li>&#x7576;&#x7136;&#x4E5F;&#x53EF;&#x4EE5;&#x540C;&#x6642;&#x6709;&#x591A;&#x500B; Atrribute &#x6216; CSS Class</li>
</ul>
<pre><code>&lt;!-- card.component.html --&gt;
...
&lt;ng-content select=&quot;[card][body]&quot;&gt;&lt;/ng-content&gt;
...
</code></pre>
<pre><code>&lt;!-- app.component.html --&gt;
...
&lt;div class=&quot;card-block&quot; body card&gt;...&lt;/div&gt;
...
</code></pre>
<ul>
<li>HTML Tag &#x4E5F;&#x53EF;&#x4EE5;&#xFF0C;&#x4F46;&#x8981;&#x591A;&#x8A2D;&#x5B9A;&#x4E00;&#x4E9B;&#x6771;&#x897F;</li>
</ul>
<pre><code>&lt;!-- card.component.html --&gt;
...
&lt;ng-content select=&quot;card-body&quot;&gt;&lt;/ng-content&gt;
...
</code></pre>
<pre><code>&lt;!-- app.component.html --&gt;
...
&lt;card-body class=&quot;card-block&quot;&gt;...&lt;card-body&gt;
...
</code></pre>
<p>&#x9019;&#x908A;&#x8981;&#x8A2D;&#x5B9A; <code>NO_ERRORS_SCHEMA</code>&#xFF0C;&#x4E0D;&#x7136;&#x6703;&#x51FA;&#x932F;</p>
<pre><code>// app.module.ts

import { NgModule, NO_ERRORS_SCHEMA }      from &apos;@angular/core&apos;; //
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { AppComponent }   from &apos;./app.component&apos;;
import { CardComponent } from &apos;./card.component&apos;;

@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent, CardComponent ],
  bootstrap:    [ AppComponent ],
  schemas:      [ NO_ERRORS_SCHEMA ] // &#x589E;&#x52A0;&#x9019;&#x884C;
})

export class AppModule { }
</code></pre>
<h2>&#x591A;&#x9EDE;&#x5D4C;&#x5165;</h2>
<p>&#x9664;&#x4E86;&#x55AE;&#x4E00;&#x9EDE;&#x5D4C;&#x5165;&#xFF0C;&#x591A;&#x9EDE;&#x5D4C;&#x5165;&#x7576;&#x7136;&#x4E5F;&#x53EF;&#x4EE5;</p>
<pre><code>&lt;!-- card.component.html --&gt;

&lt;div class=&quot;card&quot;&gt;
    &lt;div class=&quot;card-header&quot;&gt;
    &lt;!-- header slot here --&gt;
        &lt;ng-content select=&quot;card-header&quot;&gt;&lt;/ng-content&gt;
    &lt;/div&gt;
    &lt;!-- body slot here --&gt;
    &lt;ng-content select=&quot;card-body&quot;&gt;&lt;/ng-content&gt;
    &lt;div class=&quot;card-footer&quot;&gt;
    &lt;!-- footer --&gt;
        &lt;ng-content select=&quot;card-footer&quot;&gt;&lt;/ng-content&gt;
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>
<pre><code>&lt;!-- app.component.html --&gt;

&lt;h1&gt;Multi slot transclusion&lt;/h1&gt;
&lt;card&gt;
    &lt;!-- header --&gt;
    &lt;card-header&gt;
        New &lt;strong&gt;header&lt;/strong&gt;
    &lt;/card-header&gt;

    &lt;!-- body --&gt;
    &lt;card-body&gt;
        &lt;div class=&quot;card-block&quot;&gt;
            &lt;h4 class=&quot;card-title&quot;&gt;You can put any content here&lt;/h4&gt;
            &lt;p class=&quot;card-text&quot;&gt;For example this line of text and&lt;/p&gt;
            &lt;a href=&quot;#&quot; class=&quot;btn btn-primary&quot;&gt;This button&lt;/a&gt;
          &lt;/div&gt;
    &lt;/card-body&gt;

    &lt;!-- footer --&gt;
    &lt;card-footer&gt;
        New &lt;strong&gt;footer&lt;/strong&gt;
    &lt;/card-footer&gt;
&lt;card&gt;
</code></pre>
<h2>&#x7E3D;&#x7D50;</h2>
<p>&#x54EA;&#x4E00;&#x7A2E;&#x5D4C;&#x5165;&#x65B9;&#x5F0F;&#x6700;&#x597D;&#x5462;&#xFF1F;&#x5176;&#x5BE6;&#x55AE;&#x770B;&#x5927;&#x5BB6;&#x559C;&#x597D;&#x56C9;&#xFF01;&#x53EA;&#x662F;&#x5982;&#x679C;&#x7528; Atrribute &#x548C; HTML Tag &#x5C0D;&#x65BC;&#x95B1;&#x8B80;&#x7A0B;&#x5F0F;&#x78BC;&#x4F86;&#x8AAA;&#x662F;&#x6700;&#x53CB;&#x5584;&#x7684;&#xFF0C;&#x4F46;&#x662F; Tag &#x53C8;&#x5FC5;&#x9808;&#x591A;&#x52A0;&#x8A2D;&#x5B9A;&#xFF0C;&#x5176;&#x5BE6;&#x6709;&#x9EDE;&#x9EBB;&#x7169;&#xFF0C;&#x6700;&#x4F73;&#x9078;&#x64C7;&#x61C9;&#x8A72;&#x5C31;&#x662F; Atrribute &#x4E86; XD</p>
 <br>
                                                    </div>
                    </div>
                
