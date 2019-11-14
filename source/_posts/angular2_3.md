---
title: Dependency Injection In Angular 2
date: 2016-12-19 23:47:37
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x6CE8;&#x5165;&#x4F9D;&#x8CF4; (Dependency injection, DI) &#x662F; Angular &#x6700;&#x5927;&#x7684;&#x7279;&#x8272;&#x548C;&#x8CE3;&#x9EDE;&#x3002;&#x4ED6;&#x662F;&#x4E00;&#x7A2E;&#x975E;&#x5E38;&#x91CD;&#x8981;&#x7684;&#x8A2D;&#x8A08;&#x6A21;&#x5F0F;&#x3002;&#x4ED6;&#x8B93;&#x4E0D;&#x540C;&#x7684; Components &#x53EF;&#x4EE5;&#x6CE8;&#x5165;&#x4F9D;&#x8CF4;&#x5728;&#x6574;&#x500B;&#x7DB2;&#x9801;&#x7A0B;&#x5F0F;&#x3002;Components &#x4E0D;&#x9700;&#x8981;&#x77E5;&#x9053;&#x4F9D;&#x8CF4;&#x5982;&#x4F55;&#x7522;&#x751F;&#xFF0C;&#x4E5F;&#x4E0D;&#x9700;&#x8981;&#x77E5;&#x9053;&#x5F7C;&#x6B64;&#x9700;&#x8981;&#x4F9D;&#x8CF4;&#x3002;</p>
<blockquote>
<h4>&#x6458;&#x8981;</h4>
<ul>
<li>&#x4E00;&#x500B; Injector (&#x6CE8;&#x5165;)&#x7528; <code>providers</code> &#x5EFA;&#x7ACB; dependencies(&#x4F9D;&#x8CF4;)&#x3002; Providers &#x6703;&#x77E5;&#x9053;&#x5982;&#x4F55;&#x53BB;&#x5EFA;&#x7ACB; dependencies&#x3002;</li>
<li>TS &#x4E2D;&#x7684;&#x578B;&#x5225;&#x8A3B;&#x91CB;(Type annotations)&#x53EF;&#x4EE5;&#x88AB;&#x7528;&#x4F86;&#x8981;&#x6C42; dependencies &#x3002;&#x6B64;&#x5916;&#x6BCF;&#x500B; Component &#x90FD;&#x6703;&#x6709;&#x81EA;&#x5DF1;&#x7684; injector&#xFF0C;&#x7D44;&#x6210;&#x4E00;&#x500B;&#x67B6;&#x69CB;&#x8B5C;&#x3002;</li>
<li>&#x7528;&#x4E00;&#x500B;&#x4E00;&#x500B; provider &#x5982; <code>@NgModule</code>&#x3001; <code>@Component</code>&#x6216;<code>@Directive</code>&#x4F86;&#x5EFA;&#x7ACB; Injector</li>
<li>&#x5728; Component &#x7684; <code>constructor</code> &#x6CE8;&#x5165;&#x670D;&#x52D9;&#x3002;</li>
</ul>
</blockquote>
<h2>Why DI?</h2>
<p>&#x975E; DI &#x7248;&#x672C;&#x5BE6;&#x4F8B; <code>Car</code>&#xFF1A;</p>
<pre><code>export class Car {
  public engine: Engine;
  public tires: Tires;
  public description = &apos;No DI&apos;;
  constructor() {
    this.engine = new Engine();
    this.tires = new Tires();
  }
  // Method using the engine and tires
  drive() {
    return `${this.description} car with ` +
      `${this.engine.cylinders} cylinders and ${this.tires.make} tires.`
  }
}
</code></pre>
<p>&#x9019;&#x6A23;&#x7F3A;&#x9EDE;&#x662F;&#x9748;&#x6D3B;&#x5EA6;&#x5F88;&#x4F4E;&#xFF0C;<code>Car</code>&#x7684;&#x6240;&#x6709;&#x96F6;&#x4EF6;&#x90FD;&#x88AB;&#x5BEB;&#x6B7B;&#x4E86;&#xFF0C;&#x4EE5;&#x5F8C;&#x60F3;&#x8981;&#x7D66;&#x6539;&#x8B8A;&#x96F6;&#x4EF6;<code>Engine</code>&#x3001;<code>Tires</code>&#xFF0C;&#x662F;&#x5426;&#x8981;&#x5BEB;&#x65B0;&#x7684; Class&#xFF1F;&#x7576;&#x96F6;&#x4EF6;&#x8D8A;&#x4F86;&#x8D8A;&#x591A;&#xFF0C;&#x6BCF;&#x500B;&#x96F6;&#x4EF6;&#x90FD;&#x53EF;&#x4EE5;&#x63DB;&#x4F86;&#x63DB;&#x53BB;&#xFF0C;&#x51FA;&#x932F;&#x7684;&#x6A5F;&#x7387;&#x5C31;&#x5F88;&#x5927;&#x4E86;&#x3002;</p>
<p>&#x518D;&#x4F86;&#x770B;&#x770B; DI &#x7248;&#x672C;&#x7684; <code>Car</code>&#xFF1A;</p>
<pre><code>export class Car {
  public description = &apos;DI&apos;;
  constructor(public engine: Engine, public tires: Tires) { }
}

