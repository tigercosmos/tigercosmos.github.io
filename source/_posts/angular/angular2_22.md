---
title: Angular 2 + Ionic = Mobile App ( 3 ) 實作 Todo List
date: 2017-01-07 23:39:58
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x5EFA;&#x7ACB;&#x5C08;&#x6848;</h2>
<p>&#x4E0A;&#x56DE;&#x6211;&#x5011;&#x5DF2;&#x7D93;&#x8AAA;&#x660E;&#x5982;&#x4F55;&#x5EFA;&#x7ACB;&#x4E00;&#x500B;&#x5C08;&#x6848;&#xFF0C;&#x800C;&#x9019;&#x6B21;&#x6211;&#x5011;&#x7528;&#x7D93;&#x5178;&#x7684; Todo List (&#x5099;&#x5FD8;&#x9304;) &#x4F86;&#x505A;&#x8AAA;&#x660E;</p>
<pre><code>ionic start TODOApp blank --v2
</code></pre>
<p><code>blank</code> &#x5C31;&#x662F;&#x7A7A;&#x767D;&#x7684;&#x6A21;&#x677F;</p>
<p>&#x4E0A;&#x56DE;&#x4ECB;&#x7D39;&#x904E; Ionic &#x5C08;&#x6848;&#x7684;&#x67B6;&#x69CB;&#xFF0C;&#x4ECA;&#x5929;&#x6211;&#x5011;&#x90FD;&#x6703;&#x8457;&#x91CD;&#x5728; <code>scr</code> &#x7684;&#x90E8;&#x5206;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x7A0B;&#x5F0F;&#x4E3B;&#x5E79;&#x3002;</p>
<h2>&#x6210;&#x54C1;</h2>
<p>&#x5148;&#x770B;&#x770B;&#x7D50;&#x679C;<br>
<img src="https://raw.githubusercontent.com/tigercosmos/webImg/master/todo-sample.gif" alt></p>
<p><a href="https://github.com/tigercosmos/Todo_List_Sample" target="_blank">&#x9019;&#x908A;</a>&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x6211;&#x5B8C;&#x6210;&#x7684;&#x5C08;&#x6848;</p>
<h2>&#x5EFA;&#x7ACB;&#x9801;&#x9762;</h2>
<p><code>scr/pages</code> &#x662F;&#x6211;&#x5011;&#x7684; App &#x88E1;&#x9762;&#x6709;&#x7684;&#x9801;&#x9762;&#xFF0C;App &#x7684;&#x5404;&#x7A2E;&#x756B;&#x9762;&#xFF0C;&#x5C31;&#x7B49;&#x540C;&#x65BC;&#x7DB2;&#x9801;&#x7684;&#x5404;&#x500B;&#x9801;&#x9762;&#x3002;</p>
<p>&#x4E00;&#x500B;&#x7C21;&#x55AE;&#x7684; TODO&#xFF0C;&#x5305;&#x542B;&#xFF1A;</p>
<ul>
<li>&#x9996;&#x9801;&#xFF1A;&#x5448;&#x73FE;&#x6240;&#x6709;&#x4E8B;&#x9805;</li>
<li>&#x7D30;&#x7BC0;&#xFF1A;&#x6AA2;&#x8996;&#x8A73;&#x7D30;&#x5167;&#x5BB9;</li>
<li>&#x589E;&#x52A0;&#xFF1A;&#x589E;&#x52A0;&#x4E8B;&#x9805;&#x7684;&#x756B;&#x9762;</li>
</ul>
<p>&#x7A7A;&#x767D;&#x5C08;&#x6848;&#x5DF2;&#x7D93;&#x6709; <code>scr/pages/home</code> &#x4E86;&#xFF0C; <code>home</code> &#x5C31;&#x662F;&#x6211;&#x5011;&#x7684;&#x9996;&#x9801;&#xFF0C;&#x6211;&#x5011;&#x9084;&#x7F3A;&#x4E00;&#x500B; detail &#x8DDF; add<br>
&#x5148; cd &#x9032;&#x5165; TODOApp &#x8CC7;&#x6599;&#x593E;&#x5F8C;&#xFF0C;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x5728;&#x7D42;&#x7AEF;&#x6A5F;&#x8F38;&#x5165;</p>
<pre><code>ionic generate page detail
</code></pre>
<p>generate &#x53EF;&#x4EE5;&#x6E1B;&#x5BEB;&#x6210; g&#xFF0C;&#x81EA;&#x52D5;&#x7522;&#x751F; html&#x3001;ts&#x3001;scss &#x4E09;&#x500B;&#x6A94;&#x6848;</p>
<p>&#x4E5F;&#x53EF;&#x4EE5;&#x624B;&#x52D5;&#x8F38;&#x5165;</p>
<pre><code>mkdir app/pages/detail
touch app/pages/detail/detail.ts
touch app/pages/detail/detail.html
touch app/pages/detail/detail.scss
</code></pre>
<p>&#x5DEE;&#x5225;&#x5728;&#x65BC; ionic &#x6307;&#x4EE4;&#x6703;&#x7522;&#x751F;&#x5957;&#x597D;&#x6A21;&#x677F;&#x7684;&#x6587;&#x4EF6;&#xFF0C;&#x624B;&#x52D5;&#x5EFA;&#x7ACB;&#x5247;&#x662F;&#x7A7A;&#x767D;&#x7684;&#x3002;</p>
<p>&#x63A5;&#x8457;</p>
<pre><code>ionic generate page add
</code></pre>
<h2>&#x9996;&#x9801; home</h2>
<h3>html</h3>
<p>&#x9996;&#x5148;&#x4F86;&#x770B; <code>app/pages/todos/home.html</code>&#xFF0C;&#x9019;&#x662F;&#x9996;&#x9801;&#x7684;&#x6A21;&#x677F;</p>
<pre><code>&lt;ion-header&gt;
    &lt;ion-navbar&gt;
        &lt;ion-title&gt;Todo List&lt;/ion-title&gt;
        &lt;ion-buttons end&gt;
            &lt;button (click)=&quot;add()&quot; ion-button icon-only&gt;&lt;ion-icon name=&quot;add&quot;&gt;&lt;/ion-icon&gt;&lt;/button&gt;
        &lt;/ion-buttons&gt;
    &lt;/ion-navbar&gt;
