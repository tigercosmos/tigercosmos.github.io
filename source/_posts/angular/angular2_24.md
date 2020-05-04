---
title: Angular 2 事先編譯 Ahead-of-Time (AoT)
date: 2017-01-09 23:47:08
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>Angular 2 &#x96D6;&#x7136;&#x662F;&#x4E00;&#x5957;&#x5F37;&#x5927;&#x6846;&#x67B6;&#xFF0C;&#x4F46;&#x6700;&#x5F8C;&#x8F38;&#x51FA;&#x4ECD;&#x7136;&#x70BA; <code>html</code>&#x3001;<code>js</code>&#x3001;<code>css</code> &#x6A94;&#x6848;&#xFF0C;<code>js</code> &#x672C;&#x8EAB;&#x662F;&#x5373;&#x6642;&#x7DE8;&#x8B6F; (Just-in-Time, JiT)&#xFF0C;&#x700F;&#x89BD;&#x5668;&#x5148;&#x8B80;&#x53D6;&#x6211;&#x5011;&#x7684;&#x6A94;&#x6848;&#xFF0C;&#x7136;&#x5F8C;&#x700F;&#x89BD;&#x5668;&#x908A;&#x770B;&#x908A;&#x7DE8;&#x8B6F;&#xFF0C;&#x4F46;&#x9019;&#x6A23;&#x6BD4;&#x8D77;&#x6709;&#x5148;&#x7DE8;&#x8B6F;&#x904E;&#x7576;&#x7136;&#x6162;&#x4E86;&#x591A;&#xFF0C;&#x5982;&#x679C;&#x4E8B;&#x5148;&#x7DE8;&#x8B6F; (Ahead-of-Time, AoT) &#x7684;&#x8A71;&#xFF0C;&#x7576;&#x6211;&#x5011;&#x7528;&#x700F;&#x89BD;&#x5668;&#x6253;&#x958B;&#x6642;&#xFF0C;&#x5C31;&#x4E0D;&#x7528;&#x7DE8;&#x8B6F;&#xFF0C;&#x65BC;&#x662F;&#x9AD4;&#x9A57;&#x901F;&#x5EA6;&#x5C31;&#x5FEB;&#x4E86;&#x8A31;&#x591A;&#xFF0C;&#x6B64;&#x5916;&#x7DE8;&#x8B6F;&#x904E;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#x4E5F;&#x6703;&#x6BD4;&#x539F;&#x59CB;&#x78BC;&#x8F15;&#x91CF;&#x3002;&#x7531;&#x65BC;&#x5148;&#x7DE8;&#x8B6F;&#x904E;&#xFF0C;&#x5982;&#x679C;&#x6709; bug &#x7684;&#x8A71;&#x4E5F;&#x6703;&#x5F88;&#x5BB9;&#x6613;&#x767C;&#x73FE;&#x3002;</p>
<h2>AoT</h2>
<p>&#x5728; Angular 2 &#x4E2D;&#x6709;&#x5E7E;&#x7A2E;&#x65B9;&#x5F0F;&#x53EF;&#x4EE5;&#x5EFA;&#x69CB; AoT &#x7DB2;&#x9801;&#xFF1A;<br>
1.&#x4F7F;&#x7528;&#x958B;&#x767C;&#x74B0;&#x5883;<br>
2.&#x76F4;&#x63A5;&#x4F7F;&#x7528; <code>ngc</code><br>
3.<code>@ngtools/webpack</code> &#x5957;&#x4EF6;</p>
<p>&#x5982;&#x679C;&#x8981;&#x5EFA;&#x7ACB; AoT &#x8981;&#x505A;&#x591A;&#x8A2D;&#x5B9A;&#xFF0C;&#x5F8C;&#x9762;&#x5169;&#x7A2E;&#x5C6C;&#x65BC;&#x8981;&#x81EA;&#x5DF1;&#x91CD;&#x982D;&#x786C;&#x5E79;&#x7684;&#x65B9;&#x5F0F;&#xFF0C;&#x4ECB;&#x7D39;&#x8D77;&#x4F86;&#x771F;&#x7684;&#x5F88;&#x8907;&#x96DC;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x7C21;&#x55AE;&#x5E36;&#x904E;&#xFF0C;&#x901A;&#x5E38;&#x6211;&#x5011;&#x4E5F;&#x4E0D;&#x9700;&#x8981;&#x9019;&#x6A23;&#x505A;&#x3002;&#x9644;&#x4E0A;&#x4E00;&#x4E9B;&#x6587;&#x7AE0;&#x4F9B;&#x5927;&#x5BB6;&#x53C3;&#x8003;&#xFF1A;<br>
<a href="https://angular.io/docs/ts/latest/cookbook/aot-compiler.html" target="_blank">&#x5B98;&#x65B9;&#x6587;&#x4EF6;</a><br>
<a href="https://blog.mgechev.com/2016/08/14/ahead-of-time-compilation-angular-offline-precompilation/" target="_blank">Ahead-of-Time Compilation in Angular</a><br>
<a href="https://blog.mgechev.com/2016/06/26/tree-shaking-angular2-production-build-rollup-javascript/" target="_blank">Building an Angular 2 Application for Production</a></p>
<h3>1.&#x4F7F;&#x7528;&#x958B;&#x767C;&#x74B0;&#x5883;</h3>
<p>&#x9019;&#x908A;&#x958B;&#x767C;&#x74B0;&#x5883;&#x662F;&#x6307; Angular-Seed &#x9019;&#x985E;&#x7684;&#x74B0;&#x5883;&#xFF0C;&#x6216;&#x662F;&#x5225;&#x4EBA;&#x5DF2;&#x7D93;&#x6253;&#x5305;&#x597D;&#x7684; AoT &#x958B;&#x767C;&#x5C08;&#x6848;&#x76F4;&#x63A5;&#x62FF;&#x4F86;&#x4F7F;&#x7528;&#x3002;</p>
<h4>Angular-Seed</h4>
<p><a href="https://github.com/mgechev/angular-seed" target="_blank">Angular-Seed</a> &#x662F; Angular &#x7B2C;&#x4E8C;&#x53D7;&#x6B61;&#x8FCE;&#x7684;&#x958B;&#x767C;&#x74B0;&#x5883;</p>
<pre><code>$ git clone --depth 1 https://github.com/mgechev/angular-seed.git
$ cd angular-seed

