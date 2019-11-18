---
title: Angular 2 路由
date: 2016-12-24 23:41:16
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x700F;&#x89BD;&#x5668;&#x662F;&#x4E00;&#x500B;&#x6700;&#x719F;&#x6089;&#x7684;&#x5C0E;&#x5411;&#x6A21;&#x578B;&#x61C9;&#x7528;&#x4E86;&#xFF0C;&#x8F38;&#x5165;&#x4E00;&#x500B; URL &#x5730;&#x5740;&#x5F8C;&#x700F;&#x89BD;&#x5668;&#x5C0E;&#x5F15;&#x81F3;&#x76F8;&#x61C9; URL &#x9801;&#x9762;&#xFF0C;&#x9EDE;&#x64CA;&#x7DB2;&#x9801;&#x4E0A;&#x7684;&#x9023;&#x7D50;&#x63A5;&#x5C0E;&#x81F3;&#x53E6;&#x4E00;&#x500B;&#x65B0;&#x7684;&#x9801;&#x9762;&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x7684;&#x300C;&#x524D;&#x4E00;&#x9801;&#x300D;&#x6216;&#x300C;&#x5F8C;&#x4E00;&#x9801;&#x300D;&#x53EF;&#x4EE5;&#x5C0E;&#x822A;&#x81F3;&#x6211;&#x5011;&#x700F;&#x89BD;&#x5668;&#x7684;&#x6B77;&#x53F2;&#x9801;&#x9762;&#x3002;</p>
<p>Angular &#x7D44;&#x4EF6;&#x8DEF;&#x7531;&#x5C31;&#x662F;&#x85C9;&#x7528;&#x9019;&#x500B;&#x6A21;&#x578B;&#xFF0C;&#x53EF;&#x4EE5;&#x7406;&#x89E3;&#x70BA;&#x900F;&#x904E;&#x700F;&#x89BD;&#x5668;&#x7684;&#x7DB2;&#x5740;&#x4F86;&#x751F;&#x6210;&#x4F7F;&#x7528;&#x8005;&#x770B;&#x5230;&#x7684;&#x4ECB;&#x9762;&#xFF0C;&#x4E26;&#x901A;&#x904E;&#x4E00;&#x4E9B;&#x53EF;&#x9078;&#x53C3;&#x6578;&#x6307;&#x5B9A;&#x7576;&#x524D;&#x986F;&#x793A;&#x54EA;&#x4E9B;&#x756B;&#x9762;&#x3002;&#x7576;&#x7136;&#x4E5F;&#x53EF;&#x4EE5;&#x628A;&#x8DEF;&#x7531;&#x7D81;&#x5B9A;&#x81F3;&#x4E00;&#x500B;&#x756B;&#x9762;&#x7D44;&#x4EF6;&#x88E1;&#xFF0C;&#x7576;&#x9EDE;&#x64CA;&#x9023;&#x7D50;&#x6642;&#xFF0C;&#x5C0E;&#x81F3;&#x9069;&#x5408;&#x7684;&#x756B;&#x9762;&#x3002;&#x4E26;&#x4E14;&#x8A18;&#x9304;&#x5728;&#x700F;&#x89BD;&#x5668;&#x6B77;&#x53F2;&#x5217;&#x8868;&#xFF0C;&#x65B9;&#x4FBF;&#x700F;&#x89BD;&#x5668;&#x524D;&#x5F80;&#x4E0B;&#x500B;&#x6216;&#x56DE;&#x5230;&#x4E0A;&#x500B;&#x5DE5;&#x4F5C;&#x3002;</p>
<h2>&#x57FA;&#x790E;</h2>
<p>&#x5728;&#x7DB2;&#x9801;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;&#x4E2D;&#xFF0C; &#x53EF;&#x4EE5;&#x5728; <code>index.html</code> &#x4E2D;&#x53EF;&#x4EE5;&#x8A2D;&#x5B9A; <code>&lt;base&gt;</code> &#x5143;&#x4EF6;&#x4F86;&#x8A2D;&#x5B9A;&#x6839;&#x76EE;&#x9304;&#x3002;</p>
<pre><code>&lt;base href=&quot;/&quot;&gt;
</code></pre>
<p>&#x4F7F;&#x7528; Angular &#x6642;&#x5019;&#xFF0C;&#x6211;&#x5011;&#x8981;&#x5C0E;&#x5165;&#x6A21;&#x7D44; <code>@angular/router</code></p>
<pre><code>import { ROUTER_PROVIDERS } from &apos;@angular/router&apos;;
</code></pre>
<h2>&#x914D;&#x7F6E;</h2>
<p>Angular &#x900F;&#x904E; <code>RouteDefinition</code> &#x4F86;&#x8A2D;&#x5B9A; URL &#x7D66;&#x700F;&#x89BD;&#x5668;&#x67E5;&#x8A62;&#xFF0C;&#x800C;&#x4E00;&#x822C;&#x8DEF;&#x7531;&#x6703;&#x8A2D;&#x5B9A;&#x5728; Parent Component (&#x7236;&#x5143;&#x4EF6;)&#xFF0C;&#x7136;&#x5F8C;&#x900F;&#x904E; <code>@Routes</code> &#x88DD;&#x98FE;&#x5668;&#x4F86;&#x8A3B;&#x518A;&#x8DEF;&#x7531;&#x3002;</p>
<pre><code>@Component({ ... })
@Routes([
  {path: &apos;/crisis-center&apos;, component: CrisisListComponent},
  {path: &apos;/heroes&apos;,        component: HeroListComponent},
  {path: &apos;/hero/:id&apos;,      component: HeroDetailComponent}
])
export class AppComponent  implements OnInit {
  constructor(private router: Router) {}

