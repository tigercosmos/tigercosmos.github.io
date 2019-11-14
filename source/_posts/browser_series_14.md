---
title: 瀏覽器開發進階實戰（一） value sanitization of input type
date: 2017-12-25 23:42:49
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x6211;&#x5011;&#x73FE;&#x5728;&#x4E86;&#x89E3;&#x5982;&#x4F55;&#x958B;&#x767C;&#x4E00;&#x500B;&#x7C21;&#x6613;&#x7248;&#x7684;&#x700F;&#x89BD;&#x5668;&#x4E86;&#x3002;&#x5728;&#x672C;&#x7CFB;&#x5217;&#x7684;&#x5148;&#x524D;&#x6587;&#x7AE0;&#x7576;&#x4E2D;&#xFF0C;&#x5DF2;&#x7D93;&#x5E36;&#x5927;&#x5BB6;&#x4E00;&#x6B65;&#x4E00;&#x6B65;&#x5B8C;&#x6210;&#x4E00;&#x500B;&#x300C;&#x73A9;&#x5177;&#x300D;&#x7B49;&#x7D1A;&#x7684;&#x700F;&#x89BD;&#x5668;&#xFF0C;&#x96D6;&#x7136;&#x529F;&#x80FD;&#x5F88;&#x7C21;&#x964B;&#xFF0C;&#x5F88;&#x591A;&#x6771;&#x897F;&#x4E0D;&#x652F;&#x63F4;&#xFF0C;&#x4F46;&#x537B;&#x662F;&#x8CA8;&#x771F;&#x50F9;&#x5BE6;&#x7684;&#x700F;&#x89BD;&#x5668;&#xFF01;</p>
<p>&#x4F46;&#x6211;&#x5011;&#x4E26;&#x4E0D;&#x6EFF;&#x8DB3;&#xFF0C;&#x6211;&#x5011;&#x60F3;&#x505A;&#x7684;&#x662F;&#x4E00;&#x500B;&#x771F;&#x6B63;&#x7684;&#x7522;&#x54C1;&#xFF0C;&#x662F;&#x529F;&#x80FD;&#x9F4A;&#x5168;&#x3001;&#x8A2D;&#x8A08;&#x826F;&#x597D;&#x3001;&#x6548;&#x80FD;&#x8D85;&#x68D2;&#x7684;&#x700F;&#x89BD;&#x5668;&#xFF01;&#x9019;&#x9EBC;&#x4E00;&#x500B;&#x7522;&#x54C1;&#x7576;&#x7136;&#x4E0D;&#x53EF;&#x80FD;&#x96A8;&#x624B;&#x5C31;&#x505A;&#x51FA;&#x4F86;&#xFF0C;&#x5E02;&#x9762;&#x4E0A;&#x7684;&#x700F;&#x89BD;&#x5668;&#xFF0C;&#x54EA;&#x4E00;&#x500B;&#x4E0D;&#x662F;&#x958B;&#x767C;&#x5341;&#x5E74;&#xFF0C;&#x7531;&#x7121;&#x6578;&#x958B;&#x767C;&#x8005;&#x6240;&#x5806;&#x780C;&#x51FA;&#x4F86;&#x7684;&#x5462;&#xFF1F;</p>
<p>&#x672C;&#x7CFB;&#x5217;&#x7684;&#x9032;&#x968E;&#x5BE6;&#x6230;&#x90E8;&#x5206;&#x5C07;&#x4EE5; <a href="https://github.com/servo/servo" target="_blank">Servo</a> &#x5C08;&#x6848;&#x70BA;&#x4F8B;&#xFF0C;&#x5BE6;&#x4F5C;&#x4E00;&#x4E9B;&#x529F;&#x80FD;&#xFF0C;&#x8B93;&#x5927;&#x5BB6;&#x4E86;&#x89E3;&#x771F;&#x6B63;&#x958B;&#x767C;&#x700F;&#x89BD;&#x5668;&#x662F;&#x600E;&#x9EBC;&#x4E00;&#x56DE;&#x4E8B;&#x3002;</p>
<p>&#x6211;&#x5011;&#x90FD;&#x77E5;&#x9053;&#xFF0C;&#x4E00;&#x53F0;&#x6A5F;&#x5668;&#x662F;&#x7531;&#x597D;&#x5E7E;&#x500B;&#x5927;&#x7D44;&#x4EF6;&#x69CB;&#x6210;&#xFF0C;&#x5927;&#x7D44;&#x5EFA;&#x53C8;&#x662F;&#x597D;&#x591A;&#x5C0F;&#x96F6;&#x4EF6;&#x6240;&#x62FC;&#x8D77;&#x4F86;&#xFF0C;&#x5C0F;&#x96F6;&#x4EF6;&#x53EF;&#x80FD;&#x53C8;&#x662F;&#x7531;&#x5E7E;&#x500B;&#x7D20;&#x6750;&#x6240;&#x88FD;&#x9020;&#x3002;<br>
&#x597D;&#x4E86;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x4ECA;&#x5929;&#x8B1B;&#x7684;&#x6771;&#x897F;&#x662F;&#xFF0C;HTML &gt; input &#x5143;&#x7D20; &gt; type &gt; value sanitization(&#x6AA2;&#x67E5;&#x6578;&#x503C;)&#xFF0C;&#x9019;&#x6A23;&#x8B1B;&#x5927;&#x5BB6;&#x53EF;&#x80FD;&#x4E0D;&#x6E05;&#x8655;&#xFF0C;&#x7A76;&#x7ADF; type &#x662F;&#x4EC0;&#x9EBC;&#xFF1F;</p>
<p>input &#x7684; type &#x5C31;&#x662F;&#xFF1A;</p>
<pre><code>&lt;input type=&quot;month&quot;&gt;
&lt;input type=&quot;week&quot;&gt;
&lt;input type=&quot;time&quot;&gt;
&lt;input type=&quot;color&quot;&gt;
</code></pre>
<p>&#x7136;&#x5F8C; <code>type</code> &#x6703;&#x6709; <code>value</code> &#x5C31;&#x50CF;&#x662F;&#xFF1A;</p>
<pre><code>&lt;input type=&quot;month&quot; value=&quot;2014-09&quot;&gt;
&lt;input type=&quot;week&quot; value=&quot;2014-W52&quot;&gt;
&lt;input type=&quot;time&quot; value=&quot;17:30:23&quot;&gt;
&lt;input type=&quot;color&quot; value=&quot;#ffffff&quot;&gt;
</code></pre>
<p>&#x53EF;&#x662F;&#x554F;&#x984C;&#x5C31;&#x4F86;&#x4E86;&#xFF0C;&#x8AB0;&#x77E5;&#x9053;&#x4F60;&#x7D66;&#x7684;&#x6578;&#x503C;&#x662F;&#x4E0D;&#x662F;&#x6B63;&#x78BA;&#x7684;&#x5462;&#xFF1F;<br>
&#x4F8B;&#x5982;&#xFF1A;</p>
<pre><code>&lt;input type=&quot;month&quot; value=&quot;2014-29&quot;&gt;
</code></pre>
<p>&#x6708;&#x4EFD;&#x6700;&#x9AD8;&#x5C31;&#x5230; 12&#xFF0C;&#x6240;&#x4EE5;&#x4E0A;&#x9762;&#x7684;&#x7576;&#x7136;&#x5C31;&#x662F;&#x932F;&#x7684;&#xFF01;</p>
<p>&#x6240;&#x4EE5;&#x91DD;&#x5C0D;&#x9019;&#x500B;&#xFF0C;&#x6709; <a href="https://html.spec.whatwg.org/multipage/input.html" target="_blank">WHATWG&#x7684;&#x6587;&#x4EF6;</a>&#x53EF;&#x4EE5;&#x53C3;&#x8003;&#x3002;</p>
<p>&#x50CF;&#x662F;&#x4EE5; <code>week</code> &#x9019;&#x500B; type &#x70BA;&#x4F8B;&#xFF1A;<br>
&#x6587;&#x4EF6;&#x6709;&#x8AAA;&#x660E;&#x600E;&#x6A23;&#x624D;&#x662F;&#x6709;&#x6548;&#x7684;&#x6578;&#x503C;&#xFF1A;<a href="https://html.spec.whatwg.org/multipage/input.html#week-state-(type=week):value-sanitization-algorithm" target="_blank">https://html.spec.whatwg.org/multipage/input.html#week-state-(type=week):value-sanitization-algorithm</a><br>
&#x5224;&#x65B7;&#x6709;&#x6548;&#x6578;&#x503C;&#x7684;&#x6F14;&#x7B97;&#x6CD5;&#x4E5F;&#x6709;&#x6587;&#x4EF6;&#xFF1A; <a href="https://html.spec.whatwg.org/multipage/#parse-a-week-string" target="_blank">https://html.spec.whatwg.org/multipage/#parse-a-week-string</a></p>
<p>&#x7136;&#x5F8C;&#x6211;&#x5011;&#x5C31;&#x53EF;&#x4EE5;&#x5BE6;&#x4F5C;&#x4E86;&#xFF0C;&#x9019;&#x6BB5;&#x7A0B;&#x5F0F;&#x662F;&#x6211;&#x5BEB;&#x7684;&#xFF0C;&#x4E5F;&#x662F;&#x7167;&#x8457;&#x6587;&#x4EF6;&#x5BEB;&#xFF0C;&#x6BCF;&#x500B;&#x6B65;&#x9A5F;&#x90FD;&#x6709;&#x5C0D;&#x61C9;&#x6587;&#x4EF6;&#x4E0A;&#x7684;&#x6B65;&#x9A5F;&#x7DE8;&#x865F;&#x3002;</p>
<hr>
<p>&#x9996;&#x5148;&#x5F9E; input element &#x4E2D;&#x53D6;&#x5F97;&#x5C0D;&#x61C9;&#x7684; type &#x7684;&#x6578;&#x503C; (<a href="https://github.com/servo/servo/blob/7aae164fcdb8ab308bfa0806e1123e9b7eb73a7c/components/script/dom/htmlinputelement.rs#L1008-L1012" target="_blank">Gthub</a>)</p>
<pre><code>InputType::Week =&gt; {
    // &#x53D6;&#x5F97;&#x6578;&#x503C;
    let mut textinput = self.textinput.borrow_mut();
    // &#x5224;&#x65B7;&#x662F;&#x5426;&#x5408;&#x7406;
    if !textinput.single_line_content().is_valid_week_string() {
        // &#x4E0D;&#x662F;&#x6709;&#x6548;&#x7684;&#x6578;&#x503C;&#x5C31;&#x6E05;&#x9664;&#x6210; &quot;&quot;
        *textinput.single_line_content_mut().clear();
    }
}
</code></pre>
<p>&#x4E0A;&#x9762;&#x53EF;&#x4EE5;&#x770B;&#x5230; <code>is_valid_week_string()</code>&#xFF0C;&#x9019;&#x4E32;&#x662F; DOM &#x7684; binding&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x81EA;&#x8EAB;&#x7684;&#x65B9;&#x6CD5;&#xFF0C;&#x53EF;&#x4EE5;&#x7528;&#x4F86;&#x6AA2;&#x67E5;&#x6578;&#x503C;&#x3002;</p>
<pre><code>pub fn is_valid_week_string(&amp;self) -&gt; bool {
    // &#x5617;&#x8A66;&#x89E3;&#x6790;
    parse_week_string(&amp;*self.0).is_ok()
}
</code></pre>
<p>&#x6AA2;&#x67E5;&#x6578;&#x503C;&#x7684;&#x6642;&#x5019;&#x6703;&#x5617;&#x8A66;&#x89E3;&#x6790;&#x5B57;&#x4E32;&#xFF0C;&#x9019;&#x908A;&#x662F;&#x89E3;&#x6790;&#x7684;&#x6F14;&#x7B97;&#x6CD5;&#xFF0C;&#x89E3;&#x6790;&#x6210;&#x529F;&#x7684;&#x8A71;&#x5C31;&#x6703;&#x4F7F;&#x4E0A;&#x9762;&#x7684; <code>is_valid_week_string</code> &#x70BA;&#x771F;&#xFF0C;&#x5C31;&#x7B97;&#x901A;&#x904E;&#x6AA2;&#x67E5;&#x3002;(<a href="https://github.com/servo/servo/blob/7aae164fcdb8ab308bfa0806e1123e9b7eb73a7c/components/script/dom/bindings/str.rs#L457-L497" target="_blank">Github</a>)</p>
<pre><code>/// https://html.spec.whatwg.org/multipage/#parse-a-week-string
fn parse_week_string(value: &amp;str) -&gt; Result&lt;(u32, u32), ()&gt; {
    // Step 1, 2, 3 &#x53D6;&#x5F97;&#x5E74;&#x4EFD;&#xFF0C;&#x70BA; &quot;-&quot; &#x5207;&#x958B;&#x7684;&#x7B2C;&#x4E00;&#x500B;&#x5B57;&#x4E32;
    let mut iterator = value.split(&apos;-&apos;);
    let year = iterator.next().ok_or(())?;

    // Step 4 &#x5982;&#x679C;&#x5E74;&#x4EFD;&#x4E0D;&#x662F;&#x56DB;&#x500B;&#x6578;&#x5B57;&#xFF0C;&#x4E14;&#x5F9E;&#x5B57;&#x4E32;&#x8F49;&#x6210;&#x6578;&#x5B57;&#x51FA;&#x932F;&#xFF0C;&#x5C31;&#x56DE;&#x50B3;&#x932F;
    let year_int = year.parse::&lt;u32&gt;().map_err(|_| ())?;
    if year.len() &lt; 4 || year_int == 0 {
        return Err(());
    }

    // Step 5, 6 &#x5982;&#x679C;&#x80FD;&#x89E3;&#x6790;&#x4E0B;&#x500B;&#x5B57;&#x4E32;&#xFF0C;&#x4E14;&#x70BA; W &#x624D;&#x901A;&#x904E;&#x6AA2;&#x67E5;
    let week = iterator.next().ok_or(())?;
    let (week_first, week_last) = week.split_at(1);
    if week_first != &quot;W&quot; {
        return Err(());
    }

    // Step 7 &#x9031;&#x6578;&#x70BA;&#x5169;&#x500B;&#x6578;&#x5B57;
    let week_int = week_last.parse::&lt;u32&gt;().map_err(|_| ())?;
    if week_last.len() != 2 {
        return Err(());
    }

    // Step 8 &#x7576;&#x5E74;&#x6700;&#x5927;&#x9031;&#x6578;
    let max_week = max_week_in_year(year_int);

    // Step 9 &#x9031;&#x6578;&#x5FC5;&#x9808;&#x5728;&#x6700;&#x5927;&#x9031;&#x6578;&#x4EE5;&#x5167;
    if week_int &lt; 1 || week_int &gt; max_week {
        return Err(());
    }

    // Step 10 &#x5982;&#x679C;&#x5B57;&#x4E32;&#x9084;&#x6709;&#x6771;&#x897F;&#xFF0C;&#x90A3;&#x5C31;&#x662F;&#x932F;&#x7684;
    if iterator.next().is_some() {
        return Err(());
    }

    // Step 11 &#x56DE;&#x50B3;&#x89E3;&#x6790;&#x7D50;&#x679C;
    Ok((year_int, week_int))
}
</code></pre>
<hr>
<p>&#x4EE5;&#x4E0A;&#x5C31;&#x662F; value sanitization of input type  &#x7684;&#x793A;&#x7BC4;&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A;&#x700F;&#x89BD;&#x5668;&#x4E2D;&#x6709;&#x5F88;&#x591A;&#x9019;&#x7A2E;&#x5C0F;&#x529F;&#x80FD;&#x5FC5;&#x9808;&#x5BE6;&#x4F5C;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6211;&#x4E00;&#x958B;&#x59CB;&#x8209;&#x4F8B;&#x7684;&#x5C0F;&#x96F6;&#x4EF6;&#xFF0C;&#x6BCF;&#x500B;&#x87BA;&#x7D72;&#x90FD;&#x5F88;&#x91CD;&#x8981;&#xFF0C;&#x624D;&#x80FD;&#x5B8C;&#x6210;&#x6211;&#x5011;&#x6700;&#x68D2;&#x7684;&#x700F;&#x89BD;&#x5668;&#xFF01;</p>
<p>&#x5E0C;&#x671B;&#x6709;&#x5E6B;&#x5230;&#x5927;&#x5BB6;&#xFF0C;&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
