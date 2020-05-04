---
title: 當個好的建築師之 Angular 2 架構
date: 2016-12-18 23:51:18
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>Angular 2 &#x67B6;&#x69CB;</h2>
<p>Angular 2 &#x4E3B;&#x8981;&#x7684;&#x5143;&#x7D20;&#x662F; Components&#x3002; Angular 2 &#x7684;&#x4E3B;&#x8981;&#x67B6;&#x69CB;&#x5C31;&#x662F;&#x4E00;&#x5806;&#x7684; Components&#x3002;&#x4E0D;&#x904E;&#x7576;&#x7136;&#xFF0C;&#x7D44;&#x6210; Angular&#x7684;&#x6771;&#x897F;&#x9084;&#x5305;&#x542B; Module&#x3001;Template&#x3001;Metadata&#x3001;Data Binding&#x3001;Service&#x3001;Directive&#x3001;Dependency Injection&#xFF0C;&#x5F9E;&#x4E0B;&#x9762;&#x9019;&#x5F35;&#x5716;&#x53EF;&#x4EE5;&#x6E05;&#x695A;&#x770B;&#x5230;&#x5F7C;&#x6B64;&#x7684;&#x95DC;&#x4FC2;&#x3002;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-overview.png" alt></p>
<h2>&#x958B;&#x59CB;&#x756B;&#x8A2D;&#x8A08;&#x5716;&#x56C9;</h2>
<h3>Component</h3>
<p>Component &#x662F;&#x4E00;&#x500B;&#x7528; TS &#x5BEB;&#x51FA;&#x4F86;&#x7684; Class&#xFF0C;&#x9019;&#x500B; Class &#x4E4B;&#x5F8C;&#x6703;&#x88AB;&#x7DE8;&#x8B6F;&#x6210; JS&#x3002;&#x800C;&#x9019;&#x4E9B; Component &#x6700;&#x5F8C;&#x53EF;&#x4EE5;&#x88AB;&#x5305;&#x88DD;&#x8B8A;&#x6210;&#x7368;&#x7ACB;&#x7684; Module &#x8B93;&#x5176;&#x4ED6; Mudule &#x4F7F;&#x7528;&#x3002;</p>
<p>&#x4E00;&#x500B; Component&#x53EF;&#x80FD;&#x9577;&#x5F97;&#x50CF;&#x9019;&#x6A23;&#xFF1A;</p>
<pre><code>//app.component.ts
import { Component } from &apos;@angular/core&apos;;

