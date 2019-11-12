---
title: Angular 5 是啥玩意？
date: 2017-10-24 00:00:00
tags: [Chinese Posts,English Posts,Angular,Angular 5,Front End Development,Chinese,]
---


## Angular 5 是啥玩意？

<img class="dz t u ge ak" src="https://miro.medium.com/max/1204/1*1BsxHl8xsRjb8sT3ooTFSw.jpeg" role="presentation"><br/>

Angular 5即將在近期發布，讓我們來看看有啥特別的呢?

沒用過 Angular 也聽過 Angular，沒聽過 Angular 總之你現在看過了 XD<br>Angular 5即將發布，本文將介紹什麼是 Angular 以及新版本有啥有趣的東西。本文為了友善初學者，會從最基礎的東西講起，如果想直接看版本 5 的新功能可以直接跳到後面。

## 簡介

首先簡單描述一下什麼是 Angular，改編自官網：

<span style="font-size: 26px; color: #696969; font-style:italic">Angular是一個前端開發平台。它能幫你更輕鬆的構建 Web應用程式。 Angular 集聲明式模板（declarative templates）、依賴注入（dependency injection）、端到端工具和一些最佳實踐方式於一身，為您解決開發層面的各種挑戰。 替開發者提升構建 Web、手機或桌面應用程式的能力。</span>

Angular是一個前端開發平台。它能幫你更輕鬆的構建 Web應用程式。 Angular 集聲明式模板（declarative templates）、依賴注入（dependency injection）、端到端工具和一些最佳實踐方式於一身，為您解決開發層面的各種挑戰。 替開發者提升構建 Web、手機或桌面應用程式的能力。

Angular 是 Google開發出來一款開源 JavaScript框架，用來開發單一頁面應用程式（single page application, SPA）。Angular 共有 1、2、4、5 這麼多版本，1正名為 AngularJS ，而 2、4、5 版為 Angular。兩者架構差異很大，簡單來說 AngularJS 本身有些缺點，後來受到 React 的刺激後，Angular 便被開發出來與之抗衡。

Angular 採用 MVC 模式，涵蓋了M、V、C/VM 等層面，不需要組合、評估其它技術就能完成大部分前端開發任務。這是因為她已經將各種技術封裝在框架中，隔離了瀏覽器的細節，讓你不用關心她的實現細節。此外所有需要使用的套件、模組 Angular 都已經幫你打包好了，不像是 React 或 Vue 要自己去架構模組。

## 特色

### 採用 Typescript

簡單來說 Typescript 可以說是 Super版的 JavaScript，採用強型別並增加對物件導向的支援。更詳細可以參考<a href="https://ithelp.ithome.com.tw/articles/10186280" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">這篇</a>。

### 注入依賴

Angular 中的 <strong class="gw jh"><em class="ji">Service</em></strong> 物件帶有依賴注入的概念。依賴注入的觀念就是將所有東西先在「外面」準備好，然後再帶入「內部」的程式中，同時只會生成單一實體。如此一來你就能夠在檢視程式碼的時候，一目了然地知道「內部被注入」的這個物件「依賴著外部」的哪些物件。更詳細可以參考<a href="https://ithelp.ithome.com.tw/articles/10186702" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">這篇</a>。

### 模組、組件與模板

Angular 中將一個網站應用程式拆程一個一個的組件（<strong class="gw jh"><em class="ji">Component</em></strong>），而每個組件又可以是更小的組件所構成，而這種方式在現代前端開發框架中已經非常常見，在 React 與 Vue 中也可以看到差不多的概念。好處是一個功能為一個組件，彼此獨立，在修改、抽換上都比較方便，日後維護和拓展也方便。

更詳細一點的話 Angular 中除了Component 還有 Service、Directive、Pipe Router等等物件，概念都和組件很像，但受限於篇幅，這邊不介紹，大家可以去 <a href="https://angular.cn/guide/architecture" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Angular Doc</a> 上面看或參考<a href="https://ithelp.ithome.com.tw/articles/10186561" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">這篇</a>。

