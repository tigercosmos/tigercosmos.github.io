---
title: Angular 2 Lazy Loading 別讓載入速度拖垮你！
date: 2016-12-23 23:49:56
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<blockquote>
<p>Lazy loading &#x662F;&#x6307;&#x5F9E;&#x4E00;&#x500B;&#x8CC7;&#x6599;&#x7269;&#x4EF6;&#x901A;&#x904E;&#x65B9;&#x6CD5;&#x7372;&#x5F97;&#x88E1;&#x9762;&#x7684;&#x4E00;&#x500B;&#x5C6C;&#x6027;&#x7269;&#x4EF6;&#x6642;&#xFF0C;&#x9019;&#x500B;&#x5C0D;&#x61C9;&#x7269;&#x4EF6;&#x5BE6;&#x969B;&#x4E26;&#x6C92;&#x6709;&#x96A8;&#x5176;&#x7236;&#x8CC7;&#x6599;&#x7269;&#x4EF6;&#x5EFA;&#x7ACB;&#x6642;&#x4E00;&#x8D77;&#x5132;&#x5B58;&#x5728;&#x57F7;&#x884C;&#x7A7A;&#x9593;&#x4E2D;&#xFF0C;&#x800C;&#x662F;&#x5728;&#x5176;&#x8B80;&#x53D6;&#x65B9;&#x6CD5;&#x7B2C;&#x4E00;&#x6B21;&#x88AB;&#x547C;&#x53EB;&#x6642;&#x624D;&#x5F9E;&#x5176;&#x4ED6;&#x8CC7;&#x6599;&#x4F86;&#x6E90;&#x4E2D;&#x8F09;&#x5165;&#x5230;&#x57F7;&#x884C;&#x7A7A;&#x9593;&#x4E2D;&#xFF0C;&#x9019;&#x6A23;&#x53EF;&#x4EE5;&#x907F;&#x514D;&#x904E;&#x65E9;&#x5730;&#x532F;&#x5165;&#x904E;&#x5927;&#x7684;&#x8CC7;&#x6599;&#x7269;&#x4EF6;&#x4F46;&#x4E26;&#x6C92;&#x6709;&#x4F7F;&#x7528;&#x7684;&#x7A7A;&#x9593;&#x5360;&#x7528;&#x6D6A;&#x8CBB;&#x3002;</p>
</blockquote>
<p>Lazy loading &#x5728;&#x8F09;&#x5165;&#x975E;&#x5E38;&#x591A;&#x4E0D;&#x540C;&#x5167;&#x5BB9;&#x6642;&#x975E;&#x5E38;&#x6709;&#x611F;&#x3002;&#x7576;&#x4E00;&#x500B;&#x7DB2;&#x7AD9;&#x5305;&#x542B;&#x7684;&#x6771;&#x897F;&#x8D8A;&#x591A;&#xFF0C;&#x958B;&#x555F;&#x7684;&#x901F;&#x5EA6;&#x4E5F;&#x6703;&#x8D8A;&#x6162;&#xFF0C;&#x7576;&#x7DB2;&#x9801;&#x5F9E;&#x4E0A;&#x5230;&#x4E0B;&#x8B80;&#x53D6;&#xFF0C;&#x7576;&#x9047;&#x5230;&#x4E86;&#x6BD4;&#x8F03;&#x5927;&#x7684;&#x5143;&#x4EF6;&#x6642;&#xFF0C;&#x8B80;&#x53D6;&#x901F;&#x5EA6;&#x4E0A;&#x7D55;&#x4E0D;&#x6703;&#x50CF;&#x8B80;&#x53D6;&#x5C0F;&#x5143;&#x4EF6;&#x4E00;&#x6A23;&#x9806;&#x66A2;&#xFF0C;&#x5E38;&#x5E38;&#x56E0;&#x70BA;&#x6240;&#x542B;&#x7684;&#x7D44;&#x4EF6;&#x592A;&#x591A;&#xFF0C;&#x5C0E;&#x81F4;&#x7DB2;&#x7AD9;&#x8B80;&#x53D6;&#x901F;&#x5EA6;&#x8B8A;&#x6162;&#xFF0C;&#x9019;&#x7DB2;&#x7AD9;&#x771F;&#x7684;&#x662F;&#x5403;&#x4E86;&#x60B6;&#x8667;&#x3002;&#x90A3;&#x662F;&#x5426;&#x6709;&#x8FA6;&#x6CD5;&#x6539;&#x5584;&#x9019;&#x7A2E;&#x56E0;&#x70BA;&#x8B80;&#x53D6;&#x901F;&#x5EA6;&#x800C;&#x9020;&#x6210;&#x7DB2;&#x7AD9;&#x958B;&#x555F;&#x592A;&#x6162;&#x7684;&#x554F;&#x984C;&#x5462;&#xFF1F;</p>
<h2>&#x5BE6;&#x73FE;</h2>
<p>Angular2 &#x4E2D; &#xFF0C; lazy loading &#x5DF2;&#x7D93;&#x88AB;&#x5EFA;&#x5728; Router &#x88E1;&#x4E86;&#x3002; &#x63A5;&#x4E0B;&#x4F86;&#x8981;&#x82B1;&#x5E7E;&#x500B;&#x6B65;&#x9A5F;&#xFF1A;</p>
<ul>
<li>&#x6307;&#x5B9A; app.routing.ts &#x4E2D;&#x8981; lazy load &#x7684;&#x8DEF;&#x7531; (routes)</li>
<li>&#x5EFA;&#x7ACB; Component &#x8DEF;&#x7531;&#x6587;&#x4EF6;</li>
<li>&#x8ABF;&#x6574;&#x8981;&#x88AB; lazy load &#x7684; module &#x7684;&#x5167;&#x5BB9;</li>
</ul>
<h2>&#x8DEF;&#x5F91;&#x7269;&#x4EF6;</h2>
<p>&#x70BA;&#x4E86;&#x5340;&#x5206; lazy loading&#xFF0C;&#x6211;&#x5011;&#x8981;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x8DEF;&#x5F91;&#x7269;&#x4EF6;&#x5305;&#x542B; <code>loadChildren</code> &#x7279;&#x6027;&#x3002;&#x5728;&#x9019;&#x7269;&#x4EF6;&#x88E1;&#x9762;&#x8981;&#x8A2D;&#x5B9A; module &#x7684;&#x540D;&#x7A31;&#x548C;&#x8DEF;&#x5F91;&#x3002;</p>
<pre><code>//app.routes.ts

