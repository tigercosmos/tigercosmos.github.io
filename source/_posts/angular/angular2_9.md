---
title: Angular 2 動畫 (ANIMATIONS)
date: 2016-12-25 23:18:43
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x52D5;&#x756B;&#x5728;&#x73FE;&#x4EE3;&#x7DB2;&#x9801;&#x4E2D;&#x7121;&#x6240;&#x4E0D;&#x5728;&#x3002;&#x597D;&#x7684;&#x4F7F;&#x7528;&#x8005;&#x4ECB;&#x9762;&#xFF0C;&#x88E1;&#x9762;&#x7684;&#x52D5;&#x756B;&#x61C9;&#x8A72;&#x8981;&#x770B;&#x8D77;&#x4F86;&#x5F88;&#x5E73;&#x9806;&#x81EA;&#x7136;&#xFF0C;&#x5FC5;&#x8981;&#x800C;&#x4E0D;&#x82B1;&#x4FCF;&#xFF0C;&#x9019;&#x6A23;&#x624D;&#x80FD;&#x5E36;&#x7D66;&#x4F7F;&#x7528;&#x8005;&#x6700;&#x4F73;&#x7684;&#x9AD4;&#x9A57;&#xFF0C;&#x4E26;&#x4E14;&#x5728;&#x67D0;&#x4E9B;&#x91CD;&#x8981;&#x7684;&#x5730;&#x65B9;&#x8B93;&#x4F7F;&#x7528;&#x8005;&#x6CE8;&#x610F;&#x5230;&#x3002;&#x6240;&#x4EE5;&#x4E00;&#x500B;&#x6709;&#x597D;&#x7684;&#x8A2D;&#x8A08;&#x7684;&#x52D5;&#x756B;&#x9801;&#x9762;&#xFF0C;&#x53EF;&#x4EE5;&#x8B93; UI &#x66F4;&#x6709;&#x8DA3;&#x4E14;&#x66F4;&#x5BB9;&#x6613;&#x4F7F;&#x7528;&#x3002;</p>
<p>Angular &#x53EF;&#x4EE5;&#x88FD;&#x9020;&#x51FA;&#x8DDF;&#x7D14; CSS &#x52D5;&#x756B;&#x4E00;&#x6A23;&#x7684;&#x6548;&#x679C;. &#x6211;&#x5011;&#x53EF;&#x4EE5;&#x8F15;&#x9B06;&#x7684;&#x7528;&#x7A0B;&#x5F0F;&#x78BC;&#x4F86;&#x63A7;&#x5236;&#x9019;&#x4E9B;&#x52D5;&#x756B;&#x6548;&#x679C;&#xFF0C;&#x642D;&#x914D;&#x4E00;&#x4E9B;&#x908F;&#x8F2F;&#x653E;&#x5165;&#x6211;&#x5011;&#x7684;&#x7DB2;&#x9801;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x3002;</p>
<blockquote>
<p>Angular &#x52D5;&#x756B;&#x4F7F;&#x7528;&#x7684;&#x6A21;&#x7D44;&#x5DF2;&#x7D93;&#x5167;&#x5EFA;&#x5728;&#x5927;&#x591A;&#x6578;&#x700F;&#x89BD;&#x5668;&#xFF0C;&#x82E5;&#x662F;&#x4E0D;&#x652F;&#x63F4;&#x8981;&#x52A0;&#x5165; <a href="https://github.com/web-animations/web-animations-js" target="_blank">web-animations.min.js</a></p>
</blockquote>
<p>&#x63A5;&#x4E0B;&#x4F86;&#x6211;&#x5011;&#x7ADF;&#x4F86;&#x5EFA;&#x7ACB; component&#xFF0C;&#x4F86;&#x505A;&#x5230;&#x7528;&#x6DE1;&#x5165;&#x7684;&#x6548;&#x679C;&#x986F;&#x793A;&#x548C;&#x96B1;&#x85CF;&#x5167;&#x5BB9;&#xFF0C;&#x4E26;&#x8B93;&#x5176;&#x4ED6;&#x5916;&#x90E8;&#x7684; component &#x4E5F;&#x53EF;&#x4EE5;&#x8F15;&#x6613;&#x7684;&#x89F8;&#x767C;&#x4ED6;&#x5011;&#x7684;&#x6DE1;&#x5165;&#x6548;&#x679C;&#x3002;</p>
<h2>&#x6E96;&#x5099;&#x5DE5;&#x5177;</h2>
<p>&#x5148;&#x4F86;&#x770B;&#x770B;&#x505A;&#x52D5;&#x756B;&#x9700;&#x8981;&#x751A;&#x9EBC;&#x5427;&#xFF01; &#x7562;&#x7ADF;&#x5DE7;&#x5A66;&#x96E3;&#x70BA;&#x7121;&#x7C73;&#x4E4B;&#x708A;&#x3002;<br>
&#x9996;&#x5148;&#x8981;&#x5F15;&#x5165;&#x9019;&#x4E9B;&#x6771;&#x897F;</p>
<pre><code>import {
  Component,
  Input,
  trigger,
  state,
  style,
  transition,
  animate
} from &apos;@angular/core&apos;;
</code></pre>
<h2>&#x5834;&#x666F;</h2>
<p>&#x5148;&#x4F86;&#x770B;&#x770B;&#x7C21;&#x55AE;&#x7684;&#x96B1;&#x85CF;&#x986F;&#x793A;&#xFF0C;&#x4E26;&#x672A;&#x52A0;&#x5165;&#x52D5;&#x756B;&#x3002;</p>
<pre><code>@Component({
  selector: &apos;my-fader&apos;,
    template: `
    &lt;div *ngIf=&quot;visibility == &apos;shown&apos;&quot; &gt;
      &lt;ng-content&gt;&lt;/ng-content&gt;
      Can you see me? 
    &lt;/div&gt;
  `
})
export class MyComponent implements OnChanges {
  visibility = &apos;shown&apos;;