let car = new Car(new Engine(), new Tires());
</code></pre>
<p>&#x73FE;&#x5728;<code>car</code>&#x53EF;&#x4EE5;&#x8F15;&#x9B06;&#x88DD;&#x4E0A; <code>Engine</code>&#x548C;<code>Tires</code>&#x4E86;&#x3002;<br>
&#x5982;&#x679C;&#x60F3;&#x8981;&#x63DB;&#x96F6;&#x4EF6;&#xFF0C;&#x53EA;&#x662F;&#x5728;&#x5BA3;&#x544A;<code>car</code>&#x7684;&#x6642;&#x5019;&#x88DD;&#x4E0A;&#x65B0;&#x7684;&#x96F6;&#x4EF6;&#x5EF6;&#x4F38; Class&#x3002;</p>
<pre><code>class V8Engine {
  constructor(public cylinders: number) { }
}
// &#x63DB;&#x4E0A;&#x4E0D;&#x540C;&#x7684;&#x5F15;&#x64CE;
let bigCylinders = 12;
let car = new Car(new V8Engine(bigCylinders), new Tires());
</code></pre>
<p>&#x4E00;&#x500B; Class &#x5F9E;&#x5916;&#x90E8;&#x63A5;&#x6536;&#x4F9D;&#x8CF4;&#x800C;&#x975E;&#x5167;&#x90E8;&#x5275;&#x5EFA;&#xFF0C;&#x9019;&#x5C31;&#x662F;&#x4F9D;&#x8CF4;&#x6CE8;&#x5165;(DI)&#x3002;</p>
<p>&#x4F46;&#x6BCF;&#x6B21;&#x8981;&#x4F7F;&#x7528;&#x4E00;&#x500B;&#x7269;&#x4EF6;<code>Car</code>&#xFF0C;&#x9700;&#x8981;&#x81EA;&#x5DF1;&#x88FD;&#x9020;&#x96F6;&#x4EF6;<code>Engine</code>&#x3001;<code>Tires</code>&#xFF0C;&#x9084;&#x8981;&#x81EA;&#x5DF1;&#x7D44;&#x88DD;&#x96F6;&#x4EF6;&#x5BE6;&#x5728;&#x662F;&#x5F88;&#x8CBB;&#x5DE5;&#x592B;&#x7684;&#x4E8B;&#x60C5;&#xFF0C;&#x82E5;&#x662F;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x4F7F;&#x7528;&#x4E00;&#x500B;&#x7269;&#x4EF6;<code>Car</code>&#xFF0C;&#x4F46;&#x6240;&#x4EE5;&#x6771;&#x897F;&#x90FD;&#x88FD;&#x9020;&#x4E5F;&#x7D44;&#x88DD;&#x597D;&#x4E86;&#xFF0C;&#x90A3;&#x8A72;&#x6709;&#x591A;&#x597D;&#xFF01;&#x9019;&#x6642;&#x5019;&#x6211;&#x5011;&#x6709;&#x500B;<code>injector</code>&#x5DF2;&#x7D93;&#x5E6B;&#x4F60;&#x8A3B;&#x518A;&#x7D44;&#x88DD;&#x597D;&#xFF0C;&#x5C31;&#x5982;&#x540C;&#x54C1;&#x724C;&#x7522;&#x54C1;&#xFF0C;&#x76F4;&#x63A5;&#x9818;&#x53D6;&#x4E00;&#x9EDE;&#x4E5F;&#x4E0D;&#x8CBB;&#x5DE5;&#x592B;&#xFF0C;&#x9019;&#x4FBF;&#x662F;&#x6CE8;&#x5165;&#x4F9D;&#x8CF4;&#x6846;&#x67B6;&#x5728;&#x505A;&#x7684;&#x4E8B;&#x60C5;&#x56C9;&#xFF01;</p>
<pre><code>//&#x76F4;&#x63A5;&#x958B;&#x8D70;&#xFF0C;&#x4E0D;&#x9700;&#x8981;&#x81EA;&#x5DF1;&#x88DD;&#x8F2A;&#x80CE;&#xFF0C;&#x4E0D;&#x9700;&#x8981;&#x81EA;&#x5DF1;&#x88DD;&#x5F15;&#x64CE;
let car = injector.get(Car);
</code></pre>
<h2>Angular DI</h2>
<p>&#x5148;&#x770B;&#x770B;&#x9019;&#x5F35;&#x5716;<br>
<img src="https://2.bp.blogspot.com/-TK9PPhNi4nE/VyGveZ_AL8I/AAAAAAAAOMI/4x0j_TX6-EQLsVugbL0l_qy6UR1OFlPOwCLcB/s1600/Dependency%2BInjection%2Bin%2BAngular%2B2.png" alt="angular DI figure"><br>
&#x5728; Angular 2 &#x4E2D; DI &#x57FA;&#x672C;&#x4E0A;&#x662F;&#x7531;&#x4E09;&#x500B;&#x6771;&#x897F;&#x7D44;&#x6210;&#x7684;&#xFF1A;</p>
<ul>
<li>Injector - &#x6703;&#x88AB;&#x5BE6;&#x4F8B;&#x4F9D;&#x8CF4;&#x7684;&#x6CE8;&#x5165;&#x5C0D;&#x8C61;&#x3002;</li>
<li>Provider - &#x544A;&#x8A34; Injector &#x5982;&#x4F55;&#x5275;&#x5EFA;&#x4E00;&#x500B;&#x4F9D;&#x8CF4;&#x5BE6;&#x4F8B;&#x7684;&#x67B6;&#x69CB;&#x8B5C;&#x3002;</li>
<li>Dependency - &#x5275;&#x5EFA;&#x5C0D;&#x8C61;&#x7684; Type</li>
</ul>
<h3>&#x5BE6;&#x73FE;</h3>
<p>Angular&#x63D0;&#x4F9B;&#x81EA;&#x5DF1;&#x7684; DI &#x6846;&#x67B6;&#xFF0C;&#x9084;&#x53EF;&#x4EE5;&#x628A;&#x9019;&#x500B;&#x6846;&#x67B6;&#x7368;&#x7ACB;&#x904B;&#x7528;&#x5230;&#x5176;&#x4ED6;&#x7CFB;&#x7D71;&#x4E2D;&#x3002;<br>
Angular&#x5728;&#x555F;&#x52D5;&#x6642;&#x6703;&#x81EA;&#x52D5;&#x5275;&#x5EFA; injector&#x3002;</p>
<pre><code>bootstrap(AppComponent);
</code></pre>
<p>&#x6B64;&#x6642;&#x53EA;&#x9700;&#x5C0D;provider&#x53C3;&#x6578;&#x8A3B;&#x518A;&#x5BE6;&#x4F8B;&#x3002;</p>
<pre><code>bootstrap(AppComponent,
         [MyService]); // &#x4E0D;&#x5EFA;&#x8B70;&#xFF0C;&#x4F46;&#x884C;&#x5F97;&#x901A;
