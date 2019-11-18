---
title: Angular 2 PIPES(通道)
date: 2016-12-22 23:26:11
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x6BCF;&#x4E00;&#x500B;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x90FD;&#x662F;&#x4E00;&#x4E9B;&#x975E;&#x5E38;&#x7C21;&#x55AE;&#x7684;&#x4EFB;&#x52D9;&#x958B;&#x59CB;&#xFF1A;&#x7372;&#x53D6;&#x6578;&#x64DA;&#x3001;&#x8F49;&#x63DB;&#x6578;&#x64DA;&#xFF0C;&#x4E26;&#x628A;&#x5B83;&#x5011;&#x986F;&#x793A;&#x7D66;&#x7528;&#x6236;&#x3002;</p>
<p>&#x6211;&#x5011;&#x6709;&#x60F3;&#x8981;&#x5448;&#x73FE;&#x7684;&#x6578;&#x64DA;&#xFF0C;&#x4F46;&#x53EF;&#x80FD;&#x6A23;&#x5B50;&#x5F88;&#x919C;&#xFF0C;&#x9020;&#x6210;&#x7528;&#x6236;&#x9AD4;&#x9A57;&#x5F88;&#x5DEE;&#xFF0C;&#x6216;&#x8457;&#x4E0D;&#x662F;&#x6211;&#x5011;&#x8981;&#x7684;&#x683C;&#x5F0F;&#x3002;&#x6BD4;&#x65B9;&#x8AAA;&#x5E7E;&#x4E4E;&#x986F;&#x793A;&#x65E5;&#x671F; (2016-12-22) &#x800C;&#x975E;&#x539F;&#x59CB;&#x5B57;&#x7B26;&#x4E32;&#x683C;&#x5F0F; (Thu Dec 22 2016 20:00:00 GMT+0800)&#x3002;&#x6216;&#x8457;&#x6709;&#x6642;&#x5019;&#x60F3;&#x8981;&#x628A;&#x6240;&#x6709;&#x5C0F;&#x5BEB;&#x5B57;&#x6BCD;&#xFF0C;&#x5728;&#x986F;&#x793A;&#x7684;&#x6642;&#x5019;&#x8B8A;&#x6210;&#x90FD;&#x662F;&#x5927;&#x5BEB;&#x3002;</p>
<p>&#x5C07;&#x5C0F;&#x5BEB;&#x8B8A;&#x6210;&#x5927;&#x5BEB;&#xFF1A;</p>
<pre><code>// app.component.ts

import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;my-app&apos;,
  // uppercase &#x70BA; Angular &#x5167;&#x5EFA;
  template: &apos;&lt;p&gt;My name is &lt;strong&gt;{{ name | uppercase }}&lt;/strong&gt;.&lt;/p&gt;&apos;,
})
export class AppComponent {
  name = &apos;john doe&apos;;
}
</code></pre>
<p>&#x8F38;&#x51FA;&#x7D50;&#x679C;&#x6703;&#x662F; My name is JOHN DOE.</p>
<p>&#x6211;&#x5011;&#x767C;&#x73FE;&#xFF0C;&#x61C9;&#x7528;&#x7A0B;&#x5E8F;&#x4E2D;&#x91CD;&#x8907;&#x8457;&#x4E0A;&#x8FF0;&#x76F8;&#x540C;&#x7684;&#x8F49;&#x63DB;&#x975E;&#x5E38;&#x591A;&#x3002;&#x89E3;&#x6C7A;&#x65B9;&#x5F0F;&#x53EF;&#x4EE5;&#x7528; TS &#x628A;&#x6578;&#x64DA;&#x505A;&#x597D;&#x8F49;&#x63DB;&#xFF0C;&#x518D;&#x4F86;&#x5448;&#x73FE;&#x3002;&#x4E5F;&#x53EF;&#x4EE5;&#x5C07;&#x9019;&#x4E9B;&#x8F49;&#x63DB;&#x76F4;&#x63A5;&#x5728; HTML &#x6A21;&#x677F;&#x88E1;&#x8F49;&#x63DB;&#x3002;&#x5F8C;&#x8005;&#x904E;&#x7A0B;&#x53EB;&#x505A;&#x7BA1;&#x9053;(pipe)&#x3002;</p>
<h2>&#x5BA2;&#x88FD;&#x5316;&#x901A;&#x9053;</h2>
<p>&#x73FE;&#x5728;&#x6211;&#x5011;&#x8981;&#x505A;&#x4E00;&#x500B;&#x628A;&#x6BCF;&#x500B;&#x55AE;&#x5B57;&#x7B2C;&#x4E00;&#x500B;&#x5B57;&#x6BCD;&#x8B8A;&#x6210;&#x5927;&#x5BEB;&#x7684;&#x901A;&#x9053;&#xFF1A;<br>
&#x5148;&#x5B9A;&#x7FA9;&#x6211;&#x5011;&#x7684; Pipe</p>
<pre><code>// capitalize.pipe.ts

