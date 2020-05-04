---
title: Angular 2 多語言 ( 2 )
date: 2016-12-28 23:46:13
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x524D;&#x4E00;&#x7BC7;&#x5DF2;&#x7D93;&#x8AAA;&#x904E;&#x70BA;&#x751A;&#x9EBC;&#x591A;&#x8A9E;&#x8A00;&#x7684;&#x7DB2;&#x7AD9;&#x5F88;&#x91CD;&#x8981;&#xFF0C;&#x4E5F;&#x793A;&#x7BC4;&#x4E86;&#x5982;&#x4F55;&#x9054;&#x5230;&#x591A;&#x8A9E;&#x8A00;&#x7684;&#x6548;&#x679C;&#x3002;&#x4F46;&#x662F;&#xFF0C;&#x6211;&#x5011;&#x5C0D;&#x65BC;&#x8A9E;&#x8A00;&#x7FFB;&#x8B6F;&#x7684;&#x9700;&#x6C42;&#x9084;&#x6709;&#x5F88;&#x591A;&#xFF0C;&#x4F8B;&#x5982;&#x6211;&#x5982;&#x679C;&#x60F3;&#x8981;&#x8B93;&#x4E00;&#x4E32;&#x53E5;&#x5B50;&#x6BCF;&#x6B21;&#x642D;&#x914D;&#x4E0D;&#x540C;&#x7684;&#x8B8A;&#x6578;&#x600E;&#x9EBC;&#x8FA6;&#xFF0C;&#x50CF;&#x662F;&#x300C;&#x4F60;&#x597D;&#xFF0C;Tiger Liu&#x300D;&#x6216;&#x662F;&#x300C;&#x4F60;&#x597D;&#xFF0C;Tiger&#x300D;&#x9019;&#x6A23;&#x7684;&#x53EF;&#x8B8A;&#x6027;&#x3002;&#x6216;&#x662F;&#x5982;&#x679C;&#x6709;&#x4E9B;&#x8A9E;&#x8A5E;&#x5728;&#x67D0;&#x4E9B;&#x8A9E;&#x8A00;&#x4E2D;&#x7FFB;&#x8B6F;&#x4E0D;&#x51FA;&#x4F86;&#x3001;&#x4E0D;&#x60F3;&#x7FFB;&#x8B6F;&#x6216;&#x662F;&#x4E0D;&#x5C0F;&#x5FC3;&#x5FD8;&#x8A18;&#x589E;&#x52A0;&#x5B57;&#x5178;&#x6642;&#xFF0C;&#x4F8B;&#x5982;&#x300C;&#x63B0;&#x63B0;&#x56C9;&#xFF01;&#x300D;&#x5728;&#x82F1;&#x6587;&#x7FFB;&#x6210;&#x300C;Bye Bye!&#x300D;&#x53EF;&#x662F;&#x5728;&#x65E5;&#x6587;&#x7684;&#x5B57;&#x5178;&#x6A94;&#x5FD8;&#x8A18;&#x52A0;&#x4E0A;&#x9019;&#x500B;&#x5B57;&#xFF0C;&#x8981;&#x8B93;&#x7DB2;&#x7AD9;&#x9084;&#x662F;&#x80FD;&#x5920;&#x986F;&#x793A;&#x300C;Bye Bye!&#x300D;&#x600E;&#x9EBC;&#x505A;&#xFF1F;</p>
<h2>&#x76EE;&#x6A19;</h2>
<ul>
<li>&#x8B93;&#x6211;&#x5011;&#x7684;&#x7FFB;&#x8B6F;&#x53EF;&#x4EE5;&#x6709;&#x5360;&#x4F4D;&#x7B26;&#x865F; ( placeholder)&#xFF0C;&#x5982;&#x6B64;&#x4EE5;&#x4F86;&#x53EF;&#x4EE5;&#x8B93;&#x53E5;&#x5B50;&#x7684;&#x53EF;&#x8B8A;&#x6027;&#x8B8A;&#x5927;&#xFF0C;&#x5982;&#x524D;&#x8A00;&#x6240;&#x8FF0;&#x4E00;&#x822C;&#x3002;</li>
<li>&#x7576;&#x5728;&#x8A9E;&#x8A00;&#x5305;&#x627E;&#x4E0D;&#x5230;&#x7B26;&#x5408;&#x7684;&#x5B57;&#x53E5;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x81EA;&#x52D5;&#x7528;&#x5099;&#x7528;&#x7684;&#x8A9E;&#x8A00;&#x7576;&#x66FF;&#x88DC;&#x3002;</li>
</ul>
<p>&#x6211;&#x5011;&#x5C07;&#x7E7C;&#x7E8C;&#x7528;&#x4E0A;&#x4E00;&#x7BC7;&#x7684;&#x7A0B;&#x5F0F;&#x4F86;&#x4FEE;&#x6539;<br>
&#x5B8C;&#x6210;&#x7684; <a href="https://plnkr.co/edit/OQa8JWwkeP1t7BazQ770?p=preview" target="_blank">Plunker</a></p>
<h2>&#x958B;&#x5DE5;</h2>
<h3>&#x8A9E;&#x8A00;&#x5305;</h3>
<p>&#x5148;&#x4F86;&#x770B;&#x770B;&#x6211;&#x5011;&#x7684;&#x8A9E;&#x8A00;&#x5305;&#x6700;&#x5F8C;&#x9577;&#x600E;&#x6A23;</p>
<pre><code>// lang-en.ts

