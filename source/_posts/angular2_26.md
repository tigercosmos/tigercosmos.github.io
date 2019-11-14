---
title: Angular 2 裝飾器 @ViewChild
date: 2017-01-11 23:09:38
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x9023;&#x7E8C;&#x767C;&#x4E86; 20 &#x5E7E;&#x5929;&#x7684;&#x6587;&#xFF0C;&#x80FD;&#x8B1B;&#x7684;&#x4E5F;&#x90FD;&#x8B1B;&#x4E86;&#xFF0C;&#x9081;&#x5411;&#x795E;&#x4E4E;&#x5176;&#x6280;&#x4E4B;&#x8DEF;&#x53EA;&#x5269;&#x4E0B;&#x638C;&#x63E1;&#x5C0F;&#x5730;&#x65B9;&#x4E86;&#x5427;&#xFF01;<br>
&#x4E4B;&#x524D;&#x4ECB;&#x7D39;&#x904E; <code>&lt;ng-content&gt;</code> &#x8DDF; <code>ContentChild</code>&#xFF0C;&#x9084;&#x6709;&#x500B;&#x5F88;&#x985E;&#x4F3C;&#x7684;&#x662F; <code>@ViewChild</code>&#x88DD;&#x98FE;&#x5668;&#xFF0C;&#x63A5;&#x8457;&#x5C31;&#x4F86;&#x770B;&#x770B;&#x9019;&#x662F;&#x751A;&#x9EBC;&#x5427;&#xFF01;</p>
<p>&#x9019;&#x7BC7;&#x5EFA;&#x8B70;&#x642D;&#x914D;<a href="http://ithelp.ithome.com.tw/articles/10188796" target="_blank">&#x524D;&#x4E00;&#x7BC7;</a>&#x4E00;&#x8D77;&#x770B;&#x3002;</p>
<h2>@ViewChild</h2>
<p>&#x76F4;&#x63A5;&#x4F86;&#x770B;<a href="https://embed.plnkr.co/W15xez8iP7O67SMfXFrL/" target="_blank">&#x7BC4;&#x4F8B;</a>&#xFF0C;&#x9019;&#x500B;&#x7BC4;&#x4F8B;&#x5927;&#x81F4;&#x8DDF; <code>@ContentChild</code> &#x7684;<a href="https://embed.plnkr.co/rSmStf53EZx4Dh4AlI1g/" target="_blank">&#x7BC4;&#x4F8B;</a>&#x5F88;&#x50CF;&#xFF0C;&#x4F46;&#x505A;&#x4E86;&#x4E00;&#x9EDE;&#x4FEE;&#x6539;&#xFF0C;&#x665A;&#x9EDE;&#x6211;&#x5011;&#x6703;&#x505A;&#x6BD4;&#x8F03;&#x3002;</p>
<h4>app.ts</h4>
<pre><code>import {Component}       from &apos;angular2/core&apos;;
import {ParentComponent} from &apos;./parent&apos;;
import {ChildComponent}  from &apos;./child&apos;;

@Component({
    selector: &apos;my-app&apos;,
    template: `
        &lt;h2&gt;App Component&lt;/h2&gt;
        &lt;my-parent&gt;&lt;/my-parent&gt;
    `,
    directives:[ParentComponent,ChildComponent]
})
export class AppComponent {
}
</code></pre>
<p>&#x6CE8;&#x610F;&#x5230; <code>&lt;my-parent&gt;&lt;/my-parent&gt;</code> &#x88E1;&#x9762;&#x4E0D;&#x7528;&#x5305; <code>&lt;my-child&gt;</code> &#x4E86;&#x3002;</p>
<h4>child.ts</h4>
<pre><code>import {Component} from &apos;angular2/core&apos;;

@Component({
    selector: &apos;my-child&apos;,
    template: `
        &lt;div&gt;Child Component&lt;/div&gt;
    `
})
export class ChildComponent {
    name:string = &apos;childName&apos;;
}
</code></pre>
<p><code>child</code> &#x4FDD;&#x6301;&#x4E0D;&#x8B8A;</p>
<h4>parent.ts</h4>
<pre><code>import {Component,ViewChild,AfterViewInit} from &apos;angular2/core&apos;;
import {ChildComponent}         from &apos;./child&apos;;

@Component({
    selector: &apos;my-parent&apos;,
    template: `
       &lt;div&gt;Parent Component&lt;/div&gt;
       &lt;my-child&gt;&lt;/my-child&gt;
    `,
    directives:[ChildComponent]
})
export class ParentComponent implements AfterViewInit{
    @ViewChild(ChildComponent)
    child:ChildComponent;

    ngAfterViewInit() {
        console.log(this.child)
    }
}
</code></pre>
<p>&#x6539;&#x6210;&#x7528; <code>@ViewChild</code>&#xFF0C;&#x4E00;&#x6A23;&#x53EF;&#x4EE5;&#x53D6;&#x5F97; child &#x7684;&#x7D44;&#x4EF6;&#x5167;&#x5BB9;&#xFF0C;&#x4E0D;&#x904E;&#x8981;&#x5728; <code>AfterViewInit</code> &#x4E4B;&#x5F8C;&#x624D;&#x6703;&#x751F;&#x6548;&#x3002;</p>
<p>&#x5982;&#x679C;&#x6539;&#x6210;&#x9019;&#x6A23;</p>
<pre><code>template: `
       &lt;div&gt;Parent Component&lt;/div&gt;
       &lt;my-child&gt;&lt;/my-child&gt;
       &lt;p&gt;{{child.name}}&lt;/p&gt;
    `
