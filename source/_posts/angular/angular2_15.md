---
title: Angular 2 Module ( 2 )
date: 2016-12-31 23:49:38
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<p>&#x63A5;&#x7E8C; <a href="https://ithelp.ithome.com.tw/articles/10188095" target="_blank">Angular 2 Module ( 1 )</a></p>
<h2>Feature Module</h2>
<p>Angular &#x4E00;&#x5B9A;&#x6703;&#x6709;&#x4E00;&#x500B; root module&#xFF0C;&#x4F46;&#x4F60;&#x4E5F;&#x53EF;&#x4EE5;&#x6709; feature module&#xFF0C;&#x63A5;&#x8457;&#x5C31;&#x4F86;&#x770B;&#x770B;&#x600E;&#x9EBC;&#x5EFA;&#x7ACB;&#x5427;&#xFF01;<br>
&#x63A5;&#x7E8C;&#x4E0A;&#x4E00;&#x7BC7;&#xFF0C;&#x5047;&#x8A2D;&#x6211;&#x5011;&#x4F9D;&#x820A;&#x6709;<code>CreditCardMaskPipe</code> &#x3001; <code>CreditCardService</code> &#x3001;<code>CreditCardComponent</code>&#xFF0C;&#x4F46;&#x6211;&#x5011;&#x4E0D;&#x60F3;&#x8981;&#x76F4;&#x63A5;&#x653E;&#x9032; root module&#xFF0C;&#x6211;&#x5011;&#x60F3;&#x8981;&#x518D;&#x5EFA;&#x7ACB;&#x4E00;&#x500B; module &#x4F86;&#x5305;&#x88DD;&#x9019;&#x4E9B;&#x6771;&#x897F;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x65B0;&#x7684; module &#x5C31;&#x662F; feature module &#x4E86;&#x3002;</p>
<p>&#x9996;&#x5148;&#x6211;&#x5011;&#x5148;&#x5275;&#x4E00;&#x500B;&#x65B0;&#x7684;&#x8CC7;&#x6599;&#x593E;&#x7D66;&#x65B0;&#x7684; module</p>
<pre><code>&#x251C;&#x2500;&#x2500; app
&#x2502;   &#x251C;&#x2500;&#x2500; app.component.ts
&#x2502;   &#x2514;&#x2500;&#x2500; app.module.ts
&#x251C;&#x2500;&#x2500; credit-card
&#x2502;   &#x251C;&#x2500;&#x2500; credit-card-mask.pipe.ts
&#x2502;   &#x251C;&#x2500;&#x2500; credit-card.component.ts
&#x2502;   &#x251C;&#x2500;&#x2500; credit-card.module.ts
&#x2502;   &#x2514;&#x2500;&#x2500; credit-card.service.ts
&#x251C;&#x2500;&#x2500; index.html
&#x2514;&#x2500;&#x2500; main.ts
</code></pre>
<p>&#x73FE;&#x5728;&#x6709;&#x5169;&#x500B;&#x8CC7;&#x6599;&#x593E;&#x88DD;&#x6709; module &#x4E86;&#xFF1A;<code>app.module.ts</code> &#x548C; <code>credit-card.module.ts</code></p>
<p>&#x5148;&#x770B;&#x770B;&#x5F8C;&#x8005;</p>
<pre><code>//credit-card/credit-card.module.ts

import { NgModule } from &apos;@angular/core&apos;;
import { CommonModule } from &apos;@angular/common&apos;;

import { CreditCardMaskPipe } from &apos;./credit-card-mask.pipe&apos;;
import { CreditCardService } from &apos;./credit-card.service&apos;;
import { CreditCardComponent } from &apos;./credit-card.component&apos;;

