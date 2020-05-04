---
title: Angular 2  多語言 ( 1 )
date: 2016-12-27 23:50:25
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x4E00;&#x500B;&#x5C0F;&#x7DB2;&#x7AD9;&#xFF0C;&#x5BA2;&#x7FA4;&#x53EF;&#x80FD;&#x5F88;&#x55AE;&#x4E00;&#xFF0C;&#x5728;&#x53F0;&#x7063;&#x4E5F;&#x8A31;&#x53EA;&#x8981;&#x7DB2;&#x7AD9;&#x53EA;&#x8981;&#x6709;&#x4E2D;&#x6587;&#x5C31;&#x597D;&#x4E86;&#x3002;&#x53EF;&#x662F;&#x96A8;&#x8457;&#x670D;&#x52D9;&#x64F4;&#x5927;&#xFF0C;&#x5BA2;&#x7FA4;&#x4E5F;&#x8DDF;&#x8457;&#x8B8A;&#x5927;&#xFF0C;&#x53EF;&#x80FD;&#x7522;&#x54C1;&#x9032;&#x8ECD;&#x4E9E;&#x6D32;&#xFF0C;&#x751A;&#x81F3;&#x62D3;&#x5C55;&#x5230;&#x5168;&#x7403;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x81F3;&#x5C11;&#x6703;&#x63D0;&#x4F9B;&#x82F1;&#x6587;&#x4ECB;&#x9762;&#xFF0C;&#x751A;&#x81F3;&#x65E5;&#x6587;&#x3001;&#x97D3;&#x6587;&#x90FD;&#x6709;&#x80FD;&#x3002;&#x7576;&#x6211;&#x5011;&#x9EDE;&#x9032;&#x5927;&#x516C;&#x53F8;&#x7684;&#x7DB2;&#x7AD9;&#x6642;&#xFF0C;&#x4E5F;&#x90FD;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x4ED6;&#x5011;&#x63D0;&#x4F9B;&#x597D;&#x5E7E;&#x7A2E;&#x8A9E;&#x8A00;&#xFF0C;&#x53EF;&#x898B;&#x591A;&#x8A9E;&#x8A00;&#x7684;&#x4ECB;&#x9762;&#x975E;&#x5E38;&#x91CD;&#x8981;&#x3002;</p>
<h2>&#x76EE;&#x6A19;</h2>
<p>&#x6A21;&#x677F;&#x53EF;&#x4EE5;&#x9019;&#x6A23;&#x4F7F;&#x7528;</p>
<pre><code>&lt;!-- &#x7576;&#x6211;&#x5011;&#x7FFB;&#x8B6F;&#x6210;&#x897F;&#x73ED;&#x7259;&#x8A9E;&#xFF0C;&#x61C9;&#x8A72;&#x8B8A;&#x6210; &apos;hola mundo&apos;  --&gt;
&lt;p&gt;{{ &apos;hello world&apos; | translate }}&lt;/p&gt;
</code></pre>
<p>&#x6A21;&#x7D44;&#x7684;&#x90E8;&#x5206;&#x5927;&#x6982;&#x6703;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>this.translate.use(&apos;es&apos;); // &#x7528;&#x897F;&#x73ED;&#x7259;&#x6587;
</code></pre>
<p>&#x95DC;&#x65BC;&#x7FFB;&#x8B6F;&#x6280;&#x8853;&#x5C64;&#x9762;&#x7684;&#x65B0;&#x77E5;&#x8B58;&#x4E26;&#x6C92;&#x6709;&#x592A;&#x591A;&#xFF0C;&#x4E3B;&#x8981;&#x662F;&#x5C07;&#x4E00;&#x4E9B;&#x57FA;&#x790E;&#x6982;&#x5FF5;&#x4F5C;&#x61C9;&#x7528;&#xFF0C;&#x56E0;&#x6B64;&#x63A5;&#x4E0B;&#x4F86;&#x6BD4;&#x8F03;&#x4E0D;&#x6703;&#x6709;&#x592A;&#x591A;&#x6587;&#x5B57;&#x89E3;&#x91CB;&#xFF0C;&#x4E3B;&#x8981;&#x9084;&#x662F;&#x4EE5;&#x7A0B;&#x5F0F;&#x78BC;&#x4F86;&#x5C55;&#x73FE;&#x5982;&#x4F55;&#x5BE6;&#x73FE;&#x6211;&#x5011;&#x7684;&#x76EE;&#x6A19;&#x3002;</p>
<p><a href="https://embed.plnkr.co/2RQ9f7q3Gv7gKH5nSJ3K/" target="_blank">Plunker</a></p>
<h2>&#x85CD;&#x5716;</h2>
<pre><code>|- app/
    |- app.component.html
    |- app.component.ts
    |- app.module.ts
    |- main.ts
    |- translate/
        |- index.ts
        |- lang-en.ts
        |- lang-es.ts
        |- lang-zh.ts
        |- translate.pipe.ts
        |- translate.service.ts
        |- translation.ts