  ngOnInit() {
    // &#x5C0E;&#x5411; crisis-center &#x9801;&#x9762;
    this.router.navigate([&apos;/crisis-center&apos;]);
  }
}
</code></pre>
<p><code>@Routes</code> &#x88E1;&#x9762;&#x7B2C;&#x4E09;&#x7A2E;&#x7528;&#x6CD5;&#x662F;&#x7528;&#x4F86;&#x53C3;&#x6578;&#x50B3;&#x5740;&#xFF0C;<code>/:id</code> &#x7528;&#x4F86;&#x8F38;&#x5165;&#x53C3;&#x6578;&#xFF0C;&#x4F8B;&#x5982; <code>/hero/58</code></p>
<h3>Router Outlet</h3>
<p>&#x73FE;&#x5728;&#x6211;&#x5011;&#x5DF2;&#x7D93;&#x77E5;&#x9053;&#x5982;&#x4F55;&#x914D;&#x7F6E;&#x8DEF;&#x7531;&#xFF0C;&#x7576;&#x700F;&#x89BD;&#x5668;&#x8ACB;&#x6C42; URL &#x5730;&#x5740;&#xFF1A;<code>/heroes</code> &#x6642;&#xFF0C;&#x8DEF;&#x7531;&#x6703;&#x67E5;&#x627E; <code>RouteDefinition</code> &#x5339;&#x914D;&#x5230; <code>HeroListComponent</code>&#xFF0C;&#x90A3;&#x9EBC;&#x5339;&#x914D;&#x5230;&#x7684;&#x7D44;&#x4EF6;&#x653E;&#x5728;&#x54EA;&#x5462;&#xFF1F;&#x6211;&#x5011;&#x5C31;&#x9700;&#x8981;&#x5728;&#x76EE;&#x524D; Component &#x4E2D; template &#x88E1;&#x52A0;&#x5165; <code>RouterOutlet</code> &#x3002;</p>
<pre><code>&lt;router-outlet&gt;&lt;/router-outlet&gt;
</code></pre>
<h3>&#x8DEF;&#x7531;&#x9023;&#x7D50; (Router Links)</h3>
<p>&#x5728;&#x6A21;&#x677F;&#x88E1;&#x53EF;&#x4EE5;&#x7528; <code>routerLink</code> &#x4F86;&#x5C0E;&#x5411;&#xFF0C;&#x7528;&#x9663;&#x5217;&#x5305;&#x8D77;&#x4F86;&#x662F;&#x56E0;&#x70BA;&#x9084;&#x53EF;&#x4EE5;&#x50B3;&#x53C3;&#x6578;&#x3002;</p>
<pre><code>//app.component.html