  @Input() isVisible : boolean = true;

  ngOnChanges() {
   this.visibility = this.isVisible ? &apos;shown&apos; : &apos;hidden&apos;;
  }
}
</code></pre>
<p>&#x9019;&#x908A;&#x7528; <code>@Input() isVisible</code> &#x5C6C;&#x6027;&#x4F86;&#x9054;&#x5927;&#x986F;&#x793A;&#x548C;&#x96B1;&#x85CF;&#x7684;&#x6548;&#x679C;&#x3002;(<a href="https://plnkr.co/edit/vUPTsY?p=preview" target="_blank">Plurk</a>)</p>
<h2>&#x52A0;&#x6599;</h2>
<p>&#x53EA;&#x662F;&#x55AE;&#x7D14;&#x7684;&#x986F;&#x793A;&#x548C;&#x96B1;&#x85CF;&#x591A;&#x9EBC;&#x5730;&#x7121;&#x8DA3;&#x5440;&#xFF01;&#x6211;&#x5011;&#x60F3;&#x8981;&#x6709;&#x6DE1;&#x5165;&#x6216;&#x6DE1;&#x51FA;&#x7684;&#x6548;&#x679C;&#x3002;<br>
&#x4F86;&#x5E6B; Component &#x52A0;&#x9EDE;&#x6599;&#x5427;&#xFF01;</p>
<pre><code>@Component({
  ...,
  template : ``,
  animations: [
    ...
  ]
)]
class MyComponent() { ... }
</code></pre>
<p><code>animations</code> &#x7528;&#x4F86;&#x5BA3;&#x544A;&#x52D5;&#x756B;&#xFF0C;&#x548C; <code>template</code> &#x4E00;&#x6A23;&#x5C6C;&#x65BC; metadata&#x3002;</p>
<p>&#x56E0;&#x70BA;&#x6211;&#x5011;&#x7684;&#x52D5;&#x756B;&#x662F; <code>visibility</code> &#x7684;&#x5C6C;&#x6027;&#x8B8A;&#x5316;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x7684;&#x52D5;&#x756B;&#x8A2D;&#x5B9A;&#x7531;&#x5176;&#x503C;&#x8B8A;&#x5316;&#x800C;&#x89F8;&#x767C;&#x3002;</p>
<pre><code>animations: [
  trigger(&apos;visibilityChanged&apos;, [
  state(&apos;shown&apos; , style({ opacity: 1 })), 
  state(&apos;hidden&apos;, style({ opacity: 0 }))
  ])
]
</code></pre>
<p>&#x7CBE;&#x795E;&#x4E00;&#x5207;&#x76E1;&#x5728;&#x7A0B;&#x5F0F;&#x78BC;&#x4E2D;&#x3002;</p>
<p>&#x4F46;&#x662F;&#x525B;&#x525B;&#x7684;&#x8A2D;&#x5B9A;&#xFF0C;&#x662F;&#x77AC;&#x9593;&#x8B8A;&#x5316;&#xFF0C;&#x800C;&#x6211;&#x5011;&#x5E0C;&#x671B;&#x7684;&#x662F;&#x6162;&#x4E00;&#x9EDE;&#x7684;&#x6A23;&#x5B50;</p>
<pre><code>animations: [
  trigger(&#x2019;visibilityChanged&apos;, [
    state(&apos;shown&apos; , style({ opacity: 1 })), 
    state(&apos;hidden&apos;, style({ opacity: 0 })),
    transition(&apos;* =&gt; *&apos;, animate(&apos;.5s&apos;))
  ])
]
</code></pre>
<p>&#x9019;&#x6A23;&#x4E0D;&#x7BA1;&#x6DE1;&#x5165; (opacity 1 &#x5230; 0 ) &#x6216;&#x662F;&#x6DE1;&#x51FA; (opacity 0 &#x5230; 1 ) &#x90FD;&#x6703;&#x7D93;&#x904E; 500ms&#xFF0C;&#x800C; <code>animate</code> &#x4E5F;&#x53EF;&#x4EE5;&#x9019;&#x6A23;&#x8868;&#x793A; <code>animate(&apos;500ms&apos;)</code>&#x3002;<br>
<code>transition(&apos;* =&gt; *&apos;, ...)</code> &#x4EE3;&#x8868;&#x751A;&#x9EBC;&#x610F;&#x601D;&#x5462;&#xFF1F;<code>*</code> &#x4EE3;&#x8868;&#x4EFB;&#x4F55;&#x72C0;&#x614B;&#xFF0C;&#x610F;&#x601D;&#x5C31;&#x662F;&#x53EF;&#x4EE5;&#x662F; <code>shown</code> &#x6216; <code>hidden</code>&#x3002;&#x7576;&#x7136;&#x4E5F;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x6307;&#x5B9A;&#x3002;</p>
<pre><code>animations: [
  trigger(&#x2019;visibilityChanged&apos;, [
    state(&apos;shown&apos; , style({ opacity: 1 })),
    state(&apos;hidden&apos;, style({ opacity: 0 })),
    transition(&apos;shown =&gt; hidden&apos;, animate(&apos;600ms&apos;)),
    transition(&apos;hidden =&gt; shown&apos;, animate(&apos;300ms&apos;)),
  ])
]
</code></pre>
<p>&#x9019;&#x6A23;&#x6211;&#x5011;&#x5C31;&#x628A;&#x6DE1;&#x5165;&#x548C;&#x6DE1;&#x51FA;&#x505A;&#x5340;&#x9694;&#xFF0C;&#x5169;&#x8005;&#x6642;&#x9593;&#x82B1;&#x7684;&#x4E0D;&#x4E00;&#x6A23;&#x9577;&#x3002;</p>
<h2>&#x5B8C;&#x5DE5;</h2>
<p>&#x63A5;&#x4E0B;&#x4F86;&#x8981;&#x628A;&#x52D5;&#x756B;&#x548C; Compoent &#x9023;&#x8D77;&#x4F86;&#x3002; <code>visibilityChanged</code> &#x662F;&#x5982;&#x4F55;&#x548C; component &#x9023;&#x7D50;&#xFF1F;&#x52D5;&#x756B;&#x53C8;&#x662F;&#x5982;&#x4F55;&#x548C;&#x548C; component &#x7684;&#x5C6C;&#x6027;&#x4F5C;&#x7D81;&#x5B9A;&#xFF1F;</p>
<p>&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x5728;&#x6A21;&#x677F;&#x88E1;&#x9019;&#x6A23;&#x505A;&#xFF0C;&#x5C31;&#x50CF;&#x8A31;&#x591A;&#x7684;&#x6578;&#x64DA;&#x7D81;&#x5B9A;&#x6A21;&#x5F0F;&#x96F7;&#x540C;&#x3002;</p>
<pre><code>&lt;div [@visibilityChanged]=&quot;visibility&quot;&gt;
  Can you see me? I should fade in or out...
