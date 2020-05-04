---
title: Angular 2 製作 tab 元件
date: 2017-01-12 23:42:15
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>tab &#x5C31;&#x662F;&#x53EF;&#x4EE5;&#x5206;&#x9801;&#x7684;&#x6A19;&#x7C64;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/tab.PNG" alt></p>
<p>&#x5982;&#x679C;&#x6709;&#x7528; Bootstrap&#xFF0C;&#x90A3;&#x8981;&#x7528; tab &#x5C31;&#x6703;&#x5F88;&#x7C21;&#x55AE;&#x3002;</p>
<pre><code>&lt;ul class=&quot;nav nav-tabs&quot;&gt;
    &lt;li class=&quot;active&quot;&gt;&lt;a data-toggle=&quot;tab&quot; href=&quot;#home&quot;&gt;Home&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a data-toggle=&quot;tab&quot; href=&quot;#menu1&quot;&gt;Menu 1&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a data-toggle=&quot;tab&quot; href=&quot;#menu2&quot;&gt;Menu 2&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a data-toggle=&quot;tab&quot; href=&quot;#menu3&quot;&gt;Menu 3&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;

&lt;div class=&quot;tab-content&quot;&gt;
    &lt;div id=&quot;home&quot; class=&quot;tab-pane fade in active&quot;&gt;
      &lt;h3&gt;HOME&lt;/h3&gt;
      &lt;p&gt;......&lt;/p&gt;
    &lt;/div&gt;
    &lt;div id=&quot;menu1&quot; class=&quot;tab-pane fade&quot;&gt;
      &lt;h3&gt;Menu 1&lt;/h3&gt;
      &lt;p&gt;......&lt;/p&gt;
    &lt;/div&gt;
    &lt;div id=&quot;menu2&quot; class=&quot;tab-pane fade&quot;&gt;
      &lt;h3&gt;Menu 2&lt;/h3&gt;
      &lt;p&gt;......&lt;/p&gt;
    &lt;/div&gt;
    &lt;div id=&quot;menu3&quot; class=&quot;tab-pane fade&quot;&gt;
      &lt;h3&gt;Menu 3&lt;/h3&gt;
      &lt;p&gt;......&lt;/p&gt;
    &lt;/div&gt;
&lt;/div&gt;
</code></pre>
<p>&#x4F46;&#x6211;&#x5011;&#x4ECA;&#x5929;&#x7528; Angular 2 &#x4F86;&#x786C;&#x5E79;&#x4E00;&#x500B;&#xFF01;</p>
<h2>Tab</h2>
<p>&#x5BE6;&#x73FE;&#x4E00;&#x500B; tab &#x5927;&#x6982;&#x6703;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>&lt;tabs&gt;
    &lt;tab&gt;
        &lt;p&gt;This Tab Content 1&lt;/p&gt;
    &lt;/tab&gt;
    &lt;tab&gt;
        &lt;p&gt;This Tab Content 1&lt;/p&gt;
    &lt;/tab&gt;
    &lt;tab&gt;
        &lt;p&gt;This Tab Content 1&lt;/p&gt;
    &lt;/tab&gt;
&lt;/tabs&gt;
</code></pre>
<p>&#x6211;&#x5011;&#x4E26;&#x4E0D;&#x60F3;&#x5BEB;&#x6210;&#x9019;&#x6A23;</p>
<pre><code>&lt;tabs [contents]=&quot;[...]&quot;&gt;&lt;/tabs&gt;
</code></pre>
<p>&#x628A;&#x6240;&#x6709; <code>tab</code> &#x7684;&#x5167;&#x5BB9;&#x7576;&#x8B8A;&#x6578;&#x50B3;&#x905E;&#xFF0C;&#x9019;&#x6703;&#x589E;&#x52A0;&#x95B1;&#x8B80;&#x7684;&#x96E3;&#x5EA6;&#x3002;&#x6211;&#x5011;&#x60F3;&#x8981;&#x7684;&#x662F;&#x986F;&#x793A;&#x5C64;&#x6B21;&#x660E;&#x78BA;&#x7684;&#x6A23;&#x5B50;&#xFF0C;&#x9019;&#x6A23;&#x7684;&#x8A71;&#x5C31;&#x6703;&#x7528;&#x5230; <code>@ContentChild</code> &#x88DD;&#x98FE;&#x5668;&#x3002;</p>
<h4>tab.ts</h4>
<pre><code>import {Component,Input} from &apos;@angular/core&apos;;

