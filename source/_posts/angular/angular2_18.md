---
title: Angular 2 Input(s) & Output(s) 傻傻分不清
date: 2017-01-03 23:46:42
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>Angular 2 &#x4E2D; Components &#x4E4B;&#x9593;&#x7684;&#x95DC;&#x4FC2;&#x793A;&#x610F;&#x5C64;&#x4E00;&#x5C64;&#x7684;&#xFF0C;&#x5C31;&#x9577;&#x5F97;&#x5411;&#x4E0B;&#x9762;&#x9019;&#x5F35;&#x5716;&#x3002;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular2-components-inputs-and-outputs.png" alt><br>
&#x6BCF;&#x500B;&#x683C;&#x5B50;&#x5C31;&#x662F;&#x4E00;&#x500B;&#x7D44;&#x4EF6;&#xFF0C;&#x8CC7;&#x8A0A;&#x5411;&#x4E0B;&#x50B3;&#x905E;&#x5F88;&#x5BB9;&#x6613;&#xFF0C;&#x800C;&#x70BA;&#x4E86;&#x7DAD;&#x8B77;&#x8CC7;&#x6599;&#x50B3;&#x905E;&#x7684;&#x55AE;&#x4E00;&#x6027;&#xFF0C;&#x5411;&#x4E0A;&#x50B3;&#x905E;&#x9700;&#x8981;&#x89F8;&#x767C;&#x4E8B;&#x4EF6; (event)&#x3002;&#x6240;&#x4EE5;&#x73FE;&#x5728;&#x7576; child component &#x9700;&#x8981;&#x88AB; parents &#x77E5;&#x9053;&#x7684;&#x6642;&#x5019;&#xFF0C;child &#x6703;&#x88AB; parents &#x89F8;&#x767C;&#x4E8B;&#x4EF6;&#x3002;parent component &#x6703;&#x63A1;&#x53D6;&#x4EFB;&#x4F55;&#x53EF;&#x80FD;&#x7684;&#x884C;&#x70BA;&#x4F86;&#x4E32;&#x806F;&#x4ED6;&#x5E95;&#x4E0B;&#x7684;&#x7D44;&#x4EF6;&#xFF0C;&#x901A;&#x5E38;&#x5C31;&#x662F;&#x55AE;&#x65B9;&#x5411;&#x5F80;&#x4E0B;&#x8CC7;&#x8A0A;&#x50B3;&#x905E;&#x3002;&#x85C9;&#x7531;&#x5340;&#x9694;&#x5411;&#x4E0A;&#x548C;&#x5411;&#x4E0B;&#x7684;&#x8CC7;&#x6599;&#x50B3;&#x905E;&#xFF0C;&#x4E8B;&#x60C5;&#x5C31;&#x8B8A;&#x5F97;&#x6BD4;&#x8F03;&#x7C21;&#x55AE;&#x548C;&#x6BD4;&#x8F03;&#x597D;&#x7BA1;&#x7406;&#x3002;</p>
<h2>@Input() &amp; inputs</h2>
<p><code>@Input</code> &#x7684;&#x76EE;&#x7684;&#x662F;&#x78BA;&#x8A8D;&#x8CC7;&#x6599;&#x7D81;&#x5B9A; input &#x7279;&#x6027; (properties)&#x662F;&#x53EF;&#x4EE5;&#x5728;&#x6539;&#x8B8A;&#x6642;&#x88AB;&#x8FFD;&#x8E64;&#x7684;&#x3002;&#x57FA;&#x672C;&#x4E0A;&#x4F86;&#x8AAA;&#xFF0C;&#x5B83;&#x662F; Angular &#x5C07; DOM &#x85C9;&#x7531;&#x7279;&#x6027;&#x7D81;&#x5B9A; (property bindings) &#x76F4;&#x63A5;&#x5728;&#x7D44;&#x4EF6;&#x6CE8;&#x5165;&#x6578;&#x503C;&#x7684;&#x65B9;&#x6CD5;&#x3002;</p>
<p>&#x8B1B;&#x4E86;&#x9019;&#x9EBC;&#x591A;&#x9084;&#x662F;&#x4E0D;&#x592A;&#x61C2;&#xFF1F;&#x9084;&#x662F;&#x76F4;&#x63A5;&#x770B; Code &#x5427;&#xFF01; &#x5148;&#x770B;&#x770B; <a href="https://embed.plnkr.co/wuMAYPOrX77RAahL5BE6/" target="_blank">Plunker</a> &#x7BC4;&#x4F8B;&#x5427;&#xFF01;</p>
<p><code>AppComponent</code> &#x9577;&#x9019;&#x6A23;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x88E1;&#x9762;&#x6709;&#x5169;&#x500B; Components&#xFF1A;<code>HelloComponent</code>&#x3001;<code>GoodbyeComponent</code></p>
<pre><code>// app/app.component.ts