&lt;/div&gt;
</code></pre>
<p>&#x5B8C;&#x6574;&#x7248;&#x5C31;&#x6703;&#x9577;&#x5F97;&#x50CF;&#x9019;&#x6A23;&#x5B50;</p>
<pre><code>import { 
  Component, OnChanges, Input, 
  trigger, state, animate, transition, style 
} from &apos;@angular/core&apos;;

@Component({
  selector : &apos;my-fader&apos;,
  animations: [
  trigger(&apos;visibilityChanged&apos;, [
    state(&apos;shown&apos; , style({ opacity: 1 })),
    state(&apos;hidden&apos;, style({ opacity: 0 })),
    transition(&apos;* =&gt; *&apos;, animate(&apos;.5s&apos;))
  ])
  ],
  template: `
  &lt;div [@visibilityChanged]=&quot;visibility&quot; &gt;
    &lt;ng-content&gt;&lt;/ng-content&gt;  
    &lt;p&gt;Can you see me? I should fade in or out...&lt;/p&gt;
  &lt;/div&gt;
  `
})
export class FaderComponent implements OnChanges {
  @Input() isVisible : boolean = true;
  visibility = &apos;shown&apos;;

  ngOnChanges() {
   this.visibility = this.isVisible ? &apos;shown&apos; : &apos;hidden&apos;;
  }
}
</code></pre>
<h2>&#x7C21;&#x5316;</h2>
<p>&#x7528; <code>[@visibilityChanged]=&quot;isVisible&quot;</code> &#x800C;&#x4E0D;&#x662F; <code>[@visibilityChanged]=&quot;visibility&quot;</code> &#x7684;&#x8A71;&#xFF0C;&#x53EF;&#x4EE5;&#x4E0D;&#x7528;&#x5230; <code>ngOnChanges</code>&#xFF0C;&#x610F;&#x601D;&#x5C31;&#x662F;&#x7A0B;&#x5F0F;&#x78BC;&#x53EF;&#x4EE5;&#x66F4;&#x7CBE;&#x7C21;&#x3002;&#x4F46;&#x8981;&#x6CE8;&#x610F;&#x7684;&#x662F; isVisible &#x7684;&#x72C0;&#x614B;&#x662F; <code>true</code> &#x548C; <code>false</code></p>
<pre><code>import {
  Component, OnChanges, Input,
  trigger, state, animate, transition, style
} from &apos;@angular/core&apos;;

