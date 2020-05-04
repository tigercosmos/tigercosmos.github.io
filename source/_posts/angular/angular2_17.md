---
title: Angular 2 組件繼承 ( Component Inheritance )
date: 2017-01-02 23:39:11
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>Angular 2.3 &#x6700;&#x8FD1;&#x767C;&#x5E03;&#xFF0C;&#x800C;&#x6700;&#x6709;&#x7279;&#x8272;&#x7684;&#x90E8;&#x5206;&#x83AB;&#x904E;&#x65BC;&#x7D44;&#x4EF6;&#x7E7C;&#x627F; (Component Inheritance) &#x7684;&#x90E8;&#x5206;&#x4E86;&#x3002;&#x5982;&#x540C;&#x985E;&#x5225;&#x53EF;&#x4EE5;&#x7E7C;&#x627F;&#x4E00;&#x822C;&#xFF0C;&#x7D44;&#x4EF6;&#x7E7C;&#x627F;&#x53EF;&#x4EE5;&#x8B93;&#x7A0B;&#x5F0F;&#x78BC;&#x8B8A;&#x5F97;&#x66F4;&#x52A0;&#x5F37;&#x5927;&#x4E14;&#x66F4;&#x6709;&#x91CD;&#x8907;&#x4F7F;&#x7528;&#x6027;&#x3002;<br>
&#x6240;&#x4EE5;&#x7D44;&#x4EF6;&#x7E7C;&#x627F;&#x5E36;&#x4F86;&#x751A;&#x9EBC;&#xFF1F;</p>
<h2>&#x6982;&#x89C0;</h2>
<p>Component Inheritance &#x5305;&#x542B;&#x4E86;&#xFF1A;</p>
<ul>
<li>Metadata (decorator): &#x5B9A;&#x7FA9;&#x5728;&#x884D;&#x4F38;&#x7684;&#x985E;&#x5225;&#x7684; metadata &#x50CF;&#x662F; <code>@Input</code>&#x3001;<code>@Output</code> &#x7B49;&#xFF0C;&#x6703;&#x8986;&#x84CB;&#x5148;&#x524D;&#x6240;&#x6709;&#x5728;&#x7E7C;&#x627F;&#x93C8;&#x88E1;&#x9762;&#x7684; metadata&#xFF0C;&#x4E0D;&#x7136;&#x5247;&#x63A1;&#x7528;&#x57FA;&#x672C;&#x7684;&#x985E;&#x5225; (&#x7236;&#x985E;&#x5225;) &#x7684; metadata&#x3002;</li>
<li>Constructor: &#x5982;&#x679C;&#x884D;&#x4F38;&#x985E;&#x5225;&#x6C92;&#x6709; constructure&#xFF0C;&#x6703;&#x63A1;&#x7528;&#x57FA;&#x672C;&#x985E;&#x5225;&#x7684;&#x3002;&#x610F;&#x601D;&#x5C31;&#x662F;&#x8AAA;&#x6240;&#x4EE5;&#x6CE8;&#x5165;&#x5230; parent constructure &#x7684;&#x670D;&#x52D9;&#x6703;&#x88AB; child constructure &#x7E7C;&#x627F;&#x3002;</li>
<li>Lifecycle hooks: &#x751F;&#x547D;&#x9031;&#x671F;&#x9264;&#x5B50;&#x50CF;&#x662F; <code>ngOnInit</code>&#x3001;<code>ngOnChanges</code>&#x6703;&#x88AB;&#x547C;&#x53EB;&#xFF0C;&#x5C31;&#x7B97;&#x4ED6;&#x5011;&#x5728;&#x884D;&#x4F38;&#x985E;&#x5225;&#x6C92;&#x6709;&#x88AB;&#x5B9A;&#x7FA9;&#x3002;</li>
</ul>
<p>&#x7D44;&#x4EF6;&#x7E7C;&#x627F;&#x4E0D;&#x5305;&#x62EC; template &#x548C; style&#x3002;&#x4EFB;&#x4F55;&#x88AB;&#x5206;&#x4EAB;&#x7684; DOM &#x6216;&#x662F;&#x884C;&#x70BA;&#x90FD;&#x6703;&#x88AB;&#x5206;&#x5225;&#x7684;&#x8655;&#x7406;&#x3002;</p>
<h2>&#x85CD;&#x5716;</h2>
<p>&#x63A5;&#x8457;&#x8981;&#x5BE6;&#x969B;&#x505A;&#x7D44;&#x4EF6;&#x7E7C;&#x627F;&#x4E86;&#xFF0C;&#x60F3;&#x50CF;&#x4ECA;&#x5929;&#x6709;&#x500B;&#x7D44;&#x4EF6;&#x662F;&#x7528;&#x4F86;&#x505A;&#x300C;&#x5206;&#x9801;&#x300D;&#xFF0C;&#x4F60;&#x5F88;&#x559C;&#x6B61;&#x5B83;&#x7684;&#x6A23;&#x5B50;&#xFF0C;&#x529F;&#x80FD;&#x4E5F;&#x9054;&#x5230;&#x4F60;&#x7684;&#x671F;&#x671B;&#xFF0C;&#x6240;&#x4EE5;&#x4F60;&#x60F3;&#x8981;&#x4F7F;&#x7528;&#x5B83;&#xFF0C;&#x4F46;&#x4F60;&#x60F3;&#x8981;&#x7528;&#x81EA;&#x5DF1;&#x7684;&#x98A8;&#x683C;&#x3002;<br>
&#x53EF;&#x4EE5;&#x5148;&#x770B;&#x770B; <a href="https://embed.plnkr.co/hMgaYPVRiXMCiKBdfqHy/" target="_blank">Plunker</a> &#x5B8C;&#x6210;&#x5F8C;&#x7684;&#x6A23;&#x5B50;&#x3002;</p>
<p>&#x539F;&#x672C;&#x7684;&#x7D44;&#x4EF6;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular2_inheritance_1.PNG" alt></p>
<p>&#x6211;&#x5011;&#x6539;&#x7684;&#x7D44;&#x4EF6;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular2_inheritance_2.PNG" alt><br>
&#x6211;&#x5011;&#x5C07;&#x6539;&#x8B8A;&#xFF1A;</p>
<ul>
<li>&#x6309;&#x9215;&#x8B8A;&#x6210;&#x9023;&#x7D50;</li>
<li>&#x9801;&#x6578;&#x986F;&#x793A;&#x6539;&#x8B8A;</li>
</ul>
<h2>&#x52D5;&#x5DE5;</h2>
<p>&#x539F;&#x672C;&#x7684;&#x7D44;&#x4EF6;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>// simple-pagination.component.ts

