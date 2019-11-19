---
title: Angular 2 Module ( 1 )
date: 2016-12-30 23:47:16
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x5728; Angular 2 &#x4E2D;&#xFF0C;&#x4E00;&#x500B; Module ( &#x6A21;&#x7D44; ) &#x662F;&#x4E00;&#x500B;&#x628A;&#x5F7C;&#x6B64;&#x4E92;&#x76F8;&#x95DC;&#x806F;&#x7684; components&#x3001;directives&#x3001;pipes &#x548C;  services &#x6574;&#x5408;&#x7684;&#x6A5F;&#x5236;&#x3002;&#x7136;&#x5F8C;&#x9019;&#x500B;&#x6A21;&#x7D44;&#x53EF;&#x4EE5;&#x518D;&#x548C;&#x5176;&#x4ED6;&#x6A21;&#x7D44;&#x7D50;&#x5408;&#xFF0C;&#x6700;&#x5F8C;&#x5C31;&#x5F62;&#x6210;&#x6211;&#x5011;&#x7684;&#x7DB2;&#x9801;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x3002;&#x7DB2;&#x9801;&#x5C31;&#x50CF;&#x62FC;&#x5716;&#x4E00;&#x822C;&#xFF0C;&#x7531;&#x8A31;&#x591A;&#x5C0F;&#x788E;&#x7247;&#x7684;&#x7D44;&#x4EF6;&#x548C;&#x4E00;&#x584A;&#x4E00;&#x584A;&#x7684;&#x6A21;&#x7D44;&#x6240;&#x69CB;&#x6210;&#x3002;<br>
&#x4E00;&#x500B;&#x6A21;&#x7D44;&#x53C8;&#x7531;&#x9EDE;&#x50CF;&#x662F;&#x985E;&#x5225; ( Class )&#xFF0C;&#x4E00;&#x6A23;&#x4E5F;&#x6709; public &#x548C; private &#x7684;&#x6982;&#x5FF5;&#x3002;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x53EA;&#x80FD;&#x53D6;&#x7528;&#x516C;&#x958B;&#x7684;&#x90E8;&#x5206;&#xFF0C;&#x79C1;&#x6709;&#x7684;&#x90E8;&#x5206;&#x5247;&#x770B;&#x4E0D;&#x898B;&#x3002;</p>
<h2>&#x57FA;&#x790E;</h2>
<p>&#x7C21;&#x55AE;&#x7684; Angular 2  Quick Start &#x5927;&#x6982;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>|- app/
    |- app.component.html
    |- app.component.ts
    |- app.module.ts
|- index.html
</code></pre>
<p>&#x4E0D;&#x4E00;&#x5B9A;&#x5C31;&#x662F;&#x9577;&#x9019;&#x6A23;&#xFF0C;&#x4F46;&#x9019;&#x5E7E;&#x500B;&#x6587;&#x4EF6;&#x662F;&#x4E00;&#x5B9A;&#x6709;&#x7684;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x88E1;&#x9762;&#x6709; <code>app.module.ts</code>&#xFF0C;&#x9019;&#x5C31;&#x662F;&#x4E00;&#x500B; Module&#x3002;&#x63A5;&#x8457;&#x4F86;&#x770B;&#x770B;&#x88E1;&#x9762;&#x7684;&#x6A23;&#x5B50;&#x3002;</p>
<p>&#x6211;&#x5011;&#x7528; <code>NgModule</code> &#x4F86;&#x5B9A;&#x7FA9;&#x662F;&#x6A21;&#x7D44;&#x3002;</p>
<pre><code>//app/app.module.ts

import { NgModule } from &apos;@angular/core&apos;;