而每個組件由三塊所構成，分別為 <strong class="gw jh"><em class="ji">component.html</em></strong>、<strong class="gw jh"><em class="ji">component.css</em></strong>、<strong class="gw jh"><em class="ji">component.ts</em></strong>，由 ts 來做邏輯處理，並串連 HTML 模板和 CSS。模板藉由和 ts 數據綁定以及套上 <strong class="gw jh"><em class="ji">Directive</em></strong> 和 <strong class="gw jh"><em class="ji">Pipe</em></strong> 使的網頁呈現和邏輯更加強大。關於模板可以參考<a href="https://ithelp.ithome.com.tw/articles/10186854" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">這篇</a>。

而所有組件整合在一起可以變成一個模組（<strong class="gw jh"><em class="ji">module</em></strong>），一個 Angular 開發的應用程式可以同時使用好幾個模組。總之，整個架構就像曡積木一樣，積木又可以是更小的積木，最後蓋出成品。

### 開發層面

<ul>
<li id="a106" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl">Angular 自帶整合開發環境 <a href="https://github.com/angular/angular-cli" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Angular CLI</a> 開發更加方便，webpack 什麼都都幫你弄好了。</li><li id="a7dd" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl">完整官方套件<br>@angular/core<br>@angular/common<br>@angular/forms<br>@angular/http<br>@angular/router<br>@angular/material<br>@angular/platform-server<br>@angular/service-worker<br>@angular/language-service<br>……. 等等等</li><li id="f5fb" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl">支援 Progressive Web Apps</li><li id="7d88" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl">結合 <a href="https://ionicframework.com/" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Ionic</a> 可以輕鬆開發 mobile APP</li><li id="352d" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl"><a href="https://universal.angular.io/" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Angular Universal</a> 可以開發後端渲染的 Angular</li>
</ul>

關於 Angular 更多詳細細節可以參考 <a href="https://ithelp.ithome.com.tw/articles/10189032" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Angular 2 給初學者的學習指南</a> 雖然是針對 2 寫的，但內容都是最基礎的，而最基本的概念 2、4、5 都一樣，概念懂了之後再去研究不同版本的更細節差異。

---

## Angular 5 強勢來襲

說了這麼多，所以 5 到底有哪些新功能呢？

### 更好的行動裝置體驗

@angular/service-worker 套件讓 Angular 更好的實踐 <a href="https://developers.google.com/web/progressive-web-apps/" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Progressive Web Apps</a>

### Angular CLI

AOT 編譯現在是預設的編譯方式，意味著 AOT 有更好的提昇。但編譯時間還是比較長。建議是在開發時用 JIT，發布時再使用 AOT。

### 效能更好 ＆ 體積更小

初始化和編譯速度都有提昇，更好的優化讓 <code class="gj kf kg kh ki b">bundle</code>的大小也變小了，<code class="gj kf kg kh ki b">event listener</code> 的速度提高三倍。

### Multiple exportAs

Directive 可以定義多個名字作為變數在模板中使用

<pre><span id="34a0" class="ir hj em at ki b fd kl km r kn">@Directive({<br>  selector: &apos;child-dir&apos;,<br>  exportAs: &apos;child1, child2&apos;<br>})<br>class ChildDir {}<br> <br>@Component({<br>  selector: &apos;main&apos;,<br>  template: `<br>  &lt;child-dir #c1=&quot;child1&quot; #c2=&quot;child2&quot;&gt;<br>    &lt;!-- c1=== c2--&gt;<br>  &lt;/child-dir&gt;`<br>})<br>class MainComponent {}</span></pre>

### Bootstrap with Custom Zone

自由選擇要用的 <code class="gj kf kg kh ki b">Zone</code>