&lt;/ion-header&gt;
 
&lt;ion-content&gt;
    &lt;ion-list&gt;
        &lt;ion-item-sliding *ngFor=&quot;let todo of todoList; let i = index;&quot;&gt;
            &lt;button ion-item (click)=&quot;detail(i)&quot;&gt;
                &lt;h2&gt;{{ todo.title }}&lt;/h2&gt;
            &lt;/button&gt;
            &lt;ion-item-options&gt;
                &lt;button class=&quot;red&quot; (click)=&quot;delete(i)&quot;&gt;
                    &lt;ion-icon name=&quot;trash&quot;&gt;&lt;/ion-icon&gt;
                    Delete
                &lt;/button&gt;
            &lt;/ion-item-options&gt;
        &lt;/ion-item-sliding&gt;
    &lt;/ion-list&gt;
&lt;/ion-content&gt;
</code></pre>
<p><code>add()</code> &#x662F;&#x4E4B;&#x5F8C;&#x7528;&#x4F86;&#x52A0;&#x5165;&#x65B0;&#x4E8B;&#x9805;&#x7684;&#x6309;&#x9215;&#x3002;<br>
<code>delete(i)</code> &#x662F;&#x4E4B;&#x5F8C;&#x7528;&#x4F86;&#x522A;&#x6389;&#x7684;&#x6309;&#x9215;&#x3002;<br>
<code>detail(i)</code> &#x9EDE;&#x9032;&#x53BB;&#x53EF;&#x4EE5;&#x770B;&#x7D30;&#x7BC0;&#x3002;</p>
<h3>ts</h3>
<p>&#x4E00;&#x500B;&#x756B;&#x9762;&#x662F;&#x4E00;&#x500B;&#x7D44;&#x4EF6;&#xFF0C;&#x6982;&#x5FF5;&#x5C31;&#x662F; Angular 2&#x3002;<br>
<code>app/pages/todos/home.ts</code></p>
<pre><code>import { Component } from &apos;@angular/core&apos;;
import { NavController } from &apos;ionic-angular&apos;;
import { AddPage } from &quot;../add/add&quot;;
import { DetailPage } from &quot;../detail/detail&quot;;