@NgModule({
  imports: [CommonModule],
  declarations: [
    CreditCardMaskPipe,
    CreditCardComponent
  ],
  providers: [CreditCardService],
  exports: [CreditCardComponent]
})
export class CreditCardModule {}
</code></pre>
<p>&#x6211;&#x5011;&#x5DF2;&#x7D93;&#x77E5;&#x9053;&#x9019;&#x500B;&#x662F;&#x4E00;&#x500B; feature module&#xFF0C;&#x4F46;&#x770B;&#x4E00;&#x4E0B;&#x5167;&#x5BB9;&#x5176;&#x5BE6;&#x8DDF; root module &#x9577;&#x5F97;&#x5F88;&#x50CF;&#xFF0C;&#x4F46;&#x4ECD;&#x7136;&#x6709;&#x5E7E;&#x9EDE;&#x4E0D;&#x540C;&#xFF1A;</p>
<ul>
<li>&#x5F15;&#x5165; <code>CommonModule</code> &#x800C;&#x975E; <code>BrowserModule</code>
</li>
<li>
<code>@NgModule</code> &#x88E1;&#x9762;&#x591A;&#x4E86; <code>export</code>&#xFF0C;<code>declarations</code> &#x5BA3;&#x544A;&#x7528;&#x5230;&#x7684;&#x7269;&#x4EF6;&#x662F; private&#xFF0C;&#x70BA;&#x4E86;&#x8B93;&#x6211;&#x5011;&#x7684; module &#x5728;&#x88AB;&#x5176;&#x4ED6; module &#x4F7F;&#x7528;&#x7684;&#x6642;&#x5019;&#x4E5F;&#x53EF;&#x4EE5;&#x52D5;&#x7528;&#x81EA;&#x5DF1;&#x6A21;&#x7D44;&#x88E1;&#x7684;&#x7269;&#x4EF6;&#xFF0C;<code>export</code> &#x53EF;&#x4EE5;&#x8B93; <code>CeditCardComponent</code> &#x8B8A;&#x6210; public&#xFF0C; up &#x56E0;&#x70BA; <code>AppComponent</code> &#x4E4B;&#x5F8C;&#x6703;&#x7528;&#x5230;&#x3002;&#x4F46;&#x662F; <code>CreditCardMaskPipe</code> &#x5247;&#x7E7C;&#x7E8C;&#x4FDD;&#x6301; private&#xFF0C;&#x56E0;&#x70BA;&#x9019;&#x53EA;&#x6709;&#x5728;&#x81EA;&#x5DF1;&#x6A21;&#x7D44;&#x4E2D;&#x7684;&#x6E9D;&#x901A;&#x624D;&#x6703;&#x7528;&#x5230;&#x3002;</li>
</ul>
<p>&#x63A5;&#x8457;&#x4F86;&#x770B;&#x770B; <code>AppModule</code> &#x5982;&#x4F55;&#x4F7F;&#x7528;  <code>CreditCardModule</code></p>
<pre><code>app/app.module.ts
import { NgModule } from &apos;@angular/core&apos;;
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { CreditCardModule } from &apos;../credit-card/credit-card.module&apos;;
import { AppComponent } from &apos;./app.component&apos;;