<pre><span id="28ae" class="ir hj em at ki b fd kl km r kn">platformBrowserDynamic()<br>    .bootstrapModule(AppModule, {<br>        ngZone: &apos;zone.js&apos; // or &apos;noop&apos; or Custom NgZone<br>})</span></pre>

<a href="https://stackblitz.com/edit/angular-m1bktf?file=main.ts" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">這邊</a>可以看實際效果

### Animations

<ul>
<li id="677a" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl"><strong class="gw jh">:increment / :decrement</strong></li>
</ul>

<pre><span id="6a69" class="ir hj em at ki b fd kl km r kn">@Component({<br>    animations: [<br>        trigger(&quot;counter&quot;, [ <br>            transition(&apos;:increment&apos;, [ /*...*/ ]),<br>            transition(&apos;:decrement&apos;, [ /*...*/ ]),<br>        ])<br>    ],<br>    template: `<br>    &lt;span [@counter]=&quot;count&quot;&gt;<br>    `<br>})<br>class AppComponent() { <br>    count = 1;<br>}</span></pre>

<ul>
<li id="30fa" class="gu gv em at gw b gx gy gz ha hb hc hd he hf hg hh jj jk jl"><strong class="gw jh">Disable animations</strong></li>
</ul>

<pre><span id="e2b7" class="ir hj em at ki b fd kl km r kn">@Component({<br>    animations: [<br>        trigger(&quot;anim&quot;, [ /* ... */])<br>    ],<br>    template: `<br>    &lt;div [@anim]=&quot;prop&quot; [@anim.disabled]=&quot;animationDisabled&quot;&gt;<br>    `<br>})<br>class AppComponent() { <br>    prop = &apos;&apos;;<br>    animationDisabled = false;<br>}</span></pre>

<ul>
<li id="3376" class="gu gv em at gw b gx gy gz ha hb hc hd he hf hg hh jj jk jl"><strong class="gw jh">Negative Query Limit</strong></li>
</ul>

<pre><span id="3814" class="ir hj em at ki b fd kl km r kn">trigger(&quot;anim&quot;, [<br>    transition(&quot;:enter&quot;, [<br>        query(<br>            &quot;.item&quot;, <br>            [ /** ... **/ ],<br>            { limit: -5 }<br>        )<br>    ])<br>])</span></pre>

## Router

<ul>
<li id="d5cc" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl"><strong class="gw jh">ChildActivationStart / ChildActivationEnd</strong></li>
</ul>

<pre><span id="9b08" class="ir hj em at ki b fd kl km r kn">router.events<br>    .filter(e =&gt; e instanceof RouteEvent)<br>    .subscribe(e =&gt; {<br>        if (e instanceof ChildActivationStart) {<br>            spinner.start();<br>        } else if (e instanceof ChildActivationEnd) {<br>            spinner.end()<br>        }<br>    });</span><span id="8250" class="ir hj em at ki b fd ko kp kq kr ks km r kn">// Event = RouteEvent | RouterEvent<!-- --> </span></pre>

<ul>
<li id="15ca" class="gu gv em at gw b gx gy gz ha hb hc hd he hf hg hh jj jk jl"><strong class="gw jh">ActivationStart / ActivationEnd</strong></li>
</ul>

<pre><span id="9ab8" class="ir hj em at ki b fd kl km r kn">router.events<br>    .filter(e =&gt; e instanceof RouteEvent)<br>    .subscribe(e =&gt; {<br>        if (e instanceof ActivationStart) {<br>            spinner.start();<br>        } else if (e instanceof ActivationEnd) {<br>            spinner.end()<br>        }<br>    });</span><span id="f48f" class="ir hj em at ki b fd ko kp kq kr ks km r kn">// Event = RouteEvent | RouterEvent</span></pre>

### Forms

<ul>
<li id="c69f" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl"><strong class="gw jh">updateOn<br></strong>change, blur, submit</li>
</ul>

<pre><span id="8615" class="ir hj em at ki b fd kl km r kn">&lt;form [ngFormOptions]=&quot;{updateOn: &apos;change&apos;}&quot;&gt;<br>    &lt;input name=&quot;foo&quot; <br>        [(ngModel)]=&quot;foo&quot;<br>        [ngModelOptions]=&quot;{updateOn: &apos;blur&apos;}&quot;&gt;<br>    &lt;input name=&quot;bar&quot; <br>        [(ngModel)]=&quot;bar&quot;<br>        [ngModelOptions]=&quot;{updateOn: &apos;submit&apos;}&quot;&gt;<br>&lt;/form&gt;</span></pre>

### http

<ul>
<li id="716c" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl"><strong class="gw jh"><em class="ji">HttpClient </em></strong>可以直接設定 <strong class="gw jh"><em class="ji">headers </em></strong>&amp; <strong class="gw jh"><em class="ji">params</em></strong></li><li id="755f" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl"><strong class="gw jh"><em class="ji">Http</em></strong> ( @angular/http) 被淘汰，改用 <strong class="gw jh"><em class="ji">HttpClient </em></strong>(@angular/common/http)</li>
</ul>

<pre><span id="da55" class="ir hj em at ki b fd kl km r kn">httpClient.get(&quot;/api&quot;, {<br>    headers: {<br>        &quot;X-MY-HEADER&quot;: &quot;header&quot;<br>    },<br>    params: {<br>        &quot;foo&quot;:  &quot;bar&quot;<br>    },<br>})</span></pre>

### Platform Server

<ul>
<li id="068e" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl">TransferState / BrowserTransferStateModule<br>可以參考這篇 <a href="https://blog.angularindepth.com/using-transferstate-api-in-an-angular-5-universal-app-130f3ada9e5b" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">Using TransferState API in an Angular v5 Universal App</a> 和ˊ這篇 <a class="dj by jd je jf jg" target="_blank" rel="noopener" href="/@evertonrobertoauler/angular-5-universal-with-transfer-state-using-angular-cli-19fe1e1d352c">Angular 5 universal with Transfer State using @angular/cli</a></li><li id="6a01" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl">Render Hooks: BEFORE_APP_SERIALIZED</li>
</ul>

<pre><span id="4607" class="ir hj em at ki b fd kl km r kn"><a href="http://twitter.com/NgModule" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow">@NgModule</a>({<br>  bootstrap: [MyServerApp],<br>  declarations: [MyServerApp],<br>  imports: [<br>    BrowserModule.withServerTransition({appId: &apos;render-hook&apos;}), <br>    ServerModule<br>  ],<br>  providers: [<br>    {<br>       provide: BEFORE_APP_SERIALIZED, <br>       useFactory: getTitleRenderHook, <br>      multi: true, deps: [DOCUMENT]},<br>  ]<br>})<br>class RenderHookModule {}</span></pre>

### 重大改變

<ul>
<li id="b25c" class="gu gv em at gw b gx hv gz hw hb hx hd hy hf hz hh jj jk jl"><strong class="gw jh">需要 TypeScript 2.4.x</strong></li><li id="936c" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl">Common Pipes 使用 <strong class="gw jh">Intl API</strong></li><li id="dfc0" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl">使用 <a href="http://cldr.unicode.org/" class="dj by jd je jf jg" target="_blank" rel="noopener nofollow"><strong class="gw jh">Common Locale Data Repository</strong></a><strong class="gw jh"> (CLDR)<br></strong>定義地區時間 <strong class="gw jh">@angular/common/locales<br></strong><code class="gj kf kg kh ki b">en_US</code> 被設為預設，如果需要可以自行引入</li>
</ul>

<pre><span id="9e3e" class="ir hj em at ki b fd kl km r kn">import { registerLocaleData } from &apos;@angular/common&apos;;<br>import localeZh from &apos;@angular/common/locales/zh&apos;;</span><span id="df90" class="ir hj em at ki b fd ko kp kq kr ks km r kn">registerLocaleData(localeZh);</span></pre>

<ul>
<li id="1fa2" class="gu gv em at gw b gx gy gz ha hb hc hd he hf hg hh jj jk jl">淘汰 <code class="gj kf kg kh ki b">ngFor</code> 改用 <code class="gj kf kg kh ki b">ngForOf</code> ，但都還是用 <code class="gj kf kg kh ki b">*ngFor</code> 語法糖</li><li id="e489" class="gu gv em at gw b gx jm gz jn hb jo hd jp hf jq hh jj jk jl"><code class="gj kf kg kh ki b">Router</code> 淘汰 <code class="gj kf kg kh ki b">initialNavigation</code> ，直接使用 <code class="gj kf kg kh ki b">&apos;enable’|&apos;disable&apos;</code></li>
</ul>