</code></pre>
<p>&#x5247;&#x6703;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-ViewChild_err.PNG" alt><br>
&#x56E0;&#x70BA;&#x4F60;&#x5728;&#x4ED6;&#x751F;&#x6548;&#x524D;&#x5C31;&#x547C;&#x53EB;&#x4E86;&#xFF01;</p>
<hr>
<p><a href="https://embed.plnkr.co/W15xez8iP7O67SMfXFrL/" target="_blank">Plunker</a></p>
<p>&#x53EF;&#x4EE5;&#x770B;&#x5230; child &#x5728; parent &#x4E2D;&#x88AB;&#x547C;&#x53EB;&#x4E86;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-ViewChild.PNG" alt></p>
<p>&#x6240;&#x4EE5; <code>@ViewChild</code> &#x8DDF;&#x76F4;&#x63A5;&#x5F15;&#x5165;&#x7D44;&#x4EF6;&#x4F7F;&#x7528;&#x5DEE;&#x5728;&#x54EA;&#xFF1F;</p>
<p>&#x5DEE;&#x5728;&#x5982;&#x679C;&#x6211;&#x5011;&#x5728; parent &#x7684;&#x6A21;&#x677F;&#x6C92;&#x6709;&#x4F7F;&#x7528;&#x5230; <code>&lt;my-child&gt;</code> &#x7684;&#x8A71;&#xFF0C;<code>@ViewChild</code> &#x5C31;&#x6703;&#x7121;&#x6CD5;&#x8ABF;&#x7528; child &#x7684;&#x7D44;&#x4EF6;&#x5167;&#x5BB9;&#x3002;&#x800C;&#x5982;&#x679C;&#x76F4;&#x63A5;&#x5F15;&#x7528; child &#x7D44;&#x4EF6;&#x7684;&#x8A71;&#xFF0C;&#x4E0D;&#x4F7F;&#x7528;&#x6A19;&#x7C64;&#x4E5F;&#x6C92;&#x95DC;&#x4FC2;&#x3002;</p>
<h2>&#x5340;&#x5206; @ContentChild &#x548C; @ViewChild</h2>
<ul>
<li>
<code>@ContentChild</code> &#x662F;&#x7D44;&#x4EF6;&#x4E2D; <code>selector</code> &#x6A19;&#x7C64;&#x9589;&#x5408;&#x4E4B;&#x9593;&#x7684;&#x5B50;&#x7D44;&#x4EF6;&#xFF0C;&#x610F;&#x601D;&#x5C31;&#x662F;&#x5728; <code>AppComponent</code> &#x4E2D; <code>&lt;my-parent&gt;</code> &#x88E1;&#x9762;&#x5FC5;&#x9808;&#x8981;&#x5305;&#x542B; <code>&lt;my-child&gt;</code>&#xFF0C;&#x63DB;&#x8A00;&#x4E4B;&#x6C7A;&#x5B9A;&#x6B0A;&#x5728;&#x300C;&#x4F7F;&#x7528; <code>&lt;my-parent&gt;</code> &#x7684;&#x7D44;&#x4EF6;&#x300D;&#x624B;&#x4E0A;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6709; <code>@ContentChild</code> &#x7684;&#x4E0A;&#x4E00;&#x5C64;&#x3002;</li>
<li>
<code>@ViewChild</code> &#x662F;&#x7D44;&#x4EF6;&#x6A21;&#x677F;&#x7576;&#x4E2D;&#x7684;&#x5B50;&#x7D44;&#x4EF6;&#xFF0C;&#x6C7A;&#x5B9A;&#x6B0A;&#x5728;&#x7576;&#x524D;&#x7D44;&#x4EF6;&#x3002;</li>
</ul>
<p>&#x5169;&#x8005;&#x90FD;&#x6709;&#x8907;&#x6578;&#x5F62;&#x5F0F;&#xFF0C;<code>@ContentChildren</code> &#x548C; <code>@ViewChildren</code></p>
<p>&#x4EC0;&#x9EBC;&#x6642;&#x5019;&#x7372;&#x53D6;&#x5230;&#x5B50;&#x7D44;&#x4EF6;&#x7684;&#x503C;&#xFF1F;</p>
<ul>
<li>
<code>@ContentChild</code> &#x5728;&#x7236;&#x7D44;&#x4EF6;&#x751F;&#x547D;&#x9031;&#x671F;&#x51FD;&#x6578; <code>ngAfterContentInit</code> &#x4E4B;&#x5F8C;&#x53EF;&#x4EE5;&#x7372;&#x53D6;&#x5230;</li>
<li>
<code>@ViewChild</code> &#x5728;&#x7236;&#x7D44;&#x4EF6;&#x751F;&#x547D;&#x9031;&#x671F;&#x51FD; <code>ngAfterViewInit</code> &#x4E4B;&#x5F8C;&#x53EF;&#x4EE5;&#x7372;&#x53D6;&#x5230;</li>
</ul>
 <br>
                                                    </div>
                    </div>
                