import {Component, Input} from &apos;angular2/core&apos;;
import HelloComponent from &apos;./hello.component&apos;;
import GoodbyeComponent from &apos;./goodbye.component&apos;;

@Component({
	selector: &apos;app&apos;,
	template: `&lt;div&gt;
	    &lt;hello-component [myName]=&quot;name&quot;&gt;&lt;/hello-component&gt;
	    &lt;hello-component myName=&quot;Other World&quot;&gt;&lt;/hello-component&gt;
	    &lt;goodbye-component [myName]=&quot;name&quot;&gt;&lt;/goodbye-component&gt;
	    &lt;goodbye-component myName=&quot;Your World&quot;&gt;&lt;/goodbye-component&gt;
	  &lt;/div&gt;`,
	directives: [HelloComponent, GoodbyeComponent]
})
export class App {
  name: string;
  
  constructor() {
    this.name = &quot;World&quot;;
  }
}
</code></pre>
<p>&#x5148;&#x544A;&#x8A34;&#x5927;&#x5BB6;&#x986F;&#x793A;&#x7D50;&#x679C;&#x6703;&#x662F;</p>
<pre><code>Hello, World!

Hello, Other World!

Good Bye, World!

Good Bye, Your World!
</code></pre>
<p>&#x5148;&#x4F86;&#x770B;&#x770B;&#x53E6;&#x5916;&#x5169;&#x500B; Components &#x88E1;&#x9762;&#x662F;&#x751A;&#x9EBC;</p>
<pre><code>// app/hello.component.ts

import {Component, Input} from &apos;angular2/core&apos;;

@Component({
	selector: &apos;hello-component&apos;,
	template: &apos;&lt;p&gt;Hello, {{myName}}!&lt;/p&gt;&apos;,
	inputs: [&apos;myName&apos;]
})
export default class HelloComponent {
  myName: string;
  
  constructor() {}
}
</code></pre>
<pre><code>// app/goodbye.component.ts

import {Component, Input} from &apos;angular2/core&apos;;

@Component({
	selector: &apos;goodbye-component&apos;,
	template: &apos;&lt;p&gt;Good Bye, {{myName}}!&lt;/p&gt;&apos;,
})
export default class GoodbyeComponent {
  @Input()
  myName: string;
  
  constructor() {}
}
</code></pre>
<p>&#x5927;&#x5BB6;&#x4F86;&#x627E;&#x78B4;&#xFF0C;&#x627E;&#x5230;&#x4E0D;&#x4E00;&#x6A23;&#x7684;&#x5730;&#x65B9;&#x4E86;&#x55CE;&#xFF1F;</p>
<pre><code>...
@Component({
	selector: &apos;hello-component&apos;,
	template: &apos;&lt;p&gt;Hello, {{myName}}!&lt;/p&gt;&apos;,
	inputs: [&apos;myName&apos;]
})
...
</code></pre>
<pre><code>...
export default class GoodbyeComponent {
  @Input()
  myName: string;
  ...
}
</code></pre>
<p>&#x4E00;&#x500B;&#x662F;&#x653E;&#x5728; <code>@Component</code> &#x88E1;&#x9762;&#x52A0;&#x5165; <code>inputs</code>&#xFF0C;&#x4E00;&#x500B;&#x5247;&#x662F;&#x5728; <code>export</code> &#x52A0;&#x5165; <code>@Input</code>&#xFF0C;&#x5176;&#x5BE6;&#x5169;&#x500B;&#x65B9;&#x6CD5;&#x90FD;&#x53EF;&#x4EE5;&#xFF0C;&#x5F9E;&#x7BC4;&#x4F8B;&#x53EF;&#x4EE5;&#x770B;&#x5230; Hello &#x548C; GoodBye &#x5206;&#x5225;&#x63A1;&#x7528;&#x9019;&#x5169;&#x7A2E;&#x65B9;&#x6CD5;&#xFF0C;&#x90FD;&#x53EF;&#x4EE5;&#x6210;&#x529F;&#x57F7;&#x884C;&#x3002;</p>
<p>&#x6240;&#x4EE5; <code>@Input()</code> &#x662F;&#x5565;&#xFF1F;</p>
<p>&#x56DE;&#x5230; <code>AppComponent</code></p>
<pre><code>template: `&lt;div&gt;
            &lt;hello-component [myName]=&quot;name&quot;&gt;&lt;/hello-component&gt;
            &lt;hello-component myName=&quot;Other World&quot;&gt;&lt;/hello-component&gt;
            &lt;goodbye-component [myName]=&quot;name&quot;&gt;&lt;/goodbye-component&gt;
            &lt;goodbye-component myName=&quot;Your World&quot;&gt;&lt;/goodbye-component&gt;
          &lt;/div&gt;`,