@Component({
  selector: &apos;page-home&apos;,
  templateUrl: &apos;home.html&apos;
})
export class HomePage {
 
    public todoList: Array&lt;any&gt; = [];
 
    constructor(private navCtrl: NavController) { }
 
    ionViewDidEnter() {
        this.todoList = JSON.parse(localStorage.getItem(&quot;todos&quot;));
        console.log(this.todoList);
    }
 
    delete(index: number) {
        this.todoList.splice(index, 1);
        localStorage.setItem(&quot;todos&quot;, JSON.stringify(this.todoList));
    }
 
    add() {
        this.navCtrl.push(AddPage);
    }

    detail(index: number){
        this.navCtrl.push(DetailPage, {
          id: index
        });
    }
 
}
</code></pre>
<p><code>AddPage</code> <code>DetailPage</code> &#x7B49;&#x7B49;&#x8655;&#x7406;&#x3002;</p>
<p>&#x6211;&#x5011;&#x5728;  <code>ionViewDidEnter()</code> &#x624D;&#x5C0E;&#x5165; localStorage &#x8CC7;&#x6599;&#x800C;&#x975E; <code>constructor()</code> &#x662F;&#x56E0;&#x70BA;&#x524D;&#x8005;&#x53EF;&#x4EE5;&#x8B93;&#x6211;&#x5011;&#x6BCF;&#x6B21;&#x9032;&#x5165;&#x756B;&#x9762;&#x90FD;&#x89F8;&#x767C;&#xFF0C;&#x800C;&#x5F8C;&#x8005;&#x53EA;&#x6709;&#x5728;&#x88AB;&#x5C0E;&#x5411;&#x9032;&#x4F86;&#x6642;&#x624D;&#x89F8;&#x767C; (&#x5982;&#x679C;&#x6309;&#x8FD4;&#x56DE;&#x5C31;&#x6C92;&#x4E8B;)&#x3002;<br>
&#x8CC7;&#x6599;&#x90E8;&#x5206;&#x7C21;&#x55AE;&#x7528; localStorage &#x4EE5; json &#x4F86;&#x505A;&#x5132;&#x5B58;&#x3002;&#x7576;&#x7136;&#x4F60;&#x4E5F;&#x53EF;&#x4EE5;&#x7528; DB &#x5916;&#x639B;&#x4F86;&#x8655;&#x7406;&#x3002;</p>
<p><code>this.navCtrl.push()</code> &#x53EF;&#x4EE5;&#x5C0E;&#x5411;&#x5176;&#x4ED6;&#x9801;&#x9762;&#x3002;&#x4F8B;&#x5982; <code>this.navCtrl.push(AddPage)</code>&#x3002;&#x4E5F;&#x53EF;&#x4EE5;&#x52A0;&#x4E0A;&#x53C3;&#x6578; <code>this.navCtrl.push(DetailPage, {id: index});</code>&#x3002;</p>
<h2>&#x589E;&#x52A0;&#x4E8B;&#x9805;&#x7684;&#x9801;&#x9762; add</h2>
<h3>html</h3>
<pre><code>&lt;ion-header&gt;
    &lt;ion-navbar&gt;
        &lt;ion-title&gt;Add Item&lt;/ion-title&gt;
        &lt;ion-buttons end&gt;
            &lt;button (click)=&quot;save()&quot; ion-button icon-only&gt;&lt;ion-icon name=&quot;checkmark&quot;&gt;&lt;/ion-icon&gt;&lt;/button&gt;
        &lt;/ion-buttons&gt;
    &lt;/ion-navbar&gt;
&lt;/ion-header&gt;
 