export const LANG_EN_NAME = &apos;en&apos;;

export const LANG_EN_TRANS = {
    &apos;hello world&apos;: &apos;hello world&apos;,
    &apos;hello greet&apos;: &apos;Hello, %0 %1!&apos;, // two placeholder
    &apos;well done&apos;: &apos;Well done %0&apos;, // one placeholder
    &apos;good bye&apos;: &apos;bye bye&apos;, // &#x53EA;&#x6709;&#x5728;&#x82F1;&#x6587;&#x4E2D;&#x5B9A;&#x7FA9;
}

// lang-zh.ts

export const LANG_ZH_NAME = &apos;zh&apos;;

export const LANG_ZH_TRANS = {
    &apos;hello world&apos;: &apos;&#x4F60;&#x597D;&#xFF0C;&#x4E16;&#x754C;&apos;,
    &apos;hello greet&apos;: &apos;&#x4F60;&#x597D;, %0 %1!&apos;,
    &apos;well done&apos;: &apos;&#x5E79;&#x5F97;&#x597D;, %0&apos;,
};
</code></pre>
<h3>&#x66F4;&#x65B0; translate &#x670D;&#x52D9;</h3>
<pre><code>// app/translate/translate.service.ts
...

public instant(key: string, words?: string | string[]) { // &#x589E;&#x52A0;&#x53EF;&#x80FD;&#x7684;&#x8B8A;&#x6578;
    const translation: string = this.translate(key);

    if (!words) return translation;
    return this.replace(translation, words); // &#x547C;&#x53EB; replace 
}

...
</code></pre>
<p>&#x63A5;&#x8457;&#x4F86;&#x5B9A;&#x7FA9;<code>replace</code></p>
<pre><code>// app/translate/translate.service.ts
...

private PLACEHOLDER = &apos;%&apos;; // &#x6211;&#x5011;&#x7684;&#x4F54;&#x4F4D;&#x7B26;

public replace(word: string = &apos;&apos;, words: string | string[] = &apos;&apos;) {
    let translation: string = word;

    const values: string[] = [].concat(words);// &#x5C0E;&#x5165;&#x8F38;&#x5165;&#x7684;&#x53C3;&#x6578;&#x5B57;&#x4E32;
    values.forEach((e, i) =&gt; {
        //&#x6703;&#x7528; e &#x66FF;&#x63DB;&#x6389; %i: %0, %1, ...
        translation = translation.replace(this.PLACEHOLDER.concat(&lt;any&gt;i), e);
    });

    return translation;
}

...
</code></pre>
<h3>&#x66F4;&#x65B0; Pipe</h3>
<pre><code>// app/translate/translate.pipe.ts
...

transform(value: string, args: string | string[]): any { // args &#x53EF;&#x4EE5;&#x662F;&#x55AE;&#x4E00;&#x5B57;&#x4E32;&#x6216;&#x662F;&#x5B57;&#x4E32;&#x5217;
    if (!value) return;
    return this._translate.instant(value, args); // &#x52A0;&#x5165; args
}
...
</code></pre>
<h3>&#x66F4;&#x65B0;&#x6A21;&#x677F;</h3>
<pre><code>&lt;!--app/app.component.html--&gt;