</code></pre>
<p>&#x5728; <code>selector</code> &#x88E1;&#x9762;&#x6211;&#x5011;&#x6709;&#x770B;&#x5230; <code>myName</code>&#xFF0C;&#x9019;&#x500B;&#x5C31;&#x662F;&#x300C;&#x5411;&#x4E0B;&#x300D;&#x9023;&#x7D50;&#x7684;&#x610F;&#x601D;&#xFF0C;&#x525B;&#x525B;&#x6211;&#x5011;&#x5728; <code>@Input()</code> &#x5F8C;&#x9762;&#x5BA3;&#x544A; <code>myName</code> &#x5C31;&#x662F;&#x544A;&#x8A34; Child &#x4ED6;&#x7684; Parent &#x6703;&#x547C;&#x53EB;&#x4ED6;&#x3002;</p>
<pre><code>  ...
  @Input()
  myName: string;
  ...
</code></pre>
<p><code>[myname]=&quot;thisName&quot;</code> &#x5982;&#x679C;&#x9019;&#x6A23;&#x5BEB;&#x4EE3;&#x8868; Child &#x7684;&#x503C;&#x548C;&#x7576;&#x524D;&#x9019;&#x500B; Component &#x7684; <code>thisName</code> &#x9019;&#x500B;&#x8B8A;&#x6578;&#x505A;&#x7D81;&#x5B9A;&#xFF0C;&#x5982;&#x679C; <code>myname=&quot;Something&quot;</code> &#x5247;&#x662F;&#x76F4;&#x63A5;&#x5C07; <code>&quot;Something&quot;</code> &#x9019;&#x4E32;&#x503C;&#x6307;&#x5B9A;&#x7D66; Child&#x3002;</p>
<h2>@Output() &amp; outputs</h2>
<p><code>@Output</code>&#x662F;&#x7528;&#x4F86;&#x89F8;&#x767C;&#x7D44;&#x4EF6;&#x7684;&#x5BA2;&#x88FD;&#x5316;&#x4E8B;&#x4EF6;&#x4E26;&#x63D0;&#x4F9B;&#x4E00;&#x500B;&#x901A;&#x9053;&#x8B93;&#x7D44;&#x4EF6;&#x4E4B;&#x9593;&#x5F7C;&#x6B64;&#x6E9D;&#x901A;&#x3002;<br>
&#x4E00;&#x6A23;&#x5148;&#x770B;&#x770B; <a href="https://embed.plnkr.co/YrSUjChoi32eAT7vKEHw/" target="_blank">Plunker</a> &#x7BC4;&#x4F8B;&#x5427;&#xFF01;</p>
<p><img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-output.gif" alt></p>
<p><code>@Output()</code> &#x548C; <code>outputs</code> &#x72C0;&#x6CC1;&#x8DDF; <code>@Input()</code> &#x548C; <code>inputs</code> &#x4E00;&#x6A23;&#xFF0C;&#x5C31;&#x4E0D;&#x91CD;&#x8907;&#x8AAA;&#x660E;&#x4E86;&#x3002;</p>
<p>&#x73FE;&#x5728;&#x4F86;&#x7406;&#x89E3;&#x751A;&#x9EBC;&#x662F; <code>@Output()</code> &#x5427;&#xFF01;<br>
&#x525B;&#x525B;&#x8AAA;&#x904E; @Input &#x662F;&#x7531;&#x4E0A;&#x5230;&#x4E0B;&#x7684;&#x6982;&#x5FF5;&#xFF0C;&#x5C31;&#x662F; Parent &#x7D66;&#x5B9A;&#x751A;&#x9EBC;&#xFF0C;Child &#x5C31;&#x6703;&#x6709;&#x751A;&#x9EBC;&#x3002;<br>
<code>@Output</code> &#x4E0D;&#x4E00;&#x6A23;&#xFF0C;&#x662F;&#x7531;&#x4E0B;&#x5F71;&#x97FF;&#x4E0A;&#xFF0C;&#x610F;&#x601D;&#x5C31;&#x662F; Child &#x5148;&#x6709;&#x8B8A;&#x5316;&#xFF0C;&#x9032;&#x800C;&#x6539;&#x8B8A;&#x4E86; Parent&#x3002;<br>
&#x9019;&#x500B;&#x7BC4;&#x4F8B;&#x5C31;&#x662F;&#x7531; Child &#x7684;&#x6309;&#x9215;&#x57F7;&#x884C; Child &#x7684;&#x51FD;&#x6578;&#xFF0C;&#x9032;&#x800C;&#x56DE;&#x50B3;&#x7D66; Parent&#xFF0C;Parent &#x7684;&#x503C;&#x624D;&#x6539;&#x8B8A;&#x3002;</p>
<p>P.S. &#x9019;&#x908A;&#x5206;&#x5225;&#x7528;&#x5230;&#x4E09;&#x7A2E;&#x7D81;&#x5B9A;&#x65B9;&#x5F0F;&#xFF0C;&#x7528;&#x770B;&#x5F97;&#x6BD4;&#x8F03;&#x5FEB;&#xFF0C;&#x5C31;&#x4E0D;&#x8AAA;&#x660E;&#x4E86;</p>
 <br>
                                                    </div>
                    </div>
                