&lt;ion-content&gt;
    &lt;ion-list&gt;
        &lt;ion-item&gt;
            &lt;ion-label floating&gt;Title&lt;/ion-label&gt;
            &lt;ion-input type=&quot;text&quot; [(ngModel)]=&quot;todoTitle&quot;&gt;&lt;/ion-input&gt;
        &lt;/ion-item&gt;
        &lt;ion-item&gt;
            &lt;ion-label floating&gt;Description&lt;/ion-label&gt;
            &lt;ion-input type=&quot;text&quot; [(ngModel)]=&quot;todoDes&quot;&gt;&lt;/ion-input&gt;
        &lt;/ion-item&gt;
    &lt;/ion-list&gt;
&lt;/ion-content&gt;
</code></pre>
<p><code>floating</code> &#x6A19;&#x7C64;&#x53EF;&#x4EE5;&#x8B93;&#x6587;&#x5B57;&#x98C4;&#x4E0A;&#x53BB;&#x3002;</p>
<h3>ts</h3>
<pre><code>import { Component } from &apos;@angular/core&apos;;
import { NavController} from &apos;ionic-angular&apos;;

@Component({
  templateUrl: &apos;add.html&apos;
})
export class AddPage {
 
    public todoList: Array&lt;any&gt;;
    public todoTitle: string;
    public todoDes: string;
 
    constructor(private navCtrl: NavController) {
        this.todoList = JSON.parse(localStorage.getItem(&quot;todos&quot;));
        if(!this.todoList) {
            this.todoList = [];
        }
        this.todoTitle = &quot;&quot;;
        this.todoDes = &quot;&quot;; // description
    }
 
    save() {
        if(this.todoTitle != &quot;&quot; &amp;&amp; this.todoDes != &quot;&quot;) {
            this.todoList.push(
              {
                title: this.todoTitle,
                des: this.todoDes
              } 
            );
            localStorage.setItem(&quot;todos&quot;, JSON.stringify(this.todoList));
            this.navCtrl.pop();
        } else if(this.todoTitle == &quot;&quot;) {
            alert(&quot;No Title!&quot;); 
        } else if(this.todoDes == &quot;&quot;){
            alert(&quot;No Description!&quot;);
        }
    }
 
}
</code></pre>
<p><code>todoTitle</code> <code>todoDes</code> &#x548C;&#x6A21;&#x677F;&#x96D9;&#x5411;&#x7D81;&#x5B9A;&#xFF0C;&#x6309;&#x4E0B; <code>save()</code> &#x6703;&#x5132;&#x5B58;&#x9032; <code>todos</code></p>
<h2>&#x67E5;&#x770B;&#x7D30;&#x7BC0;&#x9801;&#x9762; detail</h2>
<h3>html</h3>
<pre><code>&lt;ion-header&gt;
    &lt;ion-navbar&gt;
        &lt;ion-title&gt;Detail&lt;/ion-title&gt;
    &lt;/ion-navbar&gt;
    &lt;ion-buttons end&gt;
        &lt;button (click)=&quot;close()&quot; ion-button icon-only&gt;&lt;ion-icon name=&quot;checkmark&quot;&gt;&lt;/ion-icon&gt;&lt;/button&gt;
    &lt;/ion-buttons&gt;
&lt;/ion-header&gt;

&lt;ion-content padding&gt;
    &lt;ion-card&gt;
        &lt;ion-card-header&gt;
            {{ title }}
        &lt;/ion-card-header&gt;
        &lt;ion-card-content&gt;
            {{ description }}
        &lt;/ion-card-content&gt;
    &lt;/ion-card&gt;
&lt;/ion-content&gt;
&lt;ion-header&gt;
    &lt;ion-navbar&gt;
        &lt;ion-title&gt;Detail&lt;/ion-title&gt;
        &lt;ion-buttons end&gt;
            &lt;button (click)=&quot;close()&quot;&gt;&lt;ion-icon name=&quot;close&quot;&gt;&lt;/ion-icon&gt;&lt;/button&gt;
        &lt;/ion-buttons&gt;
    &lt;/ion-navbar&gt;
&lt;/ion-header&gt;