|- index.html
|- systemjs.config.js
|- tsconfig.json
</code></pre>
<h2>&#x52D5;&#x5DE5;</h2>
<p>&#x9996;&#x5148;&#x8981;&#x9023;&#x7D50;&#x6211;&#x5011;&#x7684;&#x5B57;&#x5178;&#x6A94;</p>
<pre><code>// app/translate/translation.ts

import { OpaqueToken } from &apos;@angular/core&apos;;

// &#x5F15;&#x9032;&#x6211;&#x5011;&#x7684;&#x8A9E;&#x8A00;&#x6A94;&#x6848;&#x5305;
import { LANG_EN_NAME, LANG_EN_TRANS } from &apos;./lang-en&apos;;
import { LANG_ES_NAME, LANG_ES_TRANS } from &apos;./lang-es&apos;;
import { LANG_ZH_NAME, LANG_ZH_TRANS } from &apos;./lang-zh&apos;;

// translation token
export const TRANSLATIONS = new OpaqueToken(&apos;translations&apos;);

// &#x7FFB;&#x8B6F;&#x8FAD;&#x5178;
const dictionary = {
    [LANG_EN_NAME]: LANG_EN_TRANS,
    [LANG_ES_NAME]: LANG_ES_TRANS,
    [LANG_ZH_NAME]: LANG_ZH_TRANS,
};

// providers
export const TRANSLATION_PROVIDERS = [
    { provide: TRANSLATIONS, useValue: dictionary },
];
</code></pre>
<p><code>TRANSLATION_PROVIDERS</code> &#x6703;&#x8A3B;&#x518A;&#x5728;&#x4E00;&#x958B;&#x59CB;&#x7684; bootstrap&#x3002;</p>
<h2>Translate Service</h2>
<p>&#x63A5;&#x8457;&#x8981;&#x5EFA;&#x7ACB;&#x670D;&#x52D9;&#xFF0C;&#x7528;&#x4F86;&#x505A;&#x5207;&#x63DB;&#x8A9E;&#x8A00;&#x7528;</p>
<pre><code>// app/translate/translate.service.ts

import {Injectable, Inject} from &apos;@angular/core&apos;;
import { TRANSLATIONS } from &apos;./translations&apos;; // import our opaque token

@Injectable()
export class TranslateService {
    private _currentLang: string;

    public get currentLang() {
        return this._currentLang;
    }

    // inject our translations
    constructor(@Inject(TRANSLATIONS) private _translations: any) {
    }

    public use(lang: string): void {
        // set current language
        this._currentLang = lang;
    }

    private translate(key: string): string {
        // private perform translation
        let translation = key;

        if (this._translations[this.currentLang] &amp;&amp; this._translations[this.currentLang][key]) {
            return this._translations[this.currentLang][key];
        }

        return translation;
    }

    public instant(key: string) {
        // call translation
        return this.translate(key); 
    }
}
</code></pre>
<h2>Translation Pipe</h2>
<p>&#x4E4B;&#x524D;&#x4ECB;&#x7D39;&#x904E; Pipe&#xFF0C;&#x76EE;&#x7684;&#x662F;&#x8B93;&#x6211;&#x5011;&#x5728;&#x6A21;&#x677F;&#x4E2D;&#x7684;&#x6587;&#x5B57;&#xFF0C;&#x80FD;&#x900F;&#x904E; Pipe &#x4F86;&#x505A;&#x5207;&#x63DB;&#x3002;</p>
<pre><code>// app/translate/translate.pipe.ts

import { Pipe, PipeTransform } from &apos;@angular/core&apos;;
import { TranslateService } from &apos;../translate&apos;; // translate service

@Pipe({
    name: &apos;translate&apos;,
    pure: false // &#x4F7F;&#x6210;&#x70BA; impure
})

export class TranslatePipe implements PipeTransform {

    constructor(private _translate: TranslateService) { }

    transform(value: string, args: any[]): any {
        if (!value) return;
        return this._translate.instant(value);
    }
}
</code></pre>
<p><code>@Pipe</code> &#x88E1;&#x9762;&#x7684; <code>pure</code> &#x8981;&#x9078; <code>false</code>&#x3002;&#x9019;&#x6A23;&#x624D;&#x6703;&#x8B8A;&#x6210; impure pipe&#x3002; Angular &#x5728;&#x6BCF;&#x6B21;&#x5075;&#x6E2C;&#x8B8A;&#x5316;&#x7684;&#x9031;&#x671F;&#x90FD;&#x6703;&#x57F7;&#x884C; impure pipe&#x3002;&#x5982;&#x679C;&#x662F; pure pipe&#xFF0C;&#x53EA;&#x6709;&#x5728; Input &#x6709;&#x8B8A;&#x5316;&#x624D;&#x6703;&#x57F7;&#x884C;&#x3002; &#x6240;&#x4EE5;&#x9019;&#x908A;&#x6211;&#x5011;&#x8981;&#x52A0;&#x4E0A;&#x9019;&#x53E5;&#xFF0C;&#x624D;&#x80FD;&#x9806;&#x5229;&#x8B93;&#x7A0B;&#x5F0F;&#x7FFB;&#x8B6F;&#x3002;</p>
<h2>&#x5B57;&#x5178;&#x6A94;</h2>
<p>&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F;&#x653E;&#x4E00;&#x5806;&#x8A9E;&#x8A5E;&#x7684;&#x6A21;&#x7D44;&#x3002;</p>
<pre><code>// lang-zh.ts

