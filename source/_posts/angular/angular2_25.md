---
title: Angular 2 裝飾器 @ContentChild
date: 2017-01-10 22:34:53
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x4E4B;&#x524D;&#x5728;<a href="https://ithelp.ithome.com.tw/articles/10187991" target="_blank">&#x9019;&#x7BC7;</a>&#x4ECB;&#x7D39;&#x904E; <code>&lt;ng-content&gt;</code> &#x53EF;&#x4EE5;&#x9054;&#x6210;&#x5D4C;&#x5165;&#x5F0F;&#x8A2D;&#x8A08;&#xFF0C;&#x4F46;&#x662F;&#x900F;&#x904E;&#x9019;&#x7A2E;&#x65B9;&#x6CD5;&#x53EA;&#x80FD;&#x505A;&#x5230;&#x6A21;&#x677F;&#x7684;&#x90E8;&#x5206;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x5728; A &#x6A21;&#x677F;&#x4E2D;&#x5D4C;&#x5165; B &#x6A21;&#x677F;&#xFF0C;&#x8981;&#x662F;&#x60F3;&#x5728; A &#x4E2D;&#x9806;&#x4FBF;&#x5D4C;&#x5165; B &#x7684;&#x7D44;&#x4EF6;&#x5167;&#x5BB9;&#x5462;&#xFF1F;</p>
<p>&#x4E0D;&#x592A;&#x7406;&#x89E3;&#x6587;&#x5B57;&#x7684;&#x610F;&#x601D;&#xFF1F;&#x7E7C;&#x7E8C;&#x770B;&#x4E0B;&#x53BB;&#x3002;</p>
<h2>ContentChild</h2>
<p>app.ts</p>
<pre><code>import {Component}       from &apos;angular2/core&apos;;
import {ParentComponent} from &apos;./parent&apos;;
import {ChildComponent}  from &apos;./child&apos;;

@Component({
    selector: &apos;my-app&apos;,
    template: `
        &lt;h2&gt;App Component&lt;/h2&gt;
        &lt;my-parent&gt;
           &lt;my-child&gt;&lt;/my-child&gt;
        &lt;/my-parent&gt;
    `,
    directives:[ParentComponent,ChildComponent]
})
export class AppComponent {
}
</code></pre>
<p>&#x4E3B;&#x7A0B;&#x5F0F;&#x7684;&#x6A23;&#x5B50;&#xFF0C;&#x8981;&#x6C42; <code>&lt;my-parent&gt;</code> &#x88E1;&#x9762;&#x5305;&#x8457;&#x4E00;&#x500B; <code>&lt;my-child&gt;</code></p>
<p>child.ts</p>
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
<p><code>name</code> &#x662F;&#x6211;&#x5011;&#x5F85;&#x6703;&#x6703;&#x7528;&#x5230;&#x7684;&#x6771;&#x897F;&#x3002;</p>
<p>parent.ts</p>
<pre><code>import {Component,ContentChild} from &apos;angular2/core&apos;;
import {ChildComponent}         from &apos;./child&apos;;

@Component({
    selector: &apos;my-parent&apos;,
    template: `
        &lt;div&gt;Parent Component&lt;/div&gt;
        &lt;ng-content&gt;&lt;/ng-content&gt;
        &lt;p&gt;{{child.name}}&lt;/p&gt;
    `
})
export class ParentComponent {
    @ContentChild(ChildComponent)
    child:ChildComponent;
}
</code></pre>
<p><code>&lt;p&gt;{{child.name}}&lt;/p&gt;</code> &#x9019;&#x908A;&#x8981;&#x6C42; <code>child:ChildComponent</code> &#x7684;&#x7269;&#x4EF6;&#xFF0C;&#x4E5F;&#x5C31;&#x662F; parent &#x76F4;&#x63A5;&#x8ABF;&#x7528; child &#x7684;&#x5167;&#x5BB9;&#xFF0C;&#x9019;&#x908A;&#x662F;&#x900F;&#x904E; <code>@ContentChild</code> &#x4F86;&#x8655;&#x7406;&#xFF0C; &#x5176;&#x5BE6;&#x5C31;&#x8DDF;&#x6CE8;&#x5165;&#x7684;&#x6982;&#x5FF5;&#x5F88;&#x50CF;&#x3002;</p>
<p><a href="https://embed.plnkr.co/rSmStf53EZx4Dh4AlI1g/" target="_blank">Plunker</a><br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/angular-contentChild.PNG" alt></p>
 <br>
                                                    </div>
                    </div>
                