&lt;ion-content padding&gt;
    &lt;ion-card&gt;
        &lt;ion-card-header&gt;
            {{ title }}
        &lt;/ion-card-header&gt;
        &lt;ion-card-content&gt;
            {{ description }}
        &lt;/ion-card-content&gt;
    &lt;/ion-card&gt;
&lt;/ion-content&gt;
</code></pre>
<h3>ts</h3>
<pre><code>import { Component } from &apos;@angular/core&apos;;
import { NavController, NavParams } from &apos;ionic-angular&apos;;

@Component({
  selector: &apos;page-detail&apos;,
  templateUrl: &apos;detail.html&apos;
})
export class DetailPage {

  public title: string;
  public description: string;

  constructor(public navCtrl: NavController, public navParams: NavParams) {
    let id: number = navParams.get(&apos;id&apos;);
    let todoList: any = JSON.parse(localStorage.getItem(&quot;todos&quot;));
    this.title = todoList[id].title;
    this.description = todoList[id].des;
    console.log(this.title);
  }

  ionViewDidLoad() {
    //console.log(&apos;ionViewDidLoad DetailPage&apos;);
  }

  close(){
    this.navCtrl.pop();
  }

}
</code></pre>
<p>&#x9084;&#x8A18;&#x5F97;&#x525B;&#x525B;&#x5728; <code>home.ts</code> &#x7684; <code>detail(i)</code>&#xFF0C;&#x6211;&#x5011;&#x518D;&#x5C0E;&#x5165;&#x9032;&#x4F86; <code>detail</code> &#x6642;&#x5019;&#x6709;&#x8F38;&#x5165;&#x53C3;&#x6578;&#x55CE;&#xFF1F;<br>
&#x9019;&#x6642;&#x5019;&#x6211;&#x5011;&#x8981; <code>import { NavParams } from &apos;ionic-angular&apos;;</code> &#x4F7F;&#x7528; <code>NavParams</code>&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x53D6;&#x5F97;&#x53C3;&#x6578; <code>let id: number = navParams.get(&apos;id&apos;);</code>&#x3002;</p>
<h2>SCSS</h2>
<p>&#x63A5;&#x8457;&#x6211;&#x5011;&#x7A0D;&#x5FAE;&#x4FEE;&#x98FE;&#x4E00;&#x4E0B;&#x6211;&#x5011;&#x7684;&#x5916;&#x89C0;<br>
&#x6253;&#x958B; <code>src/theme/variables.scss</code><br>
&#x9019;&#x908A;&#x7684; scss &#x6703;&#x662F;&#x5168;&#x57DF;&#x8B8A;&#x6578;&#x3002;</p>
<pre><code>$toolbar-ios-title-font-size: 2.3rem;
$toolbar-ios-height: 30px;
$font-family-base: Microsoft JhengHei, -apple-system, &quot;Helvetica Neue&quot;, &quot;Roboto&quot;, sans-serif !default;
</code></pre>
<p>&#x9810;&#x8A2D;&#x6A19;&#x984C;&#x771F;&#x7684;&#x5F88;&#x5C0F;&#xFF0C;&#x628A;&#x6A19;&#x984C;&#x8B8A;&#x5927;&#x4E00;&#x9EDE;&#x3002;</p>
<p>&#x6253;&#x958B; <code>src/pages/home/home.scss</code></p>
<pre><code>.danger{
    background-color: #f53d3d;
    color: white;
}
</code></pre>
<p>&#x6211;&#x5011;&#x8B93;&#x522A;&#x9664;&#x7684;&#x6309;&#x9215;&#x8B8A;&#x6210;&#x7D05;&#x8272;&#x7684;&#x3002;</p>
<h4>&#x5927;&#x529F;&#x544A;&#x6210;&#x56C9;&#xFF01;</h4>
<p>&#x4E0B;&#x56DE;&#x4ECB;&#x7D39;&#x5982;&#x4F55;&#x8F38;&#x51FA;&#xFF0C;&#x5BE6;&#x969B;&#x653E;&#x5230;&#x624B;&#x6A5F;&#x4E0A;&#xFF01;</p>
 <br>
                                                    </div>
                    </div>
                