export const LANG_ZH_NAME = &apos;zh&apos;;

export const LANG_ZH_TRANS = {
    &apos;hello world&apos;: &apos;&#x4F60;&#x597D;&#xFF0C;&#x4E16;&#x754C;&apos;,
};
</code></pre>
<h2>App Module</h2>
<p>&#x57FA;&#x790E;&#x8A2D;&#x7F6E;&#xFF0C;&#x5C07;&#x7528;&#x5230;&#x7684;&#x6771;&#x897F;&#x5F15;&#x5165;&#xFF0C;&#x4E26;&#x5C07; <code>TranslatePipe</code> &#x6CE8;&#x5165;&#x3002;</p>
<pre><code>// app.module.ts

import { NgModule }      from &apos;@angular/core&apos;;
import { BrowserModule } from &apos;@angular/platform-browser&apos;;

import { AppComponent }   from &apos;./app.component&apos;;
import { TRANSLATION_PROVIDERS, TranslatePipe, TranslateService }   from &apos;./translate&apos;;

@NgModule({
  imports:      [ BrowserModule ],
  declarations: [ AppComponent, TranslatePipe ], // Inject Translate Pipe here
  bootstrap:    [ AppComponent ],
  providers:    [ TRANSLATION_PROVIDERS, TranslateService ]
})

export class AppModule { }
</code></pre>
<h2>App Component</h2>
<pre><code>// app/app.component.ts

import { Component, OnInit } from &apos;@angular/core&apos;;
import { TranslateService } from &apos;./translate&apos;;

@Component({
    moduleId: module.id,
    selector: &apos;app-root&apos;,
    templateUrl: &apos;app.component.html&apos;,
})

export class AppComponent implements OnInit {

    public translatedText: string;
    public supportedLanguages: any[];

    constructor(private _translate: TranslateService) { }

    ngOnInit() {
        // standing data
        this.supportedLangs = [
        { display: &apos;English&apos;, value: &apos;en&apos; },
        { display: &apos;Espa&#xF1;ol&apos;, value: &apos;es&apos; },
        { display: &apos;&#x4E2D;&#x6587;&apos;, value: &apos;zh&apos; },
        ];

        // &#x8A2D;&#x5B9A;&#x76EE;&#x524D;&#x8A9E;&#x8A00;
        this.selectLang(&apos;zh&apos;);
    }

    isCurrentLang(lang: string) {
        //&#x78BA;&#x5B9A;&#x9078;&#x7684;&#x8A9E;&#x8A00;&#x662F;&#x5426;&#x70BA;&#x986F;&#x793A;&#x8A9E;&#x8A00;
        return lang === this._translate.currentLang;
    }

    selectLang(lang: string) {
        // &#x8A2D;&#x5B9A;&#x76EE;&#x524D;&#x8A9E;&#x8A00;
        this._translate.use(lang);
        this.refreshText();
    }

    refreshText() {
        // &#x8A9E;&#x8A00;&#x6539;&#x8B8A;&#x5C31;&#x5237;&#x65B0;
        this.translatedText = this._translate.instant(&apos;hello world&apos;);
    }
}
</code></pre>
<h2>App Template</h2>
<p>&#x9019;&#x908A;&#x6211;&#x5011;&#x7528;&#x5169;&#x7A2E;&#x65B9;&#x5F0F;&#x7FFB;&#x8B6F;&#xFF0C;&#x4E00;&#x500B;&#x662F;&#x4F7F;&#x7528; Pipe&#xFF0C;&#x4E00;&#x500B;&#x4F7F;&#x7528;&#x670D;&#x52D9;&#x3002;</p>
<pre><code>&lt;!--app/app.component.html--&gt;

&lt;div class=&quot;container&quot;&gt;
  &lt;h4&gt;Translate: Hello World&lt;/h4&gt;
  &lt;div class=&quot;btn-group&quot;&gt;
    &lt;button *ngFor=&quot;let lang of supportedLangs&quot;
      (click)=&quot;selectLang(lang.value)&quot;
      class=&quot;btn btn-default&quot; [class.btn-primary]=&quot;isCurrentLang(lang.value)&quot;&gt;
      {{ lang.display }}
    &lt;/button&gt;
  &lt;/div&gt;
  &lt;div style=&quot;margin-top: 20px&quot;&gt;
    &lt;p&gt;
      &#x4F7F;&#x7528; Pipe &#x7FFB;&#x8B6F;: &lt;strong&gt;{{ &apos;hello world&apos; | translate }}&lt;/strong&gt;
    &lt;/p&gt;
    &lt;p&gt;
      &#x4F7F;&#x7528; Service &#x7FFB;&#x8B6F;: &lt;strong&gt;{{ translatedText }}&lt;/strong&gt;
    &lt;/p&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>
 <br>
                                                    </div>
                    </div>
                