&lt;h1&gt;Component Router&lt;/h1&gt;
&lt;nav&gt;
    &lt;a [routerLink]=&quot;[&apos;/crisis-center&apos;]&quot;&gt;Crisis Center&lt;/a&gt;
    &lt;a [routerLink]=&quot;[&apos;/heroes&apos;]&quot;&gt;Heroes&lt;/a&gt;
    
    &lt;!-- &#x4E5F;&#x53EF;&#x4EE5;&#x4E0D;&#x662F;&#x9663;&#x5217;
    &lt;a routerLink=&quot;/crisis-center&quot; routerLinkActive=&quot;active&quot;&gt;Crisis Center&lt;/a&gt;
    &lt;a routerLink=&quot;/heroes&quot; routerLinkActive=&quot;active&quot;&gt;Heroes&lt;/a&gt;
    --&gt;
&lt;/nav&gt;
&lt;router-outlet&gt;&lt;/router-outlet&gt;
</code></pre>
<p>&#x770B;&#x8D77;&#x4F86;&#x5C31;&#x6703;&#x9577;&#x9019;&#x6A23;<br>
<img src="https://angular.io/resources/images/devguide/router/shell-and-outlet.png" alt></p>
<p>&#x5047;&#x8A2D;&#x8981;&#x50B3;&#x53C3;&#x6578;&#x7684;&#x8A71;&#x5C31;&#x9019;&#x6A23;&#x7528;<br>
&#x6A21;&#x677F;&#xFF1A;</p>
<pre><code>  &lt;h1 class=&quot;title&quot;&gt;Angular Router&lt;/h1&gt;
  &lt;nav&gt;
    &lt;a [routerLink]=&quot;[&apos;/crisis-center&apos;]&quot;&gt;Crisis Center&lt;/a&gt;
    &lt;a [routerLink]=&quot;[&apos;/crisis-center/1&apos;, { foo: &apos;foo&apos; }]&quot;&gt;Dragon Crisis&lt;/a&gt;
    &lt;a [routerLink]=&quot;[&apos;/crisis-center/2&apos;]&quot;&gt;Shark Crisis&lt;/a&gt;
  &lt;/nav&gt;
  &lt;router-outlet&gt;&lt;/router-outlet&gt;
</code></pre>
<p>&#x7A0B;&#x5F0F;&#x78BC;&#x8DF3;&#x8F49;&#xFF1A;</p>
<pre><code>this.router.navigate([&apos;/hero&apos;, hero.id]);
</code></pre>
<h2>&#x8A8D;&#x8B49;&#x5B88;&#x885B;</h2>
<p>&#x5047;&#x8A2D;&#x6709;&#x500B;&#x9801;&#x9762;&#x5FC5;&#x9808;&#x8981;&#x767B;&#x5165;&#x624D;&#x80FD;&#x5920;&#x770B;&#x5230;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x8981;&#x7D93;&#x904E;&#x8A8D;&#x8B49;&#x624D;&#x80FD;&#x700F;&#x89BD;&#x9801;&#x9762;&#xFF0C;&#x90A3;&#x9EBC;&#x672A;&#x767B;&#x5165;&#x7684;&#x4EBA;&#x5C31;&#x6703;&#x88AB;&#x5C0E;&#x5411;&#x767B;&#x5165;&#x9801;&#x9762;&#x3002;<br>
&#x59D1;&#x4E14;&#x7A31;&#x9019;&#x7A2E;&#x670D;&#x52D9;&#x53EB;&#x505A;&#x8A8D;&#x8B49;&#x5B88;&#x885B;&#xFF0C;&#x6211;&#x5011;&#x5728;&#x6839;&#x76EE;&#x9304;&#x5BEB;&#x4E00;&#x500B;&#x5B88;&#x885B;&#xFF0C;&#x9019;&#x6A23;&#x5176;&#x4ED6;&#x9801;&#x9762;&#x4E4B;&#x5F8C;&#x90FD;&#x53EF;&#x4EE5;&#x7528;&#x3002;</p>
<pre><code>//auth-guard.service.ts
 