@NgModule({
  imports: [
    BrowserModule,
    CreditCardModule
  ],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule { }
</code></pre>
<p><code>imports</code> &#x4E2D;&#x5F15;&#x5165;&#x8981;&#x4F7F;&#x7528;&#x7684;&#x5176;&#x4ED6;&#x6A21;&#x7D44;</p>
<p>&#x525B;&#x525B;&#x5DF2;&#x7D93;&#x8AAA; <code>CeditCardComponent</code> &#x88AB;&#x6A21;&#x7D44;&#x516C;&#x958B;&#x4E86;&#xFF0C;&#x6240;&#x4EE5; <code>AppComponent</code> &#x9019;&#x908A;&#x5C31;&#x53EF;&#x4EE5;&#x62FF;&#x4F86;&#x4F7F;&#x7528;&#x56C9;</p>
<pre><code>//app/app.component.ts

...
@Component({
  ...
  template: `
    ...
    &lt;app-credit-card&gt;&lt;/app-credit-card&gt;
  `
})
export class AppComponent {}
</code></pre>
<h2>&#x6307;&#x4EE4;&#x885D;&#x7A81;</h2>
<p>&#x56E0;&#x70BA;&#x6211;&#x5011;&#x4E0D;&#x518D;&#x76F4;&#x63A5;&#x5B9A;&#x7FA9;&#x6BCF;&#x500B; component &#x4ED6;&#x5011;&#x6240;&#x9700;&#x8981;&#x7684; component &#x548C; directive&#x3002;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x9700;&#x8981;&#x77E5;&#x9053; Angular Module &#x5982;&#x4F55;&#x8655;&#x7406;&#x6307;&#x4EE4;&#x548C;&#x7D44;&#x4EF6;&#x540C;&#x6642;&#x4F5C;&#x7528;&#x5728;&#x540C;&#x4E00;&#x500B;&#x5143;&#x4EF6;&#x4E0A;&#x6642;&#x5019;&#x7684;&#x885D;&#x7A81;&#x3002;&#x4E5F;&#x5C31;&#x662F;&#x90FD;&#x91DD;&#x5C0D;&#x540C;&#x4E00;&#x500B; <code>selector</code> &#x6642;&#x5019;&#x6703;&#x600E;&#x9EBC;&#x505A;&#x3002;</p>
<p>&#x73FE;&#x5728;&#x5047;&#x8A2D;&#x6709;&#x5169;&#x500B;&#x6307;&#x4EE4;&#xFF0C;&#x91DD;&#x5C0D;&#x540C;&#x4E00;&#x500B;&#x5143;&#x4EF6;&#x4F5C;&#x7528;&#x3002;</p>
<p>&#x4F7F;&#x80CC;&#x666F;&#x8B8A;&#x85CD;&#xFF0C;&#x5B57;&#x8B8A;&#x7070;</p>
<pre><code>//blue-highlight.directive.ts
import { Directive, ElementRef, Renderer } from &apos;@angular/core&apos;;

@Directive({
  selector: &apos;[appHighlight]&apos;
})
export class BlueHighlightDirective {
  constructor(renderer: Renderer, el: ElementRef) {
    renderer.setElementStyle(el.nativeElement, &apos;backgroundColor&apos;, &apos;blue&apos;);
    renderer.setElementStyle(el.nativeElement, &apos;color&apos;, &apos;gray&apos;);
  }
}
</code></pre>
<p>&#x80CC;&#x666F;&#x8B8A;&#x9EC3;</p>
<pre><code>//yellow-highlight.directive.ts
import { Directive, ElementRef, Renderer } from &apos;@angular/core&apos;;

@Directive({
  selector: &apos;[appHighlight]&apos;
})
export class YellowHighlightDirective {
  constructor(renderer: Renderer, el: ElementRef) {
    renderer.setElementStyle(el.nativeElement, &apos;backgroundColor&apos;, &apos;yellow&apos;);
  }
}
</code></pre>
<p>&#x4E00;&#x500B;&#x8981;&#x8B93;&#x80CC;&#x666F;&#x8B8A;&#x9EC3;&#xFF0C;&#x4E00;&#x500B;&#x8981;&#x8B93;&#x80CC;&#x666F;&#x8B8A;&#x85CD;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x6703;&#x600E;&#x6A23;&#xFF1F;</p>
<p><code>AppModule</code> &#x9019;&#x6A23;&#x5B9A;&#x7FA9;</p>
<pre><code>//app.module.ts

// Imports

@NgModule({
  imports: [BrowserModule],
  declarations: [
    AppComponent,
    BlueHighlightDirective,
    YellowHighlightDirective
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
</code></pre>
<p>&#x6211;&#x5011;&#x7684;&#x7D44;&#x4EF6;&#x9577;&#x9019;&#x6A23;&#xFF0C;&#x5176;&#x4E2D;&#x7684; <code>appHighlight</code> &#x5C31;&#x662F;&#x88AB;&#x5169;&#x500B;&#x6307;&#x4EE4;&#x540C;&#x6642;&#x4F5C;&#x7528;&#x7684;&#x6771;&#x897F;&#x3002;</p>
<pre><code>//app.component.ts

import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;app-root&apos;,
  template: &apos;&lt;h1 appHighlight&gt;My Angular 2 App&lt;/h1&gt;&apos;
})
export class AppComponent {}
</code></pre>
<p>&#x6240;&#x4EE5;&#x6700;&#x5F8C;&#x7D50;&#x8AD6;&#x662F;&#x5982;&#x4F55;&#xFF1F;</p>
<p>&#x7B54;&#x6848;&#x662F;&#x5B57;&#x662F;&#x7070;&#x8272;&#xFF0C;&#x80CC;&#x666F;&#x662F;&#x9EC3;&#x8272; (<a href="https://plnkr.co/edit/yY3RRPDxf6urDfsMVNik?p=preview" target="_blank">Plurk</a>)</p>
<p>&#x9084;&#x8A18;&#x5F97;&#x525B;&#x525B;&#x7684; module &#x55CE;&#xFF1F;</p>
<pre><code>declarations: [
  ...,
  BlueHighlightDirective,
  YellowHighlightDirective
]
</code></pre>
<p><code>BlueHighlightDirective</code> &#x5148;&#x88AB;&#x57F7;&#x884C;&#xFF0C; <code>YellowHighlightDirective</code> &#x518D;&#x88AB;&#x57F7;&#x884C;&#xFF0C;&#x6240;&#x4EE5;&#x80CC;&#x666F;&#x5148;&#x8B8A;&#x85CD;&#x8272;&#x5F8C;&#x4F86;&#x53C8;&#x8B8A;&#x6210;&#x9EC3;&#x8272;&#x3002;</p>
<p><strong>&#x7D50;&#x8AD6;&#x5C31;&#x662F;&#x7576;&#x885D;&#x7A81;&#x767C;&#x751F;&#x6642;&#xFF0C;&#x7576;&#x8A31;&#x591A;&#x6307;&#x4EE4;&#x4F5C;&#x7528;&#x5728;&#x540C;&#x4E00;&#x500B;&#x5143;&#x4EF6;&#x6642;&#xFF0C;&#x6703;&#x4F9D;&#x7167;&#x9806;&#x5E8F;&#x57F7;&#x884C;&#x3002;</strong></p>
 <br>
                                                    </div>
                    </div>
                
