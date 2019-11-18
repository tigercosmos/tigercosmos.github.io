---
title: 深入探討瀏覽器引擎如何進行解析
date: 2017-12-13 23:08:30
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x6696;&#x8EAB;&#x5B8C;&#x7562;&#xFF01;&#x672C;&#x6587;&#x958B;&#x59CB;&#x9032;&#x5165;&#x672C;&#x7CFB;&#x5217;&#x91CD;&#x9EDE;&#x3002;<br>
&#x63A5;&#x4E0B;&#x4F86;&#x8981;&#x6DF1;&#x5165;&#x63A2;&#x8A0E;&#x6E32;&#x67D3;&#x5F15;&#x64CE;&#x7684;&#x904B;&#x4F5C;&#x539F;&#x7406;&#x4EE5;&#x53CA;&#x5BE6;&#x4F5C;&#x65B9;&#x5F0F;&#x3002;</p>
<h2>&#x76EE;&#x524D;&#x666E;&#x53CA;&#x7684;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;</h2>
<p>&#x6700;&#x5E38;&#x807D;&#x5230;&#x7684;&#x83AB;&#x904E;&#x65BC; Mozilla &#x7684; Gecko&#xFF0C;&#x6700;&#x4E3B;&#x8981;&#x88AB;&#x7528;&#x5728; Firefox &#x4E0A;&#xFF0C;&#x4E5F;&#x662F;&#x7B2C;&#x4E00;&#x6B3E;&#x88AB;&#x8A2D;&#x8A08;&#x70BA;&#x53EF;&#x4F5C;&#x70BA;&#x55AE;&#x4E00;&#x6A21;&#x7D44;&#x5B58;&#x5728;&#x7684;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;&#x3002;&#x53E6;&#x5916;&#x5C31;&#x662F; WebKit&#xFF0C;&#x8D77;&#x521D;&#x7528;&#x5728; Linux &#x5E73;&#x53F0;&#xFF0C;&#x5F8C;&#x4F86;&#x7D93;&#x7531; Apple &#x516C;&#x53F8;&#x9032;&#x884C;&#x4FEE;&#x6539;&#x5F8C;&#xFF0C;Windows &#x548C; macOS &#x4E5F;&#x652F;&#x63F4;&#xFF0C;&#x4E3B;&#x8981;&#x7528;&#x5728; Chrome &#x548C; Safari&#x3002;&#x9019;&#x5169;&#x6B3E;&#x90FD;&#x662F;&#x958B;&#x6E90;&#x5C08;&#x6848;&#x3002;</p>
<p>&#x95DC;&#x65BC;&#x5169;&#x8005;&#x7684;&#x5DE5;&#x4F5C;&#x6D41;&#x7A0B;&#xFF0C;&#x53EF;&#x4EE5;&#x53C3;&#x8003; <a href="https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/" target="_blank">how browser work</a> &#x9019;&#x7BC7;&#x6587;&#x7AE0;&#x7684;&#x793A;&#x610F;&#x5716;&#x3002;<br>
Webkit &#x9577;&#x9019;&#x6A23;&#xFF1A;<br>
<img src="https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/webkitflow.png" alt><br>
Gecko &#x9577;&#x9019;&#x6A23;&#xFF1A;<br>
<img src="https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/image008.jpg" alt></p>
<p>&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x96D6;&#x7136;&#x5169;&#x8005;&#x63A1;&#x7528;&#x7684;&#x8853;&#x8A9E;&#x4E0D;&#x540C;&#xFF0C;&#x4F46;&#x6982;&#x5FF5;&#x5176;&#x5BE6;&#x662F;&#x5F88;&#x50CF;&#x7684;&#x3002;&#x7576;&#x7136;&#xFF0C;&#x66F4;&#x6DF1;&#x5165;&#x7684;&#x5BE6;&#x4F5C;&#x65B9;&#x5F0F;&#x5C31;&#x5B8C;&#x5168;&#x4E0D;&#x540C;&#x4E86;&#xFF0C;&#x5404;&#x7A2E;&#x5C0F;&#x7D30;&#x7BC0;&#x9020;&#x5C31;&#x4E00;&#x500B;&#x5F15;&#x64CE;&#x7684;&#x53B2;&#x5BB3;&#x7A0B;&#x5EA6;&#xFF0C;&#x4E5F;&#x662F;&#x5404;&#x5BB6;&#x6BD4;&#x62FC;&#x7684;&#x91CD;&#x9EDE;&#xFF01;</p>
<h2>&#x89E3;&#x6790;</h2>
<p>&#x5728;&#x4E0A;&#x9762;&#x5169;&#x5F35;&#x5716;&#x4E2D;&#xFF0C;&#x6211;&#x5011;&#x90FD;&#x53EF;&#x4EE5;&#x770B;&#x5230; HTML Parser&#xFF0C;&#x529F;&#x7528;&#x5C31;&#x662F;&#x628A; HTML &#x7684;&#x539F;&#x59CB;&#x78BC;&#x89E3;&#x6790;&#x6210; DOM tree&#x3002;HTML &#x5728;&#x89E3;&#x6790;&#x7684;&#x6642;&#x5019;&#x4E0D;&#x80FD;&#x7528;&#x4E00;&#x822C;&#x7684;&#x89E3;&#x6790;&#x65B9;&#x5F0F;&#xFF0C;&#x56E0;&#x70BA; HTML &#x672C;&#x8EAB;&#x53EF;&#x4EE5;&#x5BB9;&#x932F;&#xFF0C;&#x4F8B;&#x5982;&#x8AAA;&#x539F;&#x672C;&#x61C9;&#x8A72;&#x662F; <code>&lt;div&gt;&lt;/div&gt;</code>&#xFF0C;&#x4F46;&#x5982;&#x679C;&#x6211;&#x5011;&#x4E0D;&#x5C0F;&#x5FC3;&#x6F0F;&#x6389; <code>&lt;/div&gt;</code>&#xFF0C;&#x4F9D;&#x820A;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x6B63;&#x78BA;&#x5730;&#x986F;&#x793A;&#x3002;&#x96D6;&#x7136;&#x8AAA;&#x5BB9;&#x932F;&#x5C0D;&#x65BC;&#x4F7F;&#x7528;&#x8005;&#x4F86;&#x8AAA;&#x5F88;&#x65B9;&#x4FBF;&#xFF0C;&#x4F46;&#x4E5F;&#x5C31;&#x4F7F;&#x5F97;&#x89E3;&#x6790;&#x7684;&#x65B9;&#x5F0F;&#x6BD4;&#x8F03;&#x7279;&#x5225;&#x4E86;&#x3002;&#x4E8B;&#x5BE6;&#x4E0A;&#xFF0C;<a href="https://www.w3.org/TR/html5/syntax.html#html-parser" target="_blank">W3C</a> &#x6709;&#x5B8C;&#x6574;&#x5B9A;&#x7FA9;&#x5982;&#x4F55;&#x53BB;&#x505A;&#x9019;&#x500B;&#x6B65;&#x9A5F;&#xFF0C;&#x901A;&#x5E38;&#x6211;&#x5011;&#x5728;&#x958B;&#x767C;&#x5F15;&#x64CE;&#x6838;&#x5FC3;&#x6642;&#xFF0C;&#x5C31;&#x662F;&#x76F4;&#x63A5;&#x7167;&#x8457; SPEC &#x4F86;&#x505A;&#x3002;</p>
<p>&#x540C;&#x7406;&#xFF0C; CSS Parser&#xFF0C;&#x529F;&#x7528;&#x5C31;&#x662F;&#x628A; CSS &#x7684;&#x539F;&#x59CB;&#x78BC;&#x89E3;&#x6790;&#x6210; CSS tree&#x3002;&#x800C;&#x4E00;&#x6A23; <a href="https://www.w3.org/TR/CSS2/grammar.html" target="_blank">W3C</a> &#x4E5F;&#x5B9A;&#x7FA9;&#x597D;&#x898F;&#x7BC4;&#x4E86;&#x3002;CSS &#x56E0;&#x70BA;&#x4E0D;&#x50CF; HTML &#x6709;&#x4E0A;&#x4E0B;&#x95DC;&#x4FC2;&#xFF08;&#x6709;<code>&lt;div&gt;</code>&#x5C31;&#x6703;&#x6709;<code>&lt;/div&gt;</code>&#xFF09;&#xFF0C;&#x6240;&#x4EE5;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;&#x4E00;&#x822C;&#x5E38;&#x898B;&#x89E3;&#x6790;&#x7684;&#x89E3;&#x6790;&#x65B9;&#x5F0F;&#x3002;&#x4F8B;&#x5982;&#xFF1A;</p>
<blockquote>
<p>WebKit &#x4F7F;&#x7528;&#x4E86;&#x5169;&#x7A2E;&#x975E;&#x5E38;&#x6709;&#x540D;&#x7684;&#x89E3;&#x6790;&#x5668;&#x751F;&#x6210;&#x5668;&#xFF1A;&#x7528;&#x65BC;&#x5275;&#x5EFA;&#x8A5E;&#x6CD5;&#x5206;&#x6790;&#x5668;&#x7684; Flex &#x4EE5;&#x53CA;&#x7528;&#x65BC;&#x5275;&#x5EFA;&#x89E3;&#x6790;&#x5668;&#x7684; Bison&#xFF08;&#x60A8;&#x4E5F;&#x53EF;&#x80FD;&#x9047;&#x5230; Lex&#x548C; Yacc&#x9019;&#x6A23;&#x7684;&#x5225;&#x540D;&#xFF09;&#x3002;Flex &#x7684;&#x8F38;&#x5165;&#x662F;&#x5305;&#x542B;&#x6A19;&#x8A18;&#x7684;&#x6B63;&#x5247;&#x8868;&#x9054;&#x5F0F;&#x5B9A;&#x7FA9;&#x7684;&#x6A94;&#x6848;&#x3002;Bison &#x7684;&#x8F38;&#x5165;&#x662F;&#x63A1;&#x7528; BNF &#x683C;&#x5F0F;&#x7684;&#x8A9E;&#x8A00;&#x8A9E;&#x6CD5;&#x898F;&#x5247;&#x3002;</p>
</blockquote>
<p>&#x95DC;&#x65BC;&#x700F;&#x89BD;&#x5668;&#x5F15;&#x64CE;&#x7684;&#x8655;&#x7406;&#x65B9;&#x5F0F;&#xFF0C;<a href="https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/" target="_blank">how browser work</a> &#x9019;&#x7BC7;&#x7D93;&#x5178;&#x6587;&#x7AE0;&#x8B1B;&#x7684;&#x592A;&#x6E05;&#x695A;&#x4E86;&#xFF0C;&#x6211;&#x8A8D;&#x70BA;&#x9019;&#x7BC7;&#x5DF2;&#x7D93;&#x975E;&#x5E38;&#x7CBE;&#x7C21;&#x4E5F;&#x5F88;&#x6E05;&#x695A;&#xFF0C;&#x56E0;&#x6B64;&#x4E0D;&#x6253;&#x7B97;&#x91CD;&#x8907;&#x95E1;&#x8FF0;&#x539F;&#x7406;&#x3002;&#x5982;&#x679C;&#x5927;&#x5BB6;&#x5728;&#x95B1;&#x8B80;&#x9019;&#x7BC7;&#x4E0A;&#x6709;&#x9047;&#x5230;&#x554F;&#x984C;&#xFF0C;&#x6B61;&#x8FCE;&#x548C;&#x6211;&#x8A0E;&#x8AD6;&#xFF01;</p>
<h2>&#x958B;&#x767C;</h2>
<p>&#x7576;&#x6211;&#x5011;&#x5728;&#x8A2D;&#x8A08;&#x4E00;&#x500B;&#x700F;&#x89BD;&#x5668;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x5BEB;&#x8655;&#x7406; HTML &#x548C; CSS &#x7684;&#x90E8;&#x5206;&#x662F;&#x76F8;&#x5C0D;&#x5BB9;&#x6613;&#x7684;&#xFF08;&#x9019;&#x908A;&#x4E0D;&#x63A2;&#x8A0E; JS&#xFF0C;&#x90A3;&#x53C8;&#x662F;&#x53E6;&#x4E00;&#x500B;&#x5F15;&#x64CE;&#x4E86;&#xFF09;&#xFF0C;&#x56E0;&#x70BA; W3C &#x90FD;&#x6709;&#x660E;&#x78BA;&#x898F;&#x7BC4;&#xFF0C;&#x4F8B;&#x5982;&#x6211;&#x5011;&#x5E38;&#x807D;&#x5230;&#x7684; HTML5&#x3001;CSS3&#xFF0C;&#x56E0;&#x70BA;&#x8981;&#x8B93;&#x5404;&#x5BB6;&#x54C1;&#x724C;&#x505A;&#x51FA;&#x4F86;&#x7684;&#x6771;&#x897F;&#x53EF;&#x4EE5;&#x5448;&#x73FE;&#x4E00;&#x6A23;&#xFF0C;&#x624D;&#x4E0D;&#x6703;&#x767C;&#x751F;&#x540C;&#x4E00;&#x4EFD;&#x539F;&#x59CB;&#x78BC;&#xFF0C;&#x5728; Chrome &#x4E0A;&#x8DDF;&#x5728; Firefox &#x4E0A;&#x5DEE;&#x975E;&#x5E38;&#x591A;&#xFF0C;&#x9019;&#x6A23;&#x958B;&#x767C;&#x8005;&#x5927;&#x6982;&#x6703;&#x760B;&#x6389;&#x5427;&#xFF01;&#x6240;&#x4EE5; W3C &#x624D;&#x90FD;&#x6709;&#x5B8C;&#x6574;&#x7684;&#x5B9A;&#x7FA9;&#xFF0C;&#x751A;&#x81F3;&#x9664;&#x4E86;&#x898F;&#x5247;&#x4EE5;&#x5916;&#xFF0C;&#x9023;&#x5BE6;&#x4F5C;&#x7684;&#x7D30;&#x9805;&#x6B65;&#x9A5F;&#x90FD;&#x5BEB;&#x5F97;&#x4E00;&#x6E05;&#x4E8C;&#x695A;&#x3002;&#x9592;&#x4F86;&#x7121;&#x4E8B;&#x7684;&#x8A71;&#x53EF;&#x4EE5;&#x9EDE;&#x958B;&#x770B;&#x770B; <a href="https://html.spec.whatwg.org" target="_blank">https://html.spec.whatwg.org</a> &#x3002;</p>
<p>&#x4F8B;&#x5982;&#x64F7;&#x53D6; <a href="https://github.com/servo/servo" target="_blank">Servo</a> &#x5C08;&#x6848; <a href="https://github.com/servo/servo/blob/master/components/script/dom/document.rs" target="_blank"><code>components/script/dom/document.rs</code></a> &#x7684;&#x5176;&#x4E2D;&#x4E00;&#x6BB5;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x9019;&#x76EE;&#x524D;&#x9019;&#x500B;&#x51FD;&#x5F0F;&#xFF0C;&#x5C31;&#x662F;&#x6839;&#x64DA;&#x8A3B;&#x89E3;&#x8D77;&#x4F86;&#x7684; SPEC &#x6587;&#x4EF6;&#x4E2D;&#x7684; <code>current-document-readiness</code> &#x4F86;&#x5BEB;&#x7684;&#x3002;</p>
<pre><code>
// https://html.spec.whatwg.org/multipage/#current-document-readiness
pub fn set_ready_state(&amp;self, state: DocumentReadyState) {
    match state {
        DocumentReadyState::Loading =&gt; {
            // https://developer.mozilla.org/en-US/docs/Web/Events/mozbrowserconnected
            self.trigger_mozbrowser_event(MozBrowserEvent::Connected);
            update_with_current_time_ms(&amp;self.dom_loading);
        },
        DocumentReadyState::Complete =&gt; {
            // https://developer.mozilla.org/en-US/docs/Web/Events/mozbrowserloadend
            self.trigger_mozbrowser_event(MozBrowserEvent::LoadEnd);
            update_with_current_time_ms(&amp;self.dom_complete);
        },
        DocumentReadyState::Interactive =&gt; update_with_current_time_ms(&amp;self.dom_interactive),
    };

    self.ready_state.set(state);

    self.upcast::&lt;EventTarget&gt;().fire_event(atom!(&quot;readystatechange&quot;));
}
</code></pre>
<hr>
<blockquote>
<h3><em><strong>&#x95DC;&#x65BC;&#x4F5C;&#x8005;</strong></em></h3>
<h2>&#x5289;&#x5B89;&#x9F4A;</h2>
<p>&#x8EDF;&#x9AD4;&#x5DE5;&#x7A0B;&#x5E2B;&#xFF0C;&#x71B1;&#x611B;&#x5BEB;&#x7A0B;&#x5F0F;&#xFF0C;&#x66F4;&#x559C;&#x6B61;&#x63A8;&#x5EE3;&#x7A0B;&#x5F0F;&#x8B93;&#x66F4;&#x591A;&#x4EBA;&#x5B78;&#x6703;</p>
<ul>
<li>
<a href="https://tigercosmos.github.io" target="_blank">&#x500B;&#x4EBA;&#x7DB2;&#x7AD9;</a>
</li>
<li>
<a href="https://github.com/tigercosmos" target="_blank">Github</a>
</li>
<li>
<a href="https://www.facebook.com/CodingNeutrino/" target="_blank">FB&#x7C89;&#x5C08;--&#x5FAE;&#x4E2D;&#x5B50;</a>
</li>
</ul>
</blockquote>
 <br>
                                                    </div>
                    </div>
                