&lt;!-- &#x591A;&#x503C;&#x901A;&#x9053; --&gt;
&lt;p&gt;
    Translate &lt;strong class=&quot;text-muted&quot;&gt;Hello, %0 %1!&lt;/strong&gt;:
&lt;br&gt;
    &lt;strong&gt;{{ &apos;hello greet&apos; | translate:[&apos;Jane&apos;, &apos;Doe&apos;] }}&lt;/strong&gt;
&lt;/p&gt;

&lt;!-- &#x55AE;&#x4E00;&#x503C;&#x901A;&#x9053; --&gt;
&lt;p&gt;
    Translate &lt;strong class=&quot;text-muted&quot;&gt;Well done %0&lt;/strong&gt;: 
    &lt;br&gt;
    &lt;strong&gt;{{ &apos;well done&apos; | translate:&apos;John&apos; }}&lt;/strong&gt;
&lt;/p&gt;
</code></pre>
<h3>&#x5EFA;&#x7ACB;&#x4E8B;&#x4EF6;</h3>
<pre><code>// app/translate/translate.service.ts
...

import { Injectable, Inject, EventEmitter } from &apos;@angular/core&apos;; // &#x5F15;&#x5165; event emitter

...

// &#x589E;&#x52A0;&#x4E8B;&#x4EF6;
public onLangChanged: EventEmitter&lt;string&gt; = new EventEmitter&lt;string&gt;();
..

// &#x9078;&#x53D6;&#x7528;&#x751A;&#x9EBC;&#x8A9E;&#x8A00;
public use(lang: string): void {
    ...
    this.onLangChanged.emit(lang); // &#x767C;&#x5E03;&#x8B8A;&#x5316;
}

...
</code></pre>
<h3>&#x4E3B;&#x7A0B;&#x5F0F;</h3>
<p>&#x5148;&#x79FB;&#x9664; <code>selectLang()</code> &#x4E2D;&#x7684; <code>refreshText()</code>&#xFF0C;&#x6211;&#x5011;&#x8981;&#x91CD;&#x65B0;&#x67B6;&#x69CB;&#x3002;</p>
<pre><code>// app/app.component.ts
...

ngOnInit() {
    // &#x8F09;&#x5165;&#x4E00;&#x4E9B;&#x6771;&#x897F;
    ...

    this.subscribeToLangChanged(); // subscribe to language changes

    // &#x8A2D;&#x5B9A;&#x76EE;&#x524D;&#x8A9E;&#x8A00;
    this.selectLang(&apos;zh&apos;);

}

selectLang(lang: string) {
    // &#x8A2D;&#x70BA;&#x9810;&#x8A2D;
    this._translate.use(lang);
    // this.refreshText(); // &#x522A;&#x6389;&#x9019;&#x884C;
}

subscribeToLangChanged() {
    // &#x5237;&#x65B0;&#x6587;&#x5B57;
    return this._translate.onLangChanged.subscribe(x =&gt; this.refreshText());
}

...
</code></pre>
<p>&#x9019;&#x6A23;&#x8A2D;&#x5B9A;&#x4E4B;&#x5F8C;&#xFF0C;&#x53EA;&#x8981;&#x8A9E;&#x8A00;&#x6539;&#x8B8A;&#xFF0C;&#x5C31;&#x6703;&#x81EA;&#x52D5;&#x66F4;&#x65B0;</p>
<h3>&#x9810;&#x8A2D; &amp; &#x5099;&#x7528;&#x8A9E;&#x8A00;</h3>
<p>&#x5099;&#x7528;&#x8A9E;&#x8A00;&#x7684;&#x6982;&#x5FF5;&#x662F;&#xFF0C;&#x5047;&#x8A2D;&#x9810;&#x8A2D;&#x662F;&#x82F1;&#x6587;&#xFF0C;&#x7576;&#x65E5;&#x6587;&#x6C92;&#x6709;&#x5B57;&#x4E32;&#x6642;&#xFF0C;&#x5C31;&#x56DE;&#x53BB;&#x7528;&#x9810;&#x8A2D;&#x7684;&#x82F1;&#x6587;&#x5B57;&#x4E32;&#x3002;</p>
<pre><code>// app/translate/translate.service.ts
...