import {Routes, RouterModule} from &quot;@angular/router&quot;;
import {ModuleWithProviders} from &quot;@angular/core&quot;;

const appRoutes: Routes  = [
    // &#x5047;&#x8A2D;&#x6709;&#x9996;&#x9801;
    { path: &quot;&quot;, redirectTo: &quot;home&quot;, pathMatch: &quot;full&quot; },
    
    // &#x8981;&#x8655;&#x7406;&#x7684; Product APP &#x9801;&#x9762;
    { path: &quot;product&quot;, loadChildren: &quot;app/product/product.module#ProductModule&quot;  }
];

export const routing: ModuleWithProviders  = RouterModule.forRoot(appRoutes);
</code></pre>
<p>&#x9019;&#x6A23;&#x4EE3;&#x8868; URL &#x6703;&#x5F9E; <code>/product</code> &#x958B;&#x59CB;&#xFF0C; angular &#x8DEF;&#x7531;&#x5C07;&#x6703;&#x5F97;&#x5230; module &#x6A94;&#x6848; <code>app/product/product.module</code> &#x4E26;&#x9810;&#x671F;&#x6709; <code>ProductModule</code> &#x9019;&#x500B; class&#x3002;</p>
<h2>&#x8DEF;&#x7531; Module</h2>
<pre><code>//product/product.routing.ts

import {RouterModule} from &quot;@angular/router&quot;;
import {ModuleWithProviders} from &quot;@angular/core&quot;;
import {ProductComponent} from &quot;./product.component&quot;;
// &#x5C0F;&#x96F6;&#x4EF6; ( &#x5404;&#x7A2E;&#x7528;&#x5230;&#x7684;&#x6771;&#x897F; )
import {ProductsListComponent} from &quot;./products-list.component&quot;;
import {ProductDetailsComponent} from &quot;./product-details.component&quot;;

const routes = [
    {
        path: &quot;&quot;, //&#x8A2D;&#x5B9A;&#x6839;&#x76EE;&#x9304;&#x70BA;&#x9019;&#x4E00;&#x5C64;
        component: ProductComponent,
        // Product &#x5305;&#x542B;&#x7684;&#x5C0F;&#x7D44;&#x4EF6;&#x5011;
        children: [
            {path: &quot;&quot;, component: ProductsListComponent},
            {path: &quot;:id&quot;, component: ProductDetailsComponent}
        ]
    }
];

export const routing: ModuleWithProviders = RouterModule.forChild(routes);
</code></pre>
<h2>&#x8A2D;&#x5B9A; Component</h2>
<p>&#x5B9A;&#x7FA9; <code>ProductComponent</code></p>
<pre><code>//product/product.component.ts
import {Component} from &quot;@angular/core&quot;;

@Component({
    template: `
        &lt;my-nav&gt;&lt;/my-nav&gt;
        &lt;h1&gt;Products&lt;/h1&gt;
        &lt;router-outlet&gt;&lt;/router-outlet&gt;
    `
})
export class ProductComponent {}
</code></pre>
<p><code>router-outlet</code> &#x6703;&#x5448;&#x73FE;&#x9019;&#x500B; module &#x5167;&#x5BB9;</p>
<h2>&#x6709; Lazy Load &#x7684; Module</h2>
<pre><code>//product/product.module.ts

import {NgModule} from &quot;@angular/core&quot;;
import {ProductsService} from &quot;./products.service&quot;;
import {ProductsListComponent} from &quot;./products-list.component&quot;;
import {ProductDetailsComponent} from &quot;./product-details.component&quot;;
import {routing} from &quot;./product.routing&quot;;
import {ProductComponent} from &quot;./product.component&quot;;

@NgModule({
    declarations: [ProductComponent, ProductsListComponent, ProductDetailsComponent],
    imports: [routing],
    providers: [ProductsService],
})
export class ProductModule {}
</code></pre>
<p>&#x9019;&#x908A;&#x6703;&#x7528;&#x5230; <code>product.routing</code> &#x7684; <code>routing</code>&#x3002;</p>
<h2>&#x6E2C;&#x8A66;</h2>
<p>&#x5047;&#x8A2D;&#x4F60;&#x7684;&#x7DB2;&#x7AD9;&#x6709;&#x4E09;&#x500B; Module: <code>home</code> <code>project</code> <code>about</code><br>
&#x90A3;&#x52A0;&#x5165; lazy loading &#x7684;&#x524D;&#x5F8C;&#x5DEE;&#x7570;&#x5927;&#x6982;&#x6703;&#x662F;&#x9019;&#x6A23;<br>
&#x52A0;&#x5165;&#x524D;<br>
<img src="https://devblog.dymel.pl/images/posts/2016-10-06-lazy-loading-angular2-modules/loading-stats.png" alt><br>
&#x52A0;&#x5165;&#x5F8C;<br>
<img src="https://devblog.dymel.pl/images/posts/2016-10-06-lazy-loading-angular2-modules/lazy-loading-stats.png" alt><br>
&#x539F;&#x56E0;&#x662F;&#x56E0;&#x70BA;&#x52A0;&#x5165; lazy loading &#x6240;&#x4EE5;&#x6703;&#x5148;&#x53EA;&#x8F09;&#x5165; <code>home</code> &#x6839; <code>about</code>&#xFF0C;&#x5728;&#x9019;&#x908A;&#x6211;&#x5011;&#x5047;&#x8A2D;&#x4ED6;&#x5011;&#x5169;&#x500B;&#x975E;&#x5E38;&#x8F15;&#x91CF;&#xFF0C;&#x90A3;&#x5C31;&#x6703;&#x4F7F;&#x5F97;&#x6574;&#x500B;&#x7DB2;&#x9801;&#x8F09;&#x5165;&#x7684;&#x9806;&#x66A2;&#x5EA6;&#x6574;&#x9AD4;&#x63D0;&#x5347;&#xFF0C;&#x800C;&#x6BD4;&#x8F03;&#x5927;&#x7684; <code>project</code> &#x5247;&#x5728;&#x4E4B;&#x5F8C;&#x8F09;&#x5165;&#xFF0C;&#x5C31;&#x4E0D;&#x6703;&#x62D6;&#x57AE;&#x901F;&#x5EA6;&#x4E86;&#xFF01;</p>
<h2>&#x88DC;&#x5145;&#xFF1A;&#x6A21;&#x677F;&#x8F09;&#x5165;&#x7D44;&#x4EF6;</h2>
<h3>&#x65B9;&#x5F0F;</h3>
<p>&#x5047;&#x8A2D;&#x6709;&#x5169;&#x500B; Components <code>fast</code> &amp; <code>slow</code></p>
<pre><code>//src/components/fast.ts
import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;fast&apos;,
  template: `
    &lt;p&gt;Fast Content&lt;/p&gt;
  `
})