import { Component, Input, Output, EventEmitter } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;simple-pagination&apos;,
  template: `
    &lt;button (click)=&quot;previousPage()&quot; [disabled]=&quot;!hasPrevious()&quot;&gt;Previous&lt;/button&gt; 
    &lt;button (click)=&quot;nextPage()&quot; [disabled]=&quot;!hasNext()&quot;&gt;Next&lt;/button&gt;

    &lt;p&gt;page {{ page }} of {{ pageCount }}&lt;/p&gt;
  `
})
export class SimplePaginationComponent {
  @Input() 
  pageCount: number;

  @Input()
  page: number;

  @Output()
  pageChanged = new EventEmitter&lt;number&gt;();

  nextPage() {
    this.page ++;
    this.pageChanged.emit(this.page);
  }

  previousPage() {
    this.page --;
    this.pageChanged.emit(this.page);
  }

  hasPrevious(): boolean { return +this.page &gt; 1; }

  hasNext(): boolean { return +this.page &lt; +this.pageCount; }

}
</code></pre>
<p>&#x4E00;&#x5207;&#x76E1;&#x5728; code &#x88E1;&#x3002;&#x7528;&#x5230;&#x5169;&#x500B;<code>@Input</code>&#x4F86;&#x5448;&#x73FE;&#x7576;&#x524D;&#x9801;&#x9762;&#x8207;&#x7E3D;&#x9801;&#x9762;&#x6578;&#x3002;&#x6BCF;&#x6B21;&#x9801;&#x9762;&#x8B8A;&#x63DB;&#x90FD;&#x6703;&#x89F8;&#x767C; <code>pageChanged</code> &#x4E8B;&#x4EF6;&#x3002;&#x7576;&#x9054;&#x5230;&#x6700;&#x524D;&#x9762;&#x6216;&#x6700;&#x5F8C;&#x9762;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x5C07;&#x6309;&#x9215;&#x9396;&#x4F4F;&#x3002;</p>
<p>&#x73FE;&#x5728;&#x6211;&#x5011;&#x6539;&#x4E00;&#x4E9B;&#x7A0B;&#x5F0F;&#x78BC;&#xFF0C;&#x8B8A;&#x6210;&#x65B0;&#x7684;&#x7D44;&#x4EF6;&#xFF0C;&#x4F46;&#x662F;&#x7528;&#x7E7C;&#x627F;&#x7684;&#x65B9;&#x5F0F;&#x3002;</p>
<pre><code>// my-pagination.component.ts