// &#x589E;&#x52A0; 3 &#x500B; properties
private _defaultLang: string;
private _currentLang: string;
private _fallback: boolean;

public get currentLang() {
    return this._currentLang || this._defaultLang; // &#x7576;&#x6C92;&#x6709;&#x7576;&#x524D;&#x9078;&#x53D6;&#x8A9E;&#x8A00;&#x6642;&#x7528;&#x9810;&#x8A2D;&#x8A9E;&#x8A00;
}

public setDefaultLang(lang: string) {
    this._defaultLang = lang; // &#x8A2D;&#x5B9A;&#x9810;&#x8A2D;
}

public enableFallback(enable: boolean) {
    this._fallback = enable; // &#x662F;&#x5426;&#x555F;&#x7528;&#x5099;&#x7528;
}

private translate(key: string): string { // &#x7FFB;&#x8B6F;&#x50B3;&#x5165;&#x7684;&#x5B57;&#x4E32;
    let translation = key;

    // &#x767C;&#x73FE;&#x76EE;&#x524D;&#x9078;&#x7684;&#x8A9E;&#x8A00;&#x6709;&#x9019;&#x500B;&#x5B57;&#x4E32;
    if (this._translations[this.currentLang] &amp;&amp; this._translations[this.currentLang][key]) {
        return this._translations[this.currentLang][key];
    }

    // &#x4E0D;&#x7528;&#x5099;&#x7528;
    if (!this._fallback) { 
        return translation;
    }

    // &#x767C;&#x73FE;&#x9810;&#x8A2D;&#x8A9E;&#x8A00;&#x6709;&#x9019;&#x5B57;&#x4E32;
    if (this._translations[this._defaultLang] &amp;&amp; this._translations[this._defaultLang][key]) {
        return this._translations[this._defaultLang][key];
    }

    // &#x90FD;&#x6C92;&#x6709;
    return translation;
}
..
</code></pre>
<p>&#x7576;&#x7136;&#x6211;&#x5011;&#x4E5F;&#x53EF;&#x4EE5;</p>
<pre><code>// app/app.component.ts
...

ngOnInit() {
    // &#x53EF;&#x4EE5;&#x505A;&#x4E00;&#x4E9B;&#x4E8B;&#x60C5;..
    ...

    this.subscribeToLangChanged();

    // &#x8A2D;&#x5B9A;&#x9810;&#x8A2D;&#x8A9E;&#x8A00;
    this._translate.setDefaultLang(&apos;en&apos;); // set English as default
    this._translate.enableFallback(true); // enable fallback

    // &#x8A2D;&#x5B9A;&#x76EE;&#x524D;&#x8981;&#x7528;&#x7684;&#x8A9E;&#x8A00;
    this.selectLang(&apos;zh&apos;);
}

...
</code></pre>
<p>&#x73FE;&#x5728;&#x53EF;&#x4EE5;&#x4F86;&#x6E2C;&#x8A66;&#x8A9E;&#x8A00;&#x5305;&#x6C92;&#x6709;&#x5B57;&#x4E32;&#x6642;&#xFF0C;&#x662F;&#x5426;&#x6703;&#x56DE;&#x53BB;&#x627E;&#x9810;&#x8A2D;&#x7684;&#x8A9E;&#x8A00;&#x5B57;&#x4E32;</p>
<pre><code>&lt;p&gt;
    Translate &lt;strong class=&quot;text-muted&quot;&gt;Good bye (fallback)&lt;/strong&gt;: 
    &lt;br&gt;
    &lt;strong&gt;{{ &apos;good bye&apos; | translate }}&lt;/strong&gt;
&lt;/p&gt;
</code></pre>
<p>&#x4E0A;&#x9762;&#x9019;&#x4E00;&#x6BB5;&#xFF0C;&#x4E0D;&#x7BA1;&#x63DB;&#x897F;&#x73ED;&#x7259;&#x8A9E;&#x6216;&#x662F;&#x4E2D;&#x6587;&#xFF0C;&#x90FD;&#x6703;&#x56DE;&#x53BB;&#x627E;&#x82F1;&#x6587;&#x7684;&#x5B57;&#x4E32;&#x4F86;&#x7528;</p>
 <br>
                                                    </div>
                    </div>
                
