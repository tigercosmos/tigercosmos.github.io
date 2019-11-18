---
title: Angular 2 替 Component 加上 CSS 的所有招數
date: 2017-01-01 23:46:04
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x984C;&#x5916;&#x8A71;</h2>
<p>&#x770B;&#x5230;&#x4E00;&#x6BB5;&#x6211;&#x5F88;&#x8A8D;&#x540C;&#x7684;&#x8A71;&#xFF1A;</p>
<blockquote>
<p>&#x61C9;&#x8A72;&#x7531;&#x300C;&#x65B0;&#x624B;&#x300D;&#x4F86;&#x6559;&#x300C;&#x8D85;&#x7D1A;&#x65B0;&#x624B;&#x300D;&#xFF0C;&#x70BA;&#x4EC0;&#x9EBC;&#xFF1F;&#x56E0;&#x70BA;&#x90A3;&#x4E9B;&#x65B0;&#x624B;&#x53EF;&#x80FD;&#x4E00;&#x500B;&#x79AE;&#x62DC;&#x524D;&#x8DDF;&#x4F60;&#x4E00;&#x6A23;&#x5361;&#x5728;&#x8FF4;&#x5708;&#xFF0C;&#x4E0D;&#x77E5;&#x9053;&#x8FF4;&#x5708;&#x5230;&#x5E95;&#x53EF;&#x4EE5;&#x505A;&#x4EC0;&#x9EBC;&#xFF0C;&#x4F46;&#x662F;&#x9019;&#x79AE;&#x62DC;&#x4ED6;&#x5C31;&#x9818;&#x609F;&#x4E86;&#x3002;&#x6211;&#x89BA;&#x5F97;&#x9019;&#x6642;&#x5019;&#x662F;&#x6700;&#x9069;&#x5408;&#x6559;&#x5B78;&#x7684;&#x6642;&#x6A5F;&#xFF0C;&#x56E0;&#x70BA;&#x4ED6;&#x5011;&#x9084;&#x8A18;&#x5F97;&#x300C;&#x7576;&#x521D;&#x5361;&#x4F4F;&#x7684;&#x90A3;&#x7A2E;&#x5FC3;&#x60C5;&#x300D;&#xFF0C;&#x4ED6;&#x5011;&#x662F;&#x6700;&#x61C2;&#x4F60;&#x5FC3;&#x60C5;&#x7684;&#x4EBA;&#x3002;<br>
By <a href="http://blog.techbridge.cc/2016/12/31/review-2016/#sthash.sxQHVfKK.dpuf" target="_blank">&#x4E00;&#x500B;&#x8CC7;&#x6DFA;&#x5DE5;&#x7A0B;&#x5E2B;&#x5E74;&#x672B;&#x7684;&#x81EA;&#x6211;&#x7701;&#x8996;</a></p>
</blockquote>
<p>&#x525B;&#x9032;&#x516C;&#x53F8;&#x6642;&#xFF0C;&#x6211;&#x4E5F;&#x662F;&#x5B8C;&#x5168;&#x6C92;&#x63A5;&#x89F8;&#x904E; Angular 2&#xFF0C;&#x90A3;&#x7A2E;&#x5FAC;&#x5FA8;&#x4E0D;&#x5B89;&#x7684;&#x65E5;&#x5B50;&#x4F9D;&#x7A00;&#x7336;&#x5B58;&#xFF0C;&#x4E00;&#x6BB5;&#x65E5;&#x5B50;&#x904E;&#x53BB;&#x900F;&#x904E;&#x4E0D;&#x65B7;&#x67E5;&#x6587;&#x737B;&#x548C;&#x5BE6;&#x4F5C;&#xFF0C;&#x4E5F;&#x7D42;&#x65BC;&#x7B97;&#x662F;&#x6709;&#x9EDE;&#x61C2;&#x4E86;&#xFF0C;&#x6211;&#x4E00;&#x76F4;&#x8A8D;&#x70BA;&#x7A0B;&#x5F0F;&#x6700;&#x56F0;&#x96E3;&#x7684;&#x5730;&#x65B9;&#x5C31;&#x662F;&#x525B;&#x5165;&#x9580;&#x7684;&#x9580;&#x6ABB;&#xFF0C;&#x4E4B;&#x5F8C;&#x5118;&#x7BA1;&#x4E5F;&#x4E0D;&#x6703;&#x5C31;&#x90FD;&#x5F88;&#x7C21;&#x55AE;&#xFF0C;&#x4F46;&#x81F3;&#x5C11;&#x53EF;&#x4EE5;&#x66A2;&#x884C;&#x7121;&#x963B;&#x3002;</p>
<h2>&#x524D;&#x8A00;</h2>
<p>Angular 2 &#x662F;&#x4E00;&#x500B;&#x7531;&#x7D44;&#x4EF6;&#x69CB;&#x6210;&#x7684;&#x67B6;&#x69CB;&#xFF0C;&#x610F;&#x601D;&#x5C31;&#x662F;&#x6240;&#x6709; UI &#x90FD;&#x662F;&#x5EFA;&#x7ACB;&#x5728;&#x7D44;&#x4EF6;&#x88E1;&#x9762;&#x3002;&#x56E0;&#x6B64;&#x7531;&#x7D44;&#x4EF6;&#x5EFA;&#x7ACB;&#x98A8;&#x683C; (style) &#x6703;&#x8B93;&#x6211;&#x5011;&#x4F7F;&#x7528; Angular &#x66F4;&#x5FEB;&#x6A02;&#x3002;&#x6211;&#x5011;&#x63A5;&#x8457;&#x5C31;&#x8981;&#x8AC7;&#x8AC7;&#x4E0D;&#x540C;&#x7684;&#x5EFA;&#x7ACB;&#x98A8;&#x683C;&#x6280;&#x5DE7;&#xFF0C;&#x4F46;&#x9996;&#x5148;&#x6211;&#x5011;&#x8981;&#x77E5;&#x9053; Shadow DOM &#x548C; View Encapsulation&#x3002;</p>
<h2>&#x89E3;&#x91CB;</h2>
<p>Shadow DOM &#x662F; W3C &#x5B9A;&#x7FA9;&#x7684;&#x7DB2;&#x9801;&#x7D44;&#x4EF6;&#x6A19;&#x6E96;&#x4E4B;&#x4E00;&#x3002;&#x5B83;&#x53EF;&#x4EE5;&#x8B93;&#x4E00;&#x7FA4; DOM &#x5BE6;&#x9AD4;&#x88AB;&#x85CF;&#x5728;&#x55AE;&#x4E00;&#x5143;&#x7D20; ( element ) &#x4E0A; ( &#x4E5F;&#x5C31;&#x662F;&#x7D44;&#x4EF6;&#x7684;&#x6982;&#x5FF5; )&#xFF0C;&#x800C;&#x4E14;&#x53EF;&#x4EE5;&#x5C07;&#x5143;&#x7D20;&#x5C01;&#x88DD; ( encapsulate ) &#x98A8;&#x683C;&#x3002;&#x610F;&#x5473;&#x8457;&#x88AB;&#x5C01;&#x88DD;&#x7684;&#x98A8;&#x683C;&#x53EA;&#x6703;&#x88AB;&#x9019;&#x4E00;&#x7FA4; DOM &#x4F7F;&#x7528;&#x800C;&#x5DF2;&#x3002;</p>
<p>&#x4F46;&#x662F; Shadow DOM &#x4E26;&#x4E0D;&#x662F;&#x6240;&#x6709;&#x700F;&#x89BD;&#x5668;&#x90FD;&#x652F;&#x63F4;&#xFF0C;&#x6C7A;&#x5B9A;&#x8981;&#x4E0D;&#x8981;&#x4F7F;&#x7528;&#x4EE5;&#x53CA;&#x5982;&#x4F55;&#x4F7F;&#x7528; Shadow DOM &#x7684;&#x65B9;&#x6CD5;&#x5C31;&#x7A31;&#x70BA; View Encapsulation&#xFF0C;&#x5206;&#x5225;&#x6709;&#x4E09;&#x7A2E;&#x72C0;&#x614B;&#xFF1A;</p>
<ul>
<li>None&#xFF1A;&#x7121; Shadow DOM &#x5B58;&#x5728;&#x3002;</li>
<li>&#x4EFF;&#x771F; (Emulated)&#xFF1A;&#x8A66;&#x5716;&#x6A21;&#x4EFF;&#x51FA; Shadow DOM&#xFF0C;&#x96D6;&#x7136;&#x4E0D;&#x662F;&#x771F;&#x7684;&#xFF0C;&#x81F3;&#x5C11;&#x8B93;&#x700F;&#x89BD;&#x5668;&#x80FD;&#x4F7F;&#x7528;&#x6211;&#x5011;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#x3002;</li>
<li>&#x81EA;&#x7136; (Native)&#xFF1A;&#x700F;&#x89BD;&#x5668;&#x80FD;&#x5B8C;&#x5168;&#x4F7F;&#x7528; Shadow DOM&#x3002;</li>
</ul>
<p>&#x8A73;&#x7D30;&#x89E3;&#x91CB;&#x9019;&#x4E09;&#x7A2E;&#x5DEE;&#x5728;&#x54EA;&#x88E1;&#xFF0C;&#x53EF;&#x4EE5;&#x53C3;&#x8003;<a href="http://ithelp.ithome.com.tw/articles/10186060" target="_blank">&#x9019;&#x4E00;&#x7BC7;</a></p>
<p>&#x8A2D;&#x7F6E; <code>encapsulation</code> &#x5927;&#x6982;&#x5C31;&#x9577;&#x9019;&#x6A23;&#xFF0C;&#x4ED6;&#x6703;&#x5728; <code>@Component</code> &#x88E1;&#x9762;</p>
<pre><code>@Component({
  templateUrl: &apos;card.html&apos;,
  styles: [`
    .card {
      height: 70px;
      width: 100px;
    }
  `],
  encapsulation: ViewEncapsulation.Native
  // encapsulation: ViewEncapsulation.None
  // encapsulation: ViewEncapsulation.Emulated is default 
})
</code></pre>
<h2>&#x6B63;&#x984C;&#x958B;&#x59CB;</h2>
<p>&#x63A5;&#x8457;&#x5C31;&#x4F86;&#x770B;&#x770B;&#x6709;&#x90A3;&#x4E9B;&#x6280;&#x5DE7;&#x53EF;&#x4EE5;&#x5E6B;&#x7D44;&#x4EF6;&#x52A0;&#x4E0A; CSS</p>
<h3>&#x5BEB;&#x5728; Component &#x88E1;&#x9762;</h3>
<p>&#x9019;&#x662F;&#x6700;&#x5E38;&#x898B;&#x7684;&#x65B9;&#x6CD5;&#xFF0C;&#x4E5F;&#x662F;&#x6700;&#x63A8;&#x85A6;&#x7684;&#xFF0C;&#x5E38;&#x5E38;&#x6703;&#x770B;&#x5230;&#x6587;&#x4EF6;&#x90FD;&#x662F;&#x9019;&#x6A23;&#x7528;&#x3002;<br>
&#x5728;&#x6211;&#x5011;&#x7684; <code>@Component</code> &#x4E2D;&#x5BE6;&#x9AD4;&#x5316;&#xFF1A;</p>
<pre><code>@Component({
  templateUrl: &apos;card.html&apos;,
  styles: [`
    .card {
      height: 70px;
      width: 100px;
    }
  `],
})
</code></pre>
<p>&#x5982;&#x679C;&#x4F7F;&#x7528; view encapsulation &#x6280;&#x8853;&#x7684;&#x9810;&#x671F;&#x7D50;&#x679C;&#xFF1A;</p>
<ul>
<li>None: style &#x76F4;&#x63A5;&#x88AB;&#x5305;&#x88DD;&#x5230; <code>&lt;head&gt;</code> &#x7684; <code>&lt;style&gt;</code> &#x88E1;&#x9762;</li>
<li>Emulated: style &#x88AB;&#x5305;&#x88DD;&#x5230; <code>&lt;head&gt;</code> &#x7684; <code>&lt;style&gt;</code> &#x88E1;&#x9762;&#xFF0C;&#x4F46;&#x53EF;&#x4EE5;&#x8FA8;&#x8B58;&#x8981;&#x5C0D;&#x61C9;&#x7684; Component</li>
<li>Native: &#x5982;&#x540C;&#x9810;&#x671F;&#x4E00;&#x822C;&#x70BA;&#x7DB2;&#x9801;&#x7D44;&#x4EF6;&#x3002;</li>
</ul>
<h3>.CSS</h3>
<p><code>@Component</code> &#x7684; <code>styleUrls</code> &#x53EF;&#x4EE5;&#x5F15;&#x5165;&#x5C0D;&#x61C9;&#x7684; CSS &#x6A94;</p>
<pre><code>@Component({
  styleUrls: [&apos;css/style.css&apos;],
  templateUrl: &apos;card.html&apos;,
})
</code></pre>
<p>&#x5982;&#x679C;&#x4F7F;&#x7528; view encapsulation &#x6280;&#x8853;&#x7684;&#x9810;&#x671F;&#x7D50;&#x679C;&#xFF1A;</p>
<ul>
<li>None: style &#x76F4;&#x63A5;&#x88AB;&#x5305;&#x88DD;&#x5230; <code>&lt;head&gt;</code> &#x7684; <code>&lt;style&gt;</code> &#x88E1;&#x9762;&#x3002;&#x4ED6;&#x6703;&#x88AB;&#x7522;&#x751F;&#x65BC;&#x57F7;&#x884C;&#x5B8C;&#x300C;&#x5BEB;&#x5728; Component &#x88E1;&#x9762;&#x300D;&#x7684;&#x65B9;&#x5F0F;&#x4E4B;&#x5F8C;&#x3002;</li>
<li>Emulated: style &#x88AB;&#x5305;&#x88DD;&#x5230; <code>&lt;head&gt;</code> &#x7684; <code>&lt;style&gt;</code> &#x88E1;&#x9762;&#xFF0C;&#x4F46;&#x53EF;&#x4EE5;&#x8FA8;&#x8B58;&#x8981;&#x5C0D;&#x61C9;&#x7684; Component&#x3002;&#x53CD;&#x800C;&#x4E0D;&#x662F;&#x5F15;&#x5165; <code>link</code> &#x5594;&#xFF01;</li>
<li>Native: &#x5982;&#x540C;&#x9810;&#x671F;&#x4E00;&#x822C;&#x70BA;&#x7DB2;&#x9801;&#x7D44;&#x4EF6;&#x3002;</li>
</ul>
<h3>&#x6A21;&#x677F;</h3>
<p>&#x4E5F;&#x53EF;&#x4EE5;&#x5BEB;&#x5728;&#x6A21;&#x677F;&#x88E1;&#x9762;&#xFF0C;&#x53EF;&#x4EE5;&#x662F;&#x653E;&#x5728; <code>&lt;style&gt;</code> &#x6A19;&#x7C64;&#x6216;&#x662F;&#x653E;&#x5728; HTML tag &#x88E1;&#x9762;</p>
<pre><code>//&#x65B9;&#x6CD5;&#x4E00;
template: `
    &lt;style&gt;
        h1 {
          color: purple;
        }
    &lt;/style&gt;
    &lt;h1&gt;Styling Angular Components&lt;/h1&gt;
    `
})
</code></pre>
<pre><code>//&#x65B9;&#x6CD5;&#x4E8C;
@Component({
  template: &apos;&lt;h1 style=&quot;color:pink&quot;&gt;Styling Angular Components&lt;/h1&gt;&apos;
})
</code></pre>
<p>&#x5982;&#x679C;&#x4F7F;&#x7528; view encapsulation &#x6280;&#x8853;&#x7684;&#x9810;&#x671F;&#x7D50;&#x679C;&#xFF1A;</p>
<ul>
<li>None:
<ul>
<li>&#x65B9;&#x6CD5;&#x4E00;&#xFF1A;style &#x76F4;&#x63A5;&#x88AB;&#x5305;&#x88DD;&#x5230; <code>&lt;head&gt;</code> &#x7684; <code>&lt;style&gt;</code> &#x88E1;&#x9762;&#x3002;&#x4ED6;&#x6703;&#x88AB;&#x7522;&#x751F;&#x65BC;&#x57F7;&#x884C;&#x5B8C;&#x300C;&#x5BEB;&#x5728; Component &#x88E1;&#x9762;&#x300D;&#x7684;&#x65B9;&#x5F0F;&#x4E4B;&#x5F8C;&#x3002;</li>
<li>&#x65B9;&#x6CD5;&#x4E8C;&#xFF1A;&#x76F4;&#x63A5;&#x5BEB;&#x5728; tag &#x88E1;&#x9762;&#x4E86;&#x3002;</li>
</ul>
</li>
<li>Emulated:
<ul>
<li>&#x65B9;&#x6CD5;&#x4E00;&#xFF1A; style &#x88AB;&#x5305;&#x88DD;&#x5230; <code>&lt;head&gt;</code> &#x7684; <code>&lt;style&gt;</code> &#x88E1;&#x9762;&#xFF0C;&#x4F46;&#x53EF;&#x4EE5;&#x8FA8;&#x8B58;&#x8981;&#x5C0D;&#x61C9;&#x7684; Component&#x3002;</li>
<li>&#x65B9;&#x6CD5;&#x4E8C;&#xFF1A;&#x4E00;&#x6A23;&#x662F;&#x76F4;&#x63A5;&#x5BEB;&#x5728; tag &#x88E1;&#x9762;&#x4E86;&#x3002;</li>
</ul>
</li>
<li>Native: &#x5982;&#x540C;&#x9810;&#x671F;&#x4E00;&#x822C;&#x70BA;&#x7DB2;&#x9801;&#x7D44;&#x4EF6;&#x3002;</li>
</ul>
<h2>&#x512A;&#x5148;&#x9806;&#x5E8F;</h2>
<p>&#x6709;&#x4E86;&#x9019;&#x4E09;&#x7A2E;&#x52A0;&#x5165; CSS &#x7684;&#x65B9;&#x6CD5;&#xFF0C;&#x90A3;&#x9EBC;&#x4E00;&#x6B21;&#x90FD;&#x7528;&#x4E0A;&#x53BB;&#x6703;&#x600E;&#x6A23;&#x5462;&#xFF1F;</p>
<pre><code>@Component({
	selector: &apos;my-app&apos;,
    
	//Component style
	styles: [`
	h1 {
	  color: red;
	}
	`],
    
	//External style
	styleUrls[&apos;style.css&apos;],
    
    // Template inline style
	template: `
	&lt;style&gt;
	h1 {
	  color: purple;
	}
	&lt;/style&gt;
	&lt;h1 style=&quot;color:green&quot;&gt;Styling Angular Components&lt;/h1&gt;
	`
})
</code></pre>
<p>&#x5206;&#x5225;&#x662F;&#xFF1A;</p>
<ul>
<li>Component style: &#x5B57;&#x8B8A;&#x7D05;</li>
<li>External style: &#x5B57;&#x8B8A;&#x85CD;</li>
<li>Template inline style: &#x5B57;&#x8B8A;&#x7D2B;</li>
</ul>
<p>&#x9EDE;&#x958B; <a href="http://embed.plnkr.co/2LQMW6sibl9qoqkXhW6P" target="_blank">Plunker</a>&#x770B;&#x770B;&#x7B54;&#x6848;&#x5427;&#xFF01; XD</p>
 <br>
                                                    </div>
                    </div>
                