import { Pipe, PipeTransform } from &apos;@angular/core&apos;;

@Pipe({name: &apos;capitalize&apos;})
export class CapitalizePipe implements PipeTransform {
  transform(value: string, args: string[]): any {
    if (!value) return value;

    return value.replace(/\w\S*/g, function(txt) {
        return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();
    });
  }
}
</code></pre>
<p>&#x63A5;&#x8457;&#x4F7F;&#x7528;&#x6211;&#x5011;&#x7684; Pipe</p>
<pre><code>// app.component.ts

import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;my-app&apos;,
  template: &apos;&lt;p&gt;My name is &lt;strong&gt;{{ name | capitalize }}&lt;/strong&gt;.&lt;/p&gt;&apos;
  // &#x7528; capitalize &#x9019;&#x500B; pipe &#x4F86;&#x505A;&#x8F49;&#x63DB;
})
export class AppComponent {
  name = &apos;john doe&apos;;
}
</code></pre>
<p>&#x8F38;&#x51FA;&#x7D50;&#x679C;&#x6703;&#x662F;  My name is John Doe.</p>
<h2>App &#x901A;&#x7528;&#x7684; Pipe</h2>
<p>&#x6709;&#x4E9B; Pipe &#x6211;&#x5011;&#x53EF;&#x80FD;&#x6703;&#x4E00;&#x76F4;&#x7528;&#x5230;&#xFF0C;&#x4F8B;&#x5982;&#x65E5;&#x671F;&#x8F49;&#x63DB;&#x3001;&#x8A9E;&#x8A00;&#x7FFB;&#x8B6F;&#xFF0C;&#x9019;&#x4E9B;&#x53EF;&#x80FD;&#x5728;&#x5F88;&#x591A;&#x500B; Components &#x4E2D;&#x90FD;&#x6709;&#x7528;&#x5230;&#xFF0C;&#x6211;&#x5011;&#x80FD;&#x505A;&#x5230;&#x8B93;&#x81EA;&#x5DF1;&#x5B9A;&#x7FA9;&#x7684; Pipe &#x5C31;&#x50CF;&#x4E00;&#x4E9B;&#x5167;&#x5EFA;&#x7684; Pipe &#x5728;&#x6BCF;&#x500B; Component &#x4E2D;&#x90FD;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;&#x3002;</p>
<p>&#x4E00;&#x7A2E;&#x65B9;&#x6CD5;&#x662F;&#x6211;&#x5011;&#x5728; App Module &#x4E2D;&#x5F15;&#x5165;&#x6211;&#x5011;&#x5BEB;&#x597D;&#x7684; Pipe</p>
<pre><code>// app.module.ts

import { NgModule }      from &apos;@angular/core&apos;;
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { AppComponent }   from &apos;./app.component&apos;;
import { CapitalizePipe } from &apos;./capitalize.pipe&apos;; // &#x5C0E;&#x5165;&#x6211;&#x5011;&#x7684; pipe

@NgModule({
  imports:      [ BrowserModule ],
  // &#x5F15;&#x5165; capitalize pipe 
  declarations: [ AppComponent, CapitalizePipe ], 
  bootstrap:    [ AppComponent ]
})

export class AppModule { }
</code></pre>
<p>&#x9019;&#x6A23;&#x4E4B;&#x5F8C;&#x8981;&#x7528; Pipe &#x5C31;&#x4E0D;&#x7528;&#x6BCF;&#x500B; Component &#x90FD;&#x4E00;&#x4E00;&#x5BA3;&#x544A;&#x56C9;&#xFF01;<br>
<a href="http://plnkr.co/edit/LVwYDhFXhAbqffs03g9h?p=preview" target="_blank">Plurk</a> &#x7BC4;&#x4F8B;</p>
 <br>
                                                    </div>
                    </div>
                
