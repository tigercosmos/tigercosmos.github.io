---
title: Angular 2 @Directive
date: 2017-01-13 23:24:36
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>Directive (&#x6307;&#x4EE4;) &#x5728; Angular &#x53EF;&#x4EE5;&#x6307;&#x5F88;&#x591A;&#x7A2E;&#x60C5;&#x5F62;&#xFF0C;&#x9019;&#x908A;&#x6211;&#x5C08;&#x9580;&#x8A0E;&#x8AD6; <code>@Directive</code>&#x3002;<code>@Directive</code> &#x901A;&#x5E38;&#x7528;&#x5728;&#x5C6C;&#x6027;&#x6307;&#x4EE4;&#x7684;&#x7D81;&#x5B9A;&#x4E0A;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5728; selector &#x4E0A;&#x9762;&#x52A0;&#x4E0A;&#x5C6C;&#x6027;&#xFF0C;&#x5DEE;&#x6240;&#x63A7;&#x5236;&#x7684;&#x985E;&#x5225;&#x6703;&#x5BE6;&#x9AD4;&#x5316;&#x6211;&#x5011;&#x6240;&#x8A2D;&#x8A08;&#x7684;&#x884C;&#x70BA;&#x6307;&#x4EE4;&#x3002;</p>
<blockquote>
<p>&#x4E00;&#x822C;&#x800C;&#x8A00;&#xFF0C;&#x592A;&#x7C21;&#x55AE;&#x7684; style &#x4E0D;&#x6703;&#x7528;&#x5230; <code>@Directive</code>&#xFF0C;&#x5148;&#x524D;&#x6709;&#x4ECB;&#x7D39;&#x591A;&#x7A2E;&#x52A0;&#x5165; style &#x7684;&#x65B9;&#x6CD5;&#x3002;&#x901A;&#x5E38;&#x6709;&#x4E92;&#x52D5;&#x7684; style &#x624D;&#x6703;&#x4F7F;&#x7528; <code>@Directive</code>&#x3002;</p>
</blockquote>
<h2>&#x4F7F;&#x7528;</h2>
<p>&#x76F4;&#x63A5;&#x770B;&#x7BC4;&#x4F8B; <a href="https://embed.plnkr.co/OR0H2lFS8o2Dkc34hBiy/" target="_blank">Plunker</a><br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-directive.gif" alt></p>
<h4>highlight.directive.ts</h4>
<pre><code>import { Directive, ElementRef, HostListener, Input } from &apos;@angular/core&apos;;

@Directive({
  selector: &apos;[myHighlight]&apos;
})
export class HighlightDirective {

  constructor(private el: ElementRef) { }

  @Input() defaultColor: string;

  @Input(&apos;myHighlight&apos;) highlightColor: string;

  @HostListener(&apos;mouseenter&apos;) onMouseEnter() {
    this.highlight(this.highlightColor || this.defaultColor || &apos;red&apos;);
  }

  @HostListener(&apos;mouseleave&apos;) onMouseLeave() {
    this.highlight(null);
  }

  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
</code></pre>
<ul>
<li>
<code>ElementRef</code>&#xFF1A; &#x7528;&#x4F86;&#x5C0D; DOM &#x8655;&#x7406;</li>
<li>
<code>HostListener</code>&#xFF1A; &#x5075;&#x6E2C;&#x4E8B;&#x4EF6;</li>
</ul>
<p>&#x9019;&#x908A;&#x5C31;&#x662F;&#x5075;&#x6E2C;&#x5230;&#x4E8B;&#x4EF6;&#xFF0C;&#x6539;&#x8B8A; DOM &#x7684; style &#x4E2D;&#x7684;&#x80CC;&#x666F;&#x984F;&#x8272;&#x3002;</p>
<pre><code>@Input(&apos;myHighlight&apos;) highlightColor: string;
</code></pre>
<p><code>myHighlight</code> &#x5728;&#x9019;&#x908A;&#x662F;&#x5225;&#x540D;&#xFF0C;&#x8B93;&#x5225;&#x4EBA;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;&#x9019;&#x7A31;&#x865F;&#x547C;&#x53EB;&#x4ED6;&#x3002;</p>
<p>&#x53EF;&#x4EE5;&#x770B;&#x5230;</p>
<pre><code>@Directive({
  selector: &apos;[myHighlight]&apos;
})
</code></pre>
<p>&#x53C8;&#x770B;&#x5230; <code>app.component.html</code> &#x4E2D;</p>
<pre><code>&lt;p [myHighlight]=&quot;color&quot;&gt;...&lt;/p&gt; // &#x55AE;&#x5411;&#x7D81;&#x5B9A;
&lt;p myHighlight=&quot;orange&quot;&gt;...&lt;/p&gt; // &#x5BEB;&#x6B7B;
</code></pre>
<p><code>@Derective</code>&#x5B9A;&#x7FA9;&#x597D; <code>selector</code> &#x4E4B;&#x5F8C;&#x5C31;&#x53EF;&#x4EE5;&#x653E;&#x5230;&#x6A21;&#x677F; <code>tag</code> &#x6216;&#x5225;&#x7684; <code>selector</code> &#x88E1;&#x9762;&#x3002;</p>
<p>&#x9019;&#x6A23;&#x5982;&#x4F55;&#x4F7F;&#x7528; <code>@Derective</code> &#x5927;&#x5BB6;&#x61C9;&#x8A72;&#x5C31;&#x6E05;&#x695A;&#x4E86;&#xFF01;&#xFF01;</p>
 <br>
                                                    </div>
                    </div>
                