@NgModule({
  imports: [ ... ],
  declarations: [ ... ],
  bootstrap: [ ... ]
})
export class AppModule { }
</code></pre>
<p><code>NgModule</code> &#x9019;&#x500B;&#x88DD;&#x98FE;&#x5668; ( decorator ) &#x9700;&#x8981;&#x81F3;&#x5C11;&#x4E09;&#x500B;&#x7279;&#x6027;&#xFF1A; <code>import</code>&#x3001;<code>declaration</code> &#x548C; <code>bootstrap</code>&#x3002;</p>
<ul>
<li>import&#xFF1A;&#x9810;&#x671F;&#x6709;&#x4E00;&#x500B;&#x9663;&#x5217;&#x5305;&#x542B;&#x8981;&#x5F15;&#x5165;&#x7684;&#x6240;&#x6709;&#x9663;&#x5217;&#x3002;</li>
<li>declaration&#xFF1A;&#x9810;&#x671F;&#x6709;&#x4E00;&#x500B;&#x9663;&#x5217;&#x5305;&#x542B;&#x6240;&#x6709;&#x9019;&#x500B;&#x6A21;&#x7D44;&#x8981;&#x7528;&#x7684; components&#x3001;directives &#x548C; pipes&#x3002;</li>
<li>bootstrap&#xFF1A;&#x6211;&#x5011;&#x7528;&#x4F86;&#x5B9A;&#x7FA9;&#x6839;&#x7D44;&#x4EF6; (root component)&#xFF0C;&#x96D6;&#x7136;&#x53EF;&#x4EE5;&#x662F;&#x4E00;&#x500B;&#x9663;&#x5217;&#xFF0C;&#x4F46;&#x901A;&#x5E38;&#x6211;&#x5011;&#x53EA;&#x6703;&#x5B9A;&#x7FA9;&#x4E00;&#x500B;&#x800C;&#x5DF2;&#x3002;&#x6839;&#x7D44;&#x4EF6;&#x6703;&#x518D;&#x5F15;&#x5165;&#x5176;&#x4ED6;&#x66F4;&#x591A;&#x7684;&#x7D44;&#x4EF6;&#x3002;</li>
</ul>
<h2>&#x7C21;&#x55AE;&#x61C9;&#x7528;</h2>
<p>&#x63A5;&#x8457;&#x4F86;&#x770B;&#x770B;&#x7C21;&#x55AE;&#x7248;&#x7684;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x5982;&#x4F55;&#x7528;&#x5230;&#x6A21;&#x7D44;&#xFF0C;&#x9019;&#x908A;&#x7684;&#x6848;&#x4F8B;&#x662F;&#x4E00;&#x500B;&#x6A21;&#x7D44;&#x642D;&#x914D;&#x4E00;&#x500B;&#x7D44;&#x4EF6;&#x3002;</p>
<pre><code>//app/app.component.ts

import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;app-root&apos;,
  template: &apos;&lt;h1&gt;My Angular 2 App&lt;/h1&gt;&apos;
})
export class AppComponent {}
</code></pre>
<pre><code>//app/app.module.ts

import { NgModule } from &apos;@angular/core&apos;;
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { AppComponent } from &apos;./app.component&apos;;