@Component({
  selector : &apos;my-fader&apos;,
  animations: [
    trigger(&apos;visibilityChanged&apos;, [
      state(&apos;true&apos; , style({ opacity: 1, transform: &apos;scale(1.0)&apos; })),
      state(&apos;false&apos;, style({ opacity: 0, transform: &apos;scale(0.0)&apos;  })),
      transition(&apos;1 =&gt; 0&apos;, animate(&apos;300ms&apos;)),
      transition(&apos;0 =&gt; 1&apos;, animate(&apos;900ms&apos;))
    ])
  ],
  template: `
  &lt;div [@visibilityChanged]=&quot;isVisible&quot; &gt;
    &lt;ng-content&gt;&lt;/ng-content&gt;
    &lt;p&gt;Can you see me? I should fade in or out...&lt;/p&gt;
  &lt;/div&gt;
  `
})
export class FaderComponent implements OnChanges {
  @Input() isVisible : boolean = true;
}
</code></pre>
<p>(<a href="https://plnkr.co/edit/74lprkmzUGjT7UWbiyUr?p=preview" target="_blank">Plurk</a>)</p>
<h2>&#x5C64;&#x6B21;</h2>
<p>parent component &#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x63A7;&#x5236; child component&#xFF0C;&#x9019;&#x908A;&#x7684;&#x4F8B;&#x5B50;&#x5C31;&#x662F; <code>&lt;my-fader&gt;</code> &#x7684; <code>isVisible</code> &#x8B8A;&#x5316;&#xFF0C;&#x6703;&#x76F4;&#x63A5;&#x5F71;&#x97FF;&#x5230; child component <code>my-fader</code>&#xFF0C;<code>my-fader</code> &#x7684;&#x6A21;&#x677F;&#x4E5F;&#x6703;&#x8DDF;&#x8457;&#x4E00;&#x8D77;&#x52D5;&#xFF0C;&#x9054;&#x5230;&#x6211;&#x5011;&#x8981;&#x7684;&#x6DE1;&#x5165;&#x6DE1;&#x51FA;&#x6548;&#x679C;&#x3002;</p>
<pre><code>@Component({
  selector : &apos;my-app&apos;,
  template: `

  &lt;my-fader [isVisible]=&quot;showFader&quot;&gt;
    Am I visible ?
  &lt;/my-fader&gt;

  &lt;button (click)=&quot;showFader = !showFader&quot;&gt; Toggle &lt;/button&gt;
  `
})
export class MyAppComponent {  
  showFader : boolean = true;
}
</code></pre>
<p>(<a href="https://plnkr.co/edit/NbWGjs?p=preview" target="_blank">Plurk</a>)</p>
<hr>
<h2>&#x7D30;&#x8AAA; State</h2>
<h3>wildcard state</h3>
<p>&#x9084;&#x8A18;&#x5F97;&#x525B;&#x525B; <code>transition(&apos;* =&gt; *&apos;,...)</code> &#x55CE;&#xFF1F; <code>*</code>&#x5C31;&#x662F; wildcard state(&#x901A;&#x7528;&#x7B26;&#x865F;)&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x8868;&#x793A;&#x6240;&#x6709;&#x72C0;&#x6CC1;&#xFF0C;&#x5728;&#x7A0B;&#x5F0F;&#x8A9E;&#x8A00;&#x4E2D;&#x61C9;&#x8A72;&#x883B;&#x5E38;&#x898B;&#x7684;&#x3002;</p>
<h3>void state</h3>
<p><code>void</code> &#x4EE3;&#x8868;&#x6C92;&#x6709;&#x6771;&#x897F;&#xFF0C;&#x53EF;&#x80FD;&#x662F;&#x88AB;&#x79FB;&#x9664;&#x6216;&#x662F;&#x9084;&#x6C92;&#x88AB;&#x7522;&#x751F;&#xFF0C;<code>void</code> &#x7528;&#x5728;&#x9032;&#x5165;&#x548C;&#x51FA;&#x5834;&#x6642;&#x975E;&#x5E38;&#x597D;&#x7528;&#x3002;&#x8209;&#x4F8B;&#x4F86;&#x8AAA; <code>* =&gt; void</code> &#x5C31;&#x4EE3;&#x8868;&#x96E2;&#x958B;&#x756B;&#x9762;&#x7684;&#x52D5;&#x756B;&#x3002;</p>
<ul>
<li>&#x98DB;&#x5165;: <code>void =&gt; *</code>
</li>
<li>&#x98DB;&#x51FA;: <code>* =&gt; void</code>
</li>
</ul>
<pre><code>animations: [
  trigger(&apos;flyInOut&apos;, [
    state(&apos;in&apos;, style({transform: &apos;translateX(0)&apos;})),
    transition(&apos;void =&gt; *&apos;, [
      style({transform: &apos;translateX(-100%)&apos;}),
      animate(100)
    ]),
    transition(&apos;* =&gt; void&apos;, [
      animate(100, style({transform: &apos;translateX(100%)&apos;}))
    ])
  ])
]
</code></pre>
<p>&#x4E0A;&#x9762;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#xFF0C;&#x6703;&#x5148;&#x6709;&#x98DB;&#x5165;&#x6548;&#x679C;&#xFF0C;&#x7DCA;&#x63A5;&#x8005;&#x98DB;&#x51FA;&#x3002;<br>
&#x770B;&#x8D77;&#x4F86;&#x5C31;&#x6703;&#x9577;&#x9019;&#x6A23;&#xFF1A;<br>
<hr>
<h2>&#x52D5;&#x756B;&#x6642;&#x9593;&#x63A7;&#x5236;</h2>
<p>Angular &#x63D0;&#x4F9B;&#x4E09;&#x7A2E;&#x63A7;&#x5236;&#x6642;&#x9593;&#x6548;&#x679C;&#x7684;&#x5C6C;&#x6027;&#xFF0C;&#x5206;&#x5225;&#x662F; <code>duration</code> &#x3001; <code>delay</code> &#x548C; <code>easing</code>&#x3002;</p>
<h4>Duration</h4>
<ul>
<li>&#x76F4;&#x63A5;&#x7528;&#x6578;&#x5B57;&#xFF0C;&#x9810;&#x8A2D;&#x55AE;&#x4F4D;&#x70BA; ms&#xFF1A; 100</li>
<li>&#x7528;&#x5B57;&#x4E32;&#x52A0;&#x4E0A; ms&#xFF1A; &apos;100ms&apos;</li>
<li>&#x7528;&#x5B57;&#x4E32;&#x52A0;&#x4E0A; s&#xFF1A; &apos;0.1s&apos;</li>
</ul>
<h4>Delay</h4>
<ul>
<li>&#x7B49;&#x5F85; 100ms &#x7136;&#x5F8C;&#x52D5;&#x756B;&#x904B;&#x4F5C; 200ms&#xFF1A; &apos;0.2s 100ms&apos;</li>
</ul>
<h4>Easing</h4>
<ul>
<li>&#x7B49;&#x5F85; 100ms &#x7136;&#x5F8C;&#x904B;&#x884C; 200ms &#x642D;&#x914D;&#x6F38;&#x6162;&#x6548;&#x679C;&#xFF1A; &apos;0.2s 100ms ease-out&apos;</li>
<li>&#x57F7;&#x884C; 200ms &#x642D;&#x914D;&#x6F38;&#x5FEB;&#x6548;&#x679C;&#xFF1A; &apos;0.2s ease-in&apos;</li>
</ul>
<pre><code>animations: [
  trigger(&apos;flyInOut&apos;, [
    state(&apos;in&apos;, style({opacity: 1, transform: &apos;translateX(0)&apos;})),
    transition(&apos;void =&gt; *&apos;, [
      style({
        opacity: 0,
        transform: &apos;translateX(-100%)&apos;
      }),
      animate(&apos;0.2s ease-in&apos;)
    ]),
    transition(&apos;* =&gt; void&apos;, [
      animate(&apos;0.2s 10 ease-out&apos;, style({
        opacity: 0,
        transform: &apos;translateX(100%)&apos;
      }))
    ])
  ])
]
</code></pre>
<p>&#x770B;&#x8D77;&#x4F86;&#x5C31;&#x6703;&#x9577;&#x9019;&#x6A23;<br>
</p>
<hr>
<p>&#x5927;&#x591A;&#x6578;&#x7684;&#x52D5;&#x756B;&#x90FD;&#x53EF;&#x4EE5;&#x7528; Angular Component &#x7684;&#x65B9;&#x5F0F;&#x505A;&#x5230;&#xFF0C;&#x800C;&#x4E0D;&#x9700;&#x8981;&#x52D5;&#x5230; TypeScript &#x4F86;&#x63A7;&#x5236;&#x52D5;&#x756B;&#x6548;&#x679C;&#xFF0C;Angular &#x52D5;&#x756B;&#x8A2D;&#x8A08;&#x7684;&#x76EE;&#x7684;&#x5C31;&#x662F;&#x8B93;&#x6211;&#x5011;&#x7528;&#x66F4;&#x76F4;&#x89C0;&#xFF0C;&#x4E0D;&#x76F4;&#x63A5;&#x52D5; DOM &#x7684;&#x65B9;&#x5F0F;&#xFF0C;&#x7528; component-&gt;template-&gt;animation &#x7684;&#x65B9;&#x5F0F;&#xFF0C;&#x8B93;&#x8A2D;&#x8A08;&#x5E2B;&#x66F4;&#x597D;&#x5EFA;&#x69CB;&#x548C;&#x5BE6;&#x73FE;&#x52D5;&#x756B;&#x3002;</p>
<p>&#x203B;&#x66F4;&#x8A73;&#x76E1;&#x5167;&#x5BB9;&#x53EF;&#x4EE5;&#x53C3;&#x8003;<a href="https://angular.io/docs/ts/latest/guide/animations.html" target="_blank">&#x5B98;&#x65B9;&#x6587;&#x4EF6;</a></p>
 <br>
                                                    </div>
                    </div>
                