@Component({
    selector: &apos;tab&apos;,
    template: `
        &lt;p [hidden]=&quot;!show&quot;&gt;
            &lt;ng-content&gt;&lt;/ng-content&gt;
        &lt;/p&gt;
    `
})
export class TabComponent {
    @Input()
    tabTitle:string;

    show:boolean = false;
}
</code></pre>
<h4>tabs.ts</h4>
<pre><code>import {Component,ContentChildren,QueryList,AfterContentInit} from &apos;@angular/core&apos;;
import {TabComponent} from &apos;./tab&apos;;

@Component({
    selector: &apos;tabs&apos;,
    template: `
       &lt;ul class=&quot;tab-list&quot;&gt;
           &lt;li *ngFor=&quot;let tab of tabs&quot; [class.active]=&quot;selectedTab===tab&quot; (click)=&quot;onSelect(tab)&quot;&gt;
               {{tab.tabTitle}}
           &lt;/li&gt;
       &lt;/ul&gt;
       &lt;ng-content&gt;&lt;/ng-content&gt;
    `,
    styles: [`
        .tab-list{
            list-style:none;
            overflow:hidden;
            padding:0;
            color: white;
        }

        .tab-list li{
            cursor:pointer;
            float:left;
            width:60px;
            height:30px;
            line-height:30px;
            text-align:center;
            background-color:gray;
        }

        .tab-list li:hover{
            background-color:#424242;
        }
        .tab-list li.active{
            background-color:black;
        }
    `]
})
export class TabsComponent implements AfterContentInit {
    @ContentChildren(TabComponent)
    tabs:QueryList&lt;TabComponent&gt;;
    
    selectedTab:TabComponent;

    ngAfterContentInit() {
        this.select(this.tabs.first);
    }

    onSelect(tab) {
        this.select(tab);
    }

    select(tab) {
        this.tabs.forEach((item)=&gt;{
            item.show = false;
        });

        this.selectedTab = tab;
        this.selectedTab.show = true;
    }
}
</code></pre>
<h4>app.ts</h4>
<pre><code>import {Component,ContentChildren,QueryList} from &apos;@angular/core&apos;;
import {TabsComponent} from &apos;./tabs&apos;;
import {TabComponent} from &apos;./tab&apos;;

@Component({
    selector: &apos;my-app&apos;,
    template: `
        &lt;h2&gt;App Component&lt;/h2&gt;
        &lt;tabs&gt;
            &lt;tab tabTitle=&quot;First&quot;&gt;
                &lt;p&gt;This Tab Content 1&lt;/p&gt;
            &lt;/tab&gt;
            &lt;tab tabTitle=&quot;Second&quot;&gt;
                &lt;p&gt;This Tab Content 2&lt;/p&gt;
            &lt;/tab&gt;
            &lt;tab tabTitle=&quot;third&quot;&gt;
                &lt;p&gt;This Tab Content 3&lt;/p&gt;
            &lt;/tab&gt;
        &lt;/tabs&gt;
    `,
    directives: [TabsComponent,TabComponent]
})
export class AppComponent {
}
</code></pre>
<h2>&#x7BC4;&#x4F8B;</h2>
<p><a href="https://embed.plnkr.co/2zem4NLqda8F7KlUQd68/" target="_blank">Plunker</a><br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/tab.gif" alt></p>
 <br>
                                                    </div>
                    </div>
                