@NgModule({
  imports: [BrowserModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule { }
</code></pre>
<p>&#x9019;&#x908A; <code>AppModule</code> &#x5F15;&#x5165; <code>BrowserModule</code>&#xFF0C;&#x5B83;&#x5305;&#x542B;&#x4E86;&#x4E00;&#x4E9B;&#x6700;&#x57FA;&#x672C;&#x7684; <code>directives</code>&#x3001; <code>pipes</code> &#x548C; <code>services</code>&#x3002;&#x6B64;&#x5916;&#x9019;&#x908A;&#x7684;&#x6839;&#x7D44;&#x4EF6;&#x662F; <code>AppComponent</code>&#x3002;<code>declarations</code>&#x8CA0;&#x8CAC;&#x5B9A;&#x7FA9;&#x7A0B;&#x5F0F;&#x9700;&#x8981;&#x751A;&#x9EBC;&#x6771;&#x897F;&#xFF0C;&#x6240;&#x4EE5;&#x4E5F;&#x8981;&#x586B;&#x5165; <code>AppComponent</code>&#x3002;</p>
<h2>&#x6A21;&#x7D44;&#x7A2E;&#x985E;</h2>
<p>&#x6A21;&#x7D44;&#x6709;&#x5169;&#x7A2E;&#xFF1A;</p>
<ul>
<li>root module</li>
<li>feature module&#x3002;<br>
&#x4E00;&#x500B;&#x7A0B;&#x5F0F;&#x57FA;&#x672C;&#x4E0A;&#x53EA;&#x6703;&#x6709;&#x4E00;&#x500B; root module&#xFF0C;&#x642D;&#x914D; 0 &#x500B;&#x6216;&#x8A31;&#x591A;&#x500B; feature module&#x3002;&#x8981;&#x555F;&#x52D5;&#x7A0B;&#x5F0F;&#x4E00;&#x5B9A;&#x8981;&#x6709; root module&#xFF0C;&#x5224;&#x5225;&#x65B9;&#x5F0F;&#x662F; root module &#x6703;&#x6709; <code>NgModule</code> &#x88DD;&#x98FE;&#x5668;&#xFF0C;&#x4E14;&#x4ED6;&#x6703;&#x5F15;&#x5165; <code>BrowserModule</code>&#x3002;<br>
&#x82E5;&#x662F; feature module &#x5247;&#x662F;&#x6703;&#x5F15;&#x5165; <code>CommonModule</code>&#x3002;</li>
</ul>
<p>&#x6309;&#x7167;&#x6163;&#x4F8B;&#xFF0C; root module &#x901A;&#x5E38;&#x90FD;&#x6703;&#x547D;&#x540D;&#x70BA; <code>AppModule</code>&#x3002;</p>
<h2>&#x6A21;&#x7D44;&#x5F15;&#x5165;&#x6771;&#x897F;</h2>
<p>&#x5047;&#x8A2D;&#x6211;&#x5011;&#x73FE;&#x5728;&#x9084;&#x6709; <code>CreditCardMaskPipe</code> &#x3001; <code>CreditCardService</code> &#x3001; <code>CreditCardComponent</code>&#xFF0C;&#x6211;&#x5011;&#x5C31;&#x8981;&#x66F4;&#x65B0;&#x4E00;&#x4E0B;&#x6211;&#x5011;&#x7684;&#x6A21;&#x7D44;&#xFF0C;&#x5426;&#x5247; Angular &#x4E5F;&#x4E0D;&#x6703;&#x53BB;&#x7DE8;&#x8B6F;&#x9019;&#x4E9B;&#x6771;&#x897F;&#x3002;</p>
<pre><code>//app.module.ts

import { NgModule } from &apos;@angular/core&apos;;
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { AppComponent } from &apos;./app.component&apos;;

import { CreditCardMaskPipe } from &apos;./credit-card-mask.pipe&apos;;
import { CreditCardService } from &apos;./credit-card.service&apos;;
import { CreditCardComponent } from &apos;./credit-card.component&apos;;

@NgModule({
  imports: [BrowserModule],
  providers: [CreditCardService],
  declarations: [
    AppComponent,
    CreditCardMaskPipe,
    CreditCardComponent
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
</code></pre>
<p><code>providers</code> &#x53EA;&#x80FD;&#x7528;&#x5728; root module &#xFF0C;&#x7528;&#x4F86;&#x6CE8;&#x5165;&#x4F9D;&#x8CF4;&#x670D;&#x52D9;&#x3002;&#x7528;&#x5728; feature module &#x7684;&#x8A71;&#xFF0C;&#x5F88;&#x53EF;&#x80FD;&#x6703;&#x5C0E;&#x81F4;&#x4E0D;&#x660E;&#x7684;&#x932F;&#x8AA4;&#x3002;</p>
<p>&#x4E0B;&#x7BC7; <a href="https://ithelp.ithome.com.tw/articles/10188188" target="_blank">Angular 2 Module ( 2 )</a> &#x6703;&#x7E7C;&#x7E8C;&#x63A2;&#x8A0E;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