export class FastComponent { }
</code></pre>
<pre><code>//src/components/slow.ts
import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;slow&apos;,
  template: `
    &lt;p&gt;Slow Content&lt;/p&gt;
  `
})

export class SlowComponent { }
</code></pre>
<p>&#x5728; Template &#x88E1;&#x9762;&#x8F09;&#x5165; Component &#x662F;&#x6700;&#x5E38;&#x7528;&#x8F09;&#x5165;&#x65B9;&#x5F0F;&#x3002;&#x975E;&#x5E38;&#x7C21;&#x55AE;&#xFF0C;&#x53EA;&#x9700;&#x8981;&#x5B58;&#x653E;&#x76F8;&#x61C9;&#x7684; <code>selector</code> &#xFF0C;&#x6A21;&#x677F;&#x5F15;&#x64CE;&#x5C31;&#x6703;&#x81EA;&#x5DF1;&#x627E;&#x5230;&#x4E26;&#x7DE8;&#x8B6F;&#x3002;</p>
<pre><code>//app.component.ts
import {Component} from &apos;@angular/core&apos;

import {FastComponent} from &apos;src/components/fast&apos;
import {SlowComponent} from &apos;src/components/slow&apos;

@Component({
  selector: &apos;template-load&apos;,
  template: `
      &lt;h1&gt;&#x65B9;&#x5F0F;&#x4E00;&#xFF1A;template &#x52D5;&#x614B;&#x8F09;&#x5165;&lt;/h1&gt;
      &lt;fast&gt;&lt;/fast&gt;
      &lt;slow&gt;&lt;/slow&gt;
  `,
  directives: [ FastComponent, SlowComponent ]
})
export class TemplateLoadComponent {
  constructor() {

  }
}
</code></pre>
 <br>
                                                    </div>
                    </div>
                