import { Injectable }     from &apos;@angular/core&apos;;
import { CanActivate }    from &apos;@angular/router&apos;;

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate() {
    console.log(&apos;AuthGuard#canActivate called&apos;);
    return true;
  }
}
</code></pre>
<p>&#x9019;&#x4FBF;&#x53EA;&#x662F;&#x8B93;&#x5B88;&#x885B; log &#x8A0A;&#x606F;&#xFF0C;&#x4E26;&#x56DE;&#x50B3; <code>true</code> &#x8B93;&#x5C0E;&#x5411;&#x7E7C;&#x7E8C;&#x3002;</p>
<p>&#x63A5;&#x8457;&#x5C31;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;&#x6211;&#x5011;&#x7684; <code>canActivate</code> &#x4FDD;&#x8B77;&#x63AA;&#x65BD;</p>
<pre><code>//admin/admin-routing.module.ts  

import { AuthGuard } from &apos;../auth-guard.service&apos;;

const adminRoutes: Routes = [
  {
    path: &apos;admin&apos;,
    component: AdminComponent,
    canActivate: [AuthGuard],
    children: [
      {
        path: &apos;&apos;,
        children: [
          { path: &apos;crises&apos;, component: ManageCrisesComponent },
          { path: &apos;heroes&apos;, component: ManageHeroesComponent },
          { path: &apos;&apos;, component: AdminDashboardComponent }
        ],
      }
    ]
  }
];

@NgModule({
  imports: [
    RouterModule.forChild(adminRoutes)
  ],
  exports: [
    RouterModule
  ]
})
export class AdminRoutingModule {}
</code></pre>
<p>&#x9019;&#x6A23;&#x5B50;&#x6211;&#x5011;&#x7C21;&#x55AE;&#x7684;&#x5B88;&#x885B;&#x4FBF;&#x6709;&#x4FDD;&#x8B77;&#x5230; <code>admin</code> &#x9019;&#x500B;&#x9801;&#x9762;&#x4E86;&#x3002;</p>
<p>&#x82E5;&#x8981;&#x66F4;&#x8CBC;&#x5207;&#x771F;&#x5BE6;&#x4E00;&#x9EDE;&#x7684;&#x5B88;&#x885B;&#x6A23;&#x8C8C;&#x7684;&#x8A71;&#xFF0C;&#x5927;&#x6982;&#x6703;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>//auth-guard.service.ts

import { Injectable }       from &apos;@angular/core&apos;;
import {
  CanActivate, Router,
  ActivatedRouteSnapshot,
  RouterStateSnapshot
}                           from &apos;@angular/router&apos;;
import { AuthService }      from &apos;./auth.service&apos;;

@Injectable()
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): boolean {
    let url: string = state.url;

    return this.checkLogin(url);
  }

  checkLogin(url: string): boolean {
    if (this.authService.isLoggedIn) { return true; }

    // &#x5132;&#x5B58;&#x73FE;&#x5728;&#x7684; URL&#xFF0C;&#x9019;&#x6A23;&#x767B;&#x5165;&#x5F8C;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x56DE;&#x4F86;&#x9019;&#x500B;&#x9801;&#x9762;
    this.authService.redirectUrl = url;

    // &#x5C0E;&#x56DE;&#x767B;&#x5165;&#x9801;&#x9762;
    this.router.navigate([&apos;/login&apos;]);
    return false;
  }
}
</code></pre>
 <br>
                                                    </div>
                    </div>
                