import { Component } from &apos;@angular/core&apos;;
import { SimplePaginationComponent } from &apos;./simple-pagination.component&apos;;

@Component({
  selector: &apos;my-pagination&apos;,
  template: `
    &lt;a (click)=&quot;previousPage()&quot; [class.disabled]=&quot;!hasPrevious()&quot; 
      href=&quot;javascript:void(0)&quot;&gt;
      &#xAB;&#xAB;
    &lt;/a&gt; 
    &lt;span&gt;{{ page }} / {{ pageCount }}&lt;/span&gt;
    &lt;a (click)=&quot;nextPage()&quot; [class.disabled]=&quot;!hasNext()&quot;
      href=&quot;javascript:void(0)&quot; &gt;
      &#xBB;&#xBB;
    &lt;/a&gt;
  `
})
export class MyPaginationComponent extends SimplePaginationComponent {
}
</code></pre>
<p>&#x9996;&#x5148;&#xFF0C;&#x6211;&#x5011;&#x5F15;&#x5165; <code>SimplePaginationComponent</code>&#xFF0C;&#x63A5;&#x8457; <code>extends</code> (&#x5EF6;&#x4F38;)<code>SimplePaginationComponent</code>&#x3002;&#x7136;&#x5F8C;&#x6211;&#x5011;&#x6539;&#x8B8A;&#x6A21;&#x677F;&#xFF0C;&#x8B8A;&#x6210;&#x7528;&#x8D85;&#x9023;&#x7D50;&#x7684;&#x65B9;&#x5F0F;&#x986F;&#x793A;&#x9801;&#x78BC;&#x3002;&#x7136;&#x5F8C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x6211;&#x5011;&#x5C07; <code>SimplePaginationComponent</code> &#x88E1;&#x9762;&#x7684; <code>inputs</code>&#x3001;<code>outputs</code> &#x548C; <code>function</code> &#x90FD;&#x7528;&#x5728;&#x6211;&#x5011;&#x7684;&#x65B0;&#x6A21;&#x677F;&#x4E2D;&#x4E86;&#x3002;</p>
<h2>&#x8986;&#x84CB; Parents&apos; &#x7684;&#x7279;&#x6027;</h2>
<p>&#x539F;&#x4F86;&#x7D44;&#x4EF6;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>// simple-pagination.component.ts