# &#x5B89;&#x88DD;&#x5957;&#x4EF6;
$ npm install
# &#x5FEB;&#x4E00;&#x9EDE;&#x5B89;&#x88DD;&#x5957;&#x4EF6; (&#x7528; Yarn&#xFF1A; https://yarnpkg.com)
$ yarn install  # or yarn

# AoT compilation &#x7DE8;&#x8B6F;&#x6A94;&#x6848;&#xFF0C;&#x6A94;&#x6848;&#x6703;&#x7522;&#x751F;&#x5728; `dist/prod`
$ npm run build.prod.aot
</code></pre>
<h3>2.ngc</h3>
<p>&#x63A1;&#x7528; Angular CLI &#x958B;&#x767C;</p>
<p>&#x9996;&#x5148;&#x8981;&#x5B89;&#x88DD;&#x5957;&#x4EF6;</p>
<pre><code>npm install @angular/compiler-cli @angular/platform-server --save
</code></pre>
<p>&#x5EFA;&#x7ACB;&#x4E00;&#x500B; <code>tsconfig-aot.json</code></p>
<pre><code>{
  &quot;compilerOptions&quot;: {
    &quot;target&quot;: &quot;es5&quot;,
    &quot;module&quot;: &quot;es2015&quot;,
    &quot;moduleResolution&quot;: &quot;node&quot;,
    &quot;sourceMap&quot;: true,
    &quot;emitDecoratorMetadata&quot;: true,
    &quot;experimentalDecorators&quot;: true,
    &quot;lib&quot;: [&quot;es2015&quot;, &quot;dom&quot;],
    &quot;noImplicitAny&quot;: true,
    &quot;suppressImplicitAnyIndexErrors&quot;: true
  },

  &quot;files&quot;: [
    &quot;app/app.module.ts&quot;,
    &quot;app/main.ts&quot;
  ],

  &quot;angularCompilerOptions&quot;: {
   &quot;genDir&quot;: &quot;aot&quot;,
   &quot;skipMetadataEmit&quot; : true
 }
}
</code></pre>
<p>&#x7DE8;&#x8B6F;</p>
<pre><code>node_modules/.bin/ngc -p tsconfig-aot.json
</code></pre>
<p>Bootstrap &#x4E5F;&#x8981;&#x8ABF;&#x6574;</p>
<pre><code>//app/main.ts