</code></pre>
<p>&#x4F46;&#x9019;&#x6A23;&#x7576;&#x5F88;&#x591A;&#x7684; Class &#x90FD;&#x8981;&#x8A3B;&#x518A;&#x6642;&#xFF0C;&#x4FBF;&#x986F;&#x5F97;&#x975E;&#x5E38;&#x4E0D;&#x5BE6;&#x969B;&#x4E86;&#x3002;</p>
<p>&#x6240;&#x4EE5;&#x6211;&#x5011;&#x4E0D;&#x6703;&#x5728; <code>bootstrap</code> &#x88E1;&#x9762;&#x653E;&#x5165;&#x6240;&#x6709;&#x8981;&#x8A3B;&#x518A;&#x7684;&#x6771;&#x897F;&#x3002;</p>
<h4>&#x7D44;&#x4EF6;&#x5167;&#x8A3B;&#x518A;</h4>
<p>&#x5C0D;&#x65BC;&#x8A31;&#x591A;&#x7D44;&#x4EF6;&#x6703;&#x7528;&#x5230;&#x7684;&#x670D;&#x52D9;&#x3001;&#x901A;&#x9053;&#xFF0C;&#x6700;&#x4E0A;&#x5C64;&#x4E5F;&#x5C31;&#x662F;&#x7D44;&#x4EF6;&#x672C;&#x8EAB;&#x4E86;&#x3002;&#x63DB;&#x8A00;&#x4E4B;&#xFF0C;&#x9664;&#x4E86;&#x9019;&#x500B;&#x7D44;&#x4EF6;&#x5176;&#x4ED6;&#x7D44;&#x4EF6;&#x7528;&#x4E0D;&#x5230;&#xFF0C;&#x90A3;&#x9EBC;&#x6211;&#x5011;&#x4E0D;&#x9700;&#x8981;&#x628A;&#x9019;&#x4E9B;&#x670D;&#x52D9;&#x3001;&#x901A;&#x9053;&#x6CE8;&#x5165;&#x4F9D;&#x8CF4;&#x5728;&#x5168;&#x57DF;&#xFF0C;&#x53EA;&#x8981;&#x5728;&#x7D44;&#x4EF6;&#x4E4B;&#x4E0B;&#x5C31;&#x597D;&#x3002;</p>
<p>&#x8209;&#x4F8B;&#xFF1A;</p>
<pre><code>import { Component }          from &apos;angular2/core&apos;;
import { HeroListComponent }  from &apos;./hero-list.component&apos;;
import { HeroService }        from &apos;./hero.service&apos;;
@Component({
  selector: &apos;my-heroes&apos;,
  template: `
  &lt;h2&gt;Heroes&lt;/h2&gt;
  &lt;hero-list&gt;&lt;/hero-list&gt;
  `,
  providers:[HeroService],
  directives:[HeroListComponent]
})
export class HeroesComponent { }
</code></pre>
<p>&#x5176;&#x4E2D;&#x7684; <code>providers:[HeroService],</code> &#x53EA;&#x5411; <code>HeroesComponent</code> &#x548C;&#x65D7;&#x4E0B;&#x5B50;&#x7D44;&#x4EF6; <code>HeroListComponent</code> &#x63D0;&#x4F9B;&#x670D;&#x52D9;&#x3002;</p>
<p>&#x5728;&#x57F7;&#x884C; <code>HeroesComponent</code> &#x7684;&#x6642;&#x5019;&#xFF0C; DI &#x6703;&#x627E;&#x5230;&#x4E4B;&#x524D;&#x8A3B;&#x518A;&#x7684;&#x670D;&#x52D9;&#xFF0C;&#x7136;&#x5F8C;&#x53D6;&#x5F97; <code>HeroService</code> &#x5BE6;&#x4F8B;&#xFF0C;&#x8ABF;&#x7528;&#x88E1;&#x9762;&#x7684;&#x51FD;&#x6578;&#xFF0C;&#x9019;&#x4E00;&#x5207;&#x90FD;&#x662F;&#x4EE5; DI &#x5F62;&#x5F0F;&#x9032;&#x884C;&#x3002;</p>
<pre><code>import { Component }   from &apos;angular2/core&apos;;
import { Hero }        from &apos;./hero&apos;;
import { HeroService } from &apos;./hero.service&apos;;
@Component({
  selector: &apos;hero-list&apos;,
  template: `
  &lt;div *ngFor=&quot;#hero of heroes&quot;&gt;
    {{hero.id}} - {{hero.name}}
  &lt;/div&gt;
  `,
})
export class HeroListComponent {
  heroes: Hero[];
  constructor(heroService: HeroService) {
    this.heroes = heroService.getHeroes();
  }
}
</code></pre>
<h4>&#x96B1;&#x5F62;&#x5F0F; DI</h4>
<p>&#x5947;&#x602A;&#xFF1F;&#x6C92;&#x770B;&#x5230;&#x6709;&#x4F7F;&#x7528; DI &#x7684;&#x8A9E;&#x6CD5;&#x554A;&#xFF1F;<br>
&#x9019;&#x662F;&#x56E0;&#x70BA; Angular &#x6703;&#x81EA;&#x52D5;&#x5E6B;&#x6211;&#x5011;&#x5B8C;&#x6210;&#x3002;</p>
<pre><code>injector = Injector.resolveAndCreate([Car, Engine, Tires, Logger]);
let car = injector.get(Car);
</code></pre>
<h4>&#x55AE;&#x4F8B;&#x5BE6;&#x4F8B;</h4>
<p>injector &#x9ED8;&#x8A8D;&#x63D0;&#x4F9B;&#x7684; DI &#x90FD;&#x662F;&#x55AE;&#x4F8B;&#x5BE6;&#x4F8B;&#xFF0C;&#x6240;&#x4EE5; <code>HeroesComponent</code> &#x548C; <code>HeroListComponent</code> &#x6703;&#x5171;&#x4EAB;&#x540C;&#x4E00;&#x500B;&#x5BE6;&#x4F8B;&#x3002;&#x610F;&#x601D;&#x662F;&#xFF0C;<code>HeroesComponent</code> &#x82E5;&#x662F;&#x5C0D; DI &#x5BE6;&#x4F8B;&#x505A;&#x8B8A;&#x5316;&#xFF0C;<code>HeroListComponent</code> &#x4E0B;&#x6B21;&#x4F7F;&#x7528;&#x9019;&#x500B; DI &#x5BE6;&#x4F8B;&#x6642;&#xFF0C;&#x6703;&#x662F;&#x5DF2;&#x7D93;&#x8B8A;&#x5316;&#x904E;&#x7684;&#x5BE6;&#x4F8B;&#x3002;</p>
<h3>Why @Injectable()?</h3>
<p>&#x770B;&#x4E00;&#x4E0B;&#x4E0B;&#x9762;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#xFF1A;</p>
<pre><code>import { Injectable } from &apos;@angular/core&apos;;
@Injectable()
export class Logger {
  logs: string[] = []; // capture logs for testing
  log(message: string) {
    this.logs.push(message);
    console.log(message);
  }
}
</code></pre>
<p>&#x6CE8;&#x610F;&#x5230;&#x88E1;&#x9762;&#x6709; <code>@Injectable()</code> &#x4E86;&#x55CE;&#xFF1F;</p>
<p>&#x7167;&#x81EA;&#x9762;&#x4E0A;&#x610F;&#x601D;&#x5C31;&#x662F;&#x8981;&#x6CE8;&#x5165;&#x9019;&#x500B; class&#xFF0C;&#x4F46;&#x4E4B;&#x524D;&#x6C92;&#x6709;&#x4F7F;&#x7528; <code>@Injectable</code>  &#x4E5F;&#x53EF;&#x4EE5;&#x4F7F;&#x7528; DI &#x5440;&#xFF1F;<br>
&#x9019;&#x662F;&#x56E0;&#x70BA; <code>@Component</code>&#x3001;<code>@Directive</code>&#x3001;<code>@Pipe</code>&#xFF0C;&#x90FD;&#x662F; Injectable &#x7684;&#x5B50;&#x578B;&#x3002;</p>
<p>&#x800C;&#x9019;&#x908A;&#x56E0;&#x70BA;&#x90FD;&#x6C92;&#x6709;&#x88DD;&#x98FE;&#x5668;&#xFF0C;&#x6240;&#x4EE5;&#x9700;&#x8981;&#x52A0;&#x4E0A; <code>Injectable</code> &#x4F86;&#x544A;&#x8A34; ts&#xFF0C;&#x8B93;&#x4ED6;&#x7522;&#x751F; metadata&#xFF0C;&#x624D;&#x80FD;&#x6B63;&#x5E38;&#x7DE8;&#x8B6F;&#x3002;</p>
<h2>&#x7E3D;&#x7D50;</h2>
<p>DI &#x662F;&#x975E;&#x5E38;&#x91CD;&#x8981;&#x6280;&#x5DE7;&#xFF0C;&#x7B97;&#x662F;&#x4E00;&#x7A2E;&#x5F88;&#x5E38;&#x7528;&#x7684;&#x8A2D;&#x8A08;&#x6A21;&#x5F0F;&#xFF0C; Angular &#x4E2D;&#x4E5F;&#x7121;&#x6240;&#x4E0D;&#x5728;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