@Component({
  selector: &apos;simple-pagination&apos;,
  template: `
    &lt;button (click)=&quot;previousPage()&quot; [disabled]=&quot;!hasPrevious()&quot;&gt;{{ previousText }}&lt;/button&gt; 
    &lt;button (click)=&quot;nextPage()&quot; [disabled]=&quot;!hasNext()&quot;&gt;{{ nextText }}&lt;/button&gt;

    &lt;p&gt;page {{ page }} of {{ pageCount }}&lt;/p&gt;
  `
})
export class SimplePaginationComponent {
  ...

  @Input()
  previousText = &apos;Previous&apos;;

  @Input()
  nextText = &apos;Next&apos;;

  ...

}
</code></pre>
<p>&#x73FE;&#x5728;&#x6211;&#x4E0D;&#x60F3;&#x8981;  <code>previousText</code> &#x548C; <code>nextText</code> &#x88E1;&#x9762;&#x7684;&#x6A23;&#x5B50;&#xFF0C;&#x5728;&#x6211;&#x5011;&#x5EFA;&#x7ACB;&#x7684;&#x7E7C;&#x627F;&#x7D44;&#x4EF6;&#x4E2D;&#xFF0C;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x91CD;&#x5BEB;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x8986;&#x84CB;&#x6389;&#x4ED6;&#x5011;&#xFF0C;&#x800C;&#x6C92;&#x52D5;&#x7684;&#x5730;&#x65B9;&#x5247;&#x662F;&#x7E7C;&#x7E8C;&#x7E7C;&#x627F;&#x3002;</p>
<pre><code>// my-pagination.component.ts

...
...

export class MyPaginationComponent extends SimplePaginationComponent {
  @Input()
  previousText = &apos;&lt;&lt;&apos;; // &#x8986;&#x84CB;&#x539F;&#x672C;&#x7684;&#x6587;&#x5B57;

  @Input()
  nextText = &apos;&gt;&gt;&apos;; // &#x8986;&#x84CB;&#x539F;&#x672C;&#x7684;&#x6587;&#x5B57;

  ...
}
</code></pre>
<h2>Child &#x52A0;&#x5165;&#x65B0;&#x7279;&#x6027;</h2>
<p>&#x90A3;&#x6211;&#x5011;&#x60F3;&#x8981;&#x5728;&#x7E7C;&#x627F;&#x7684;&#x7D44;&#x4EF6;&#x4E2D;&#x589E;&#x52A0;&#x6771;&#x897F;&#x600E;&#x9EBC;&#x8FA6;&#xFF1F;<br>
&#x53EA;&#x8981;&#x5728;&#x539F;&#x672C;&#x7684;&#x7D44;&#x4EF6;&#x4E0A;&#x9762;&#x5148;&#x5B9A;&#x7FA9;&#x597D;&#x6211;&#x5011;&#x8981;&#x7684;&#x7279;&#x6027;&#xFF0C;&#x4F46;&#x662F;&#x4E0D;&#x4F7F;&#x7528;&#x5B83;&#xFF0C;&#x7136;&#x5F8C;&#x5728;&#x7E7C;&#x627F;&#x7684;&#x7D44;&#x4EF6;&#x4E0A;&#x52A0;&#x4E0A; <code>@Input</code>&#xFF0C;&#x9019;&#x6A23;&#x7E7C;&#x627F;&#x7684;&#x7D44;&#x4EF6;&#x4E4B;&#x5F8C;&#x5C31;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x7528;&#x5B9A;&#x7FA9;&#x904E;&#x7684;&#x7279;&#x6027;&#x4F86;&#x6539;&#x8B8A;&#x4E86;&#xFF01;</p>
<pre><code> // my-pagination.component.ts
 
@Component({

...

export class MyPaginationComponent extends SimplePaginationComponent {
  @Input()
  title: string; // &#x53EA;&#x7528;&#x4F86;&#x6539; child component 

  ...
}
</code></pre>
 <br>
                                                    </div>
                    </div>
                