import { platformBrowser }    from &apos;@angular/platform-browser&apos;;
import { AppModuleNgFactory } from &apos;../aot/app/app.module.ngfactory&apos;;
platformBrowser().bootstrapModuleFactory(AppModuleNgFactory);
</code></pre>
<p>Rollup: &#x4E00;&#x7A2E; treeshaking &#x7684;&#x6280;&#x5DE7;&#xFF0C;&#x5C31;&#x662F;&#x628A;&#x591A;&#x9918;&#x7121;&#x7528;&#x7684; code &#x50CF;&#x6416;&#x6A39;&#x822C;&#x6416;&#x6389;&#x3002;<br>
&#x9996;&#x5148;&#x8981;&#x5B89;&#x88DD;</p>
<pre><code>npm install rollup rollup-plugin-node-resolve rollup-plugin-commonjs rollup-plugin-uglify --save-dev
</code></pre>
<p>&#x7136;&#x5F8C;&#x589E;&#x52A0;&#x4E00;&#x500B; <code>rollup-config.js</code> &#x6A94;&#x6848;</p>
<pre><code>import rollup      from &apos;rollup&apos;
import nodeResolve from &apos;rollup-plugin-node-resolve&apos;
import commonjs    from &apos;rollup-plugin-commonjs&apos;;
import uglify      from &apos;rollup-plugin-uglify&apos;

export default {
  entry: &apos;app/main.js&apos;,
  dest: &apos;dist/build.js&apos;, // output a single application bundle
  sourceMap: false,
  format: &apos;iife&apos;,
  plugins: [
      nodeResolve({jsnext: true, module: true}),
      commonjs({
        include: &apos;node_modules/rxjs/**&apos;,
      }),
      uglify()
  ]
}
</code></pre>
<p>&#x57F7;&#x884C; rollup</p>
<pre><code>node_modules/.bin/rollup -c rollup-config.js
</code></pre>
<p>&#x628A; <code>index.html</code> &#x4E2D;&#x7528; SystemJS &#x7684;&#x90E8;&#x5206;&#x79FB;&#x9664;&#xFF0C;&#x6539;&#x6210;&#xFF1A;</p>
<pre><code>&lt;body&gt;
  &lt;my-app&gt;Loading...&lt;/my-app&gt;
&lt;/body&gt;

&lt;script src=&quot;dist/build.js&quot;&gt;&lt;/script&gt;
</code></pre>
<p>&#x9019;&#x6A23;&#x5C31;&#x5B8C;&#x6210;&#x56C9;&#xFF01;</p>
<h3>3.@ngtools/webpack</h3>
<p>&#x9996;&#x5148;&#x8981;&#x88DD;&#x9019;&#x500B;&#x5957;&#x4EF6;</p>
<pre><code>npm install -D @ngtools/webpack
</code></pre>
<p>&#x8A2D;&#x5B9A;&#x6210; development dependency</p>
<p>&#x63A5;&#x8457;&#x52A0;&#x5165; Webpack configuration &#x6A94;&#x6848; <code>webpack.config.js</code>&#xFF0C;&#x4E26;&#x52A0;&#x5165;&#x4EE5;&#x4E0B;&#x5167;&#x5BB9;&#xFF1A;</p>
<pre><code>import {AotPlugin} from &apos;@ngtools/webpack&apos;

exports = { /* ... */
  module: {
    rules: [
      {
        test: /\.ts$/,
        loader: &apos;@ngtools/webpack&apos;,
      }
    ]
  },

  plugins: [
    new AotPlugin({
      tsConfigPath: &apos;path/to/tsconfig.json&apos;,
      entryModule: &apos;path/to/app.module#AppModule&apos;
    })
  ]
}
</code></pre>
<p>&#x9019;&#x908A; <code>@ngtools/webpack</code> &#x6703;&#x53D6;&#x4EE3; typescript &#x8F09;&#x5165;&#x5668;&#x50CF;&#x662F; <code>ts-loader</code> &#x6216; <code>awesome-typescript-loader</code>&#x3002; &#x9019;&#x500B;&#x5957;&#x4EF6;&#x6703;&#x548C; AotPlugin &#x4E00;&#x8D77;&#x5B8C;&#x6210; AoT &#x7DE8;&#x8B6F;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