@Component({
  moduleId: module.id,
  selector: &apos;my-app&apos;,
  templateUrl: &apos;app.component.html&apos;,
  styleUrls: [&apos;app.component.css&apos;]
})
export class AppComponent implements OnInit { 
    //Do Something
}
</code></pre>
<p>&#x800C;&#x4ED6;&#x8CA0;&#x8CAC;&#x5305;&#x88DD;&#x5B83;&#x7684; Module &#x5247;&#x53EF;&#x80FD;&#x9577;&#x9019;&#x6A23;&#xFF1A;</p>
<pre><code>//app.module.ts
import { NgModule }      from &apos;@angular/core&apos;;
import { AppComponent } from &apos;./app.component&apos;; //&#x5F15;&#x5165; Component
import { BrowserModule } from &apos;@angular/platform-browser&apos;;
@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
</code></pre>
<p>&#x4E00;&#x500B; Module&#x53EF;&#x4EE5;&#x5305;&#x88DD;&#x5F88;&#x591A; Component &#x7D66;&#x5176;&#x4ED6; Module &#x4F7F;&#x7528;&#x3002;</p>
<h3>Metadata</h3>
<p>&#x518D;&#x56DE;&#x4F86;&#x770B;&#x7C21;&#x55AE;&#x7684; Component&#xFF1A;</p>
<pre><code>import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;my-app&apos;,
  templateUrl: &apos;aa.component.html&apos;,
  styleUrls: [&apos;app.component.css&apos;]
})
export class AppComponent { name = &apos;Angular&apos;; }
</code></pre>
<p>Component &#x7528;&#x7A31;&#x4F5C; decorator function&#x7684; <code>@Component</code>&#x4F86;&#x8868;&#x793A;&#x70BA; Metadata&#x7269;&#x4EF6;&#x3002; Metadata &#x7528;&#x4F86;&#x7D81;&#x5B9A; HTML template &#x3001;CSS &#x548C; Component&#x3002;</p>
<p>&#x81F3;&#x65BC; <code>selector</code> &#x5247;&#x662F;&#x544A;&#x8A34; Angular &#x9019;&#x500B; Component &#x8981;&#x653E;&#x5728; <code>index.html</code> &#x88E1;&#x7684;&#x81EA;&#x8A02;&#x6A19;&#x7C64; <code>&lt;my-app&gt;</code>&#x3002;</p>
<pre><code>//index.html 
&lt;body&gt;
...
&lt;my-app&gt;Loading AppComponent content here ...&lt;/my-app&gt;
...
</code></pre>
<h3>Directive</h3>
<p>&#x5171;&#x6709;&#x4E09;&#x7A2E; Directive&#xFF1A;</p>
<ul>
<li>Components directives&#xFF1A; &#x7528;&#x4F86;&#x63A7;&#x5236; HTML Template&#x3002;&#x662F;&#x6211;&#x5011;&#x6700;&#x5E38;&#x7528;&#x5230;&#x7684; Directive&#x3002;</li>
<li>&#x7D50;&#x69CB;&#x6027; directives&#xFF1A;&#x4F8B;&#x5982; ngFor (&#x7528;&#x4F86;&#x6539;&#x8B8A; HTML DOM&#xFF0C;&#x53EF;&#x4EE5;&#x662F;&#x589E;&#x52A0;&#x6216;&#x522A;&#x6389;)<br>
<code>&lt;div *ngFor=&quot;let hero of heroes&quot;&gt;{{hero.fullName}}&lt;/div&gt;</code>
</li>
<li>&#x5C6C;&#x6027; directives&#xFF1A; &#x4F8B;&#x5982; ngStyle (&#x7528;&#x4F86;&#x6539;&#x8B8A; Elements &#x7684; Style)<br>
<code>&lt;p [style.background]=&quot;&apos;lime&apos;&quot;&gt;I am green with envy!&lt;/p&gt;</code>
</li>
</ul>
<p>&#x6211;&#x5011;&#x7528; Directives &#x4F86;&#x5C0D; Metadata &#x505A;&#x4E00;&#x4E9B;&#x529F;&#x80FD;&#x3002;</p>
<p>&#x81F3;&#x65BC;&#x5BE6;&#x969B;&#x600E;&#x9EBC;&#x7528;&#xFF0C;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;<code>@Directive</code>&#x6216;&#x662F;<code>@Component</code>&#x3002;&#x7C21;&#x55AE;&#x5340;&#x5206;&#x7684;&#x8A71;&#xFF1A;</p>
<ul>
<li>
<code>@Directive</code>&#x9069;&#x5408;&#x76F4;&#x63A5;&#x7528;&#x5728;&#x5DF2;&#x7D93;&#x5B58;&#x5728;&#x7684; DOM element&#x3002;&#x53EF;&#x4EE5;&#x91CD;&#x8907;&#x4F7F;&#x7528;&#xFF0C;&#x4E00;&#x500B; DOM element &#x53EF;&#x4EE5;&#x6709;&#x5F88; Directive&#x3002;</li>
<li>
<code>@Component</code>&#x9069;&#x5408;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x53EF;&#x4EE5;&#x91CD;&#x8907;&#x4F7F;&#x7528;&#x7684; DOM element&#xFF0C;&#x901A;&#x5E38;&#x7528;&#x4F86;&#x5EFA;&#x7ACB; UI&#x5DE5;&#x5177;&#xFF0C;&#x6B64;&#x5916;&#x4E00;&#x500B; DOM elelment &#x53EA;&#x80FD;&#x6709;&#x4E00;&#x500B; Component&#xFF0C;&#x800C;&#x4E14;&#x5FC5;&#x9808;&#x642D;&#x914D;<code>@View</code>&#x6216;&#x662F;<code>templateUrl</code>&#x3002;</li>
</ul>
<h3>Data Binding</h3>
<h4>Interpolation</h4>
<p>&#x76F4;&#x63A5;&#x5728; HTML &#x4E2D;&#x63D2;&#x5165;&#x8B8A;&#x6578;</p>
<pre><code>&lt;h1&gt;{{employee.name}}&lt;/h1&gt;  
</code></pre>
<h4>One Way Binding</h4>
<p>&#x53EF;&#x4EE5;&#x662F;&#x4EFB;&#x4F55; HTML property&#x3002;&#x50CF;&#x662F;<code>innerText</code> <code>style</code>&#x3002;</p>
<pre><code>&lt;h1 [innerText]=&quot;employee.name&quot;&gt;&lt;/h1&gt; 
</code></pre>
<pre><code>&lt;span [style.backgroundColor]=&quot;employee.favouriteColor&quot;&gt;&lt;/span&gt;
</code></pre>
<h4>Two Way Binding</h4>
<p>&#x53EF;&#x4EE5;&#x7531;&#x4F7F;&#x7528;&#x8005;&#x63A7;&#x5236;&#xFF0C;&#x50CF;&#x662F;&#x9078;&#x55AE;&#x3001;&#x8F38;&#x5165;&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x7531;&#x7A0B;&#x5F0F;&#x63A7;&#x5236;&#x3002;</p>
<pre><code>&lt;input [(ngModel)]=&quot;employee.name&quot;/&gt; 
</code></pre>
<h4>Event Binding</h4>
<p>&#x7D81;&#x5B9A;&#x4E8B;&#x4EF6;&#xFF0C;&#x50CF;&#x662F;<code>click</code>&#x3001;<code>focus</code>&#x6216;<code>blur</code></p>
<pre><code>&lt;button (click)=&quot;sendForm()&quot;&gt;Send&lt;/h1&gt;  
</code></pre>
 <br>
                                                    </div>
                    </div>
                
