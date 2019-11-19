---
title: 為什麼手機上網速度比較慢呢？
date: 2017-12-29 23:25:55
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
<h2>&#x554F;&#x984C;&#xFF1A;&#x70BA;&#x4EC0;&#x9EBC;&#x624B;&#x6A5F;&#x4E0A;&#x7DB2;&#x901F;&#x5EA6;&#x6BD4;&#x8F03;&#x6162;&#xFF1F;</h2>
<p>&#x4ECA;&#x5929;&#x4F86;&#x9EDE;&#x8F15;&#x9B06;&#x7684;&#x4E3B;&#x984C;&#x3002;<br>
&#x4F60;&#x6709;&#x6C92;&#x6709;&#x60F3;&#x904E;&#xFF0C;&#x70BA;&#x4EC0;&#x9EBC;&#x624B;&#x6A5F;&#x4E0A;&#x7DB2;&#x901F;&#x5EA6;&#x6BD4;&#x8F03;&#x6162;&#xFF1F;</p>
<ol>
<li>&#x624B;&#x6A5F;&#x8655;&#x7406;&#x5668;&#x4E0D;&#x5920;&#x5F37;</li>
<li>&#x624B;&#x6A5F;&#x8A18;&#x61B6;&#x9AD4;&#x4E0D;&#x5920;&#x5927;</li>
<li>&#x7DB2;&#x8DEF;&#x901F;&#x5EA6;&#x5F71;&#x97FF;&#x7684;</li>
</ol>
<p>&#x767E;&#x842C;&#x5C0F;&#x5B78;&#x5802;&#xFF0C;&#x8ACB;&#x56DE;&#x7B54;&#xFF01;</p>
<hr>
<p>&#x9019;&#x554F;&#x984C;&#x771F;&#x7684;&#x6EFF;&#x6709;&#x8DA3;&#x7684;&#xFF0C;&#x7D66;&#x6211;&#x56DE;&#x7B54;&#x7684;&#x8A71;&#x6211;&#x6703;&#x56DE;&#x7B54; 1&#xFF0C;&#x76F4;&#x89BA;&#x544A;&#x8A34;&#x6211;&#x8655;&#x7406;&#x5668;&#x8D8A;&#x5F37;&#x958B;&#x7DB2;&#x9801;&#x8D8A;&#x5FEB;&#x3002;&#x53EF;&#x60DC;&#x76F4;&#x89BA;&#x662F;&#x932F;&#x7684;&#x3002;<br>
&#x95DC;&#x65BC;&#x9019;&#x500B;&#x554F;&#x984C;&#x5C31;&#x6709;&#x4E00;&#x7BC7; Paper(<a href="https://www.ruf.rice.edu/~mobile/publications/wang11hotmobile.pdf" target="_blank">Why are Web BrowsersSlowon Smartphones?</a>)&#x5728;&#x8A0E;&#x8AD6;&#x3002;&#x672C;&#x7BC7;&#x622A;&#x53D6;&#x91CD;&#x9EDE;&#x544A;&#x8A34;&#x5927;&#x5BB6;&#x9019;&#x984C;&#x7684;&#x7B54;&#x6848;&#x3002;</p>
<hr>
<h2>&#x89E3;&#x7B54;</h2>
<p>&#x9996;&#x5148;&#x4F86;&#x770B;&#x5716;&#x4E00;<br>
<img src="https://user-images.githubusercontent.com/18013815/34439654-6622f5a2-ecea-11e7-9255-b948aea96581.png" alt></p>
<p>IR(Internal representation) &#x4EE3;&#x8868; build &#x7684;&#x904E;&#x7A0B;&#xFF0C;&#x5148;&#x524D;&#x63D0;&#x5230;&#x904E;&#x89E3;&#x6790;&#x6E32;&#x67D3;&#x7684;&#x904E;&#x7A0B;&#x3002;&#x6B64;&#x5916;&#x904E;&#x7A0B;&#x4E2D;&#x6703;&#x7531; <code>index.html</code> &#x5EF6;&#x4F38;&#x628A;&#x6240;&#x6709;&#x8981;&#x7684;&#x8CC7;&#x6599;&#x90FD;&#x6293;&#x56DE;&#x4F86;&#x3002;<br>
&#x9019;&#x908A;&#x986F;&#x793A;&#x7684;&#x662F;&#x7C21;&#x6613;&#x7684;&#x7DB2;&#x9801;&#x8655;&#x7406;&#x6D41;&#x7A0B;&#xFF0C;&#x6211;&#x5011;&#x4E5F;&#x770B;&#x904E;&#x4E0D;&#x5C11;&#x6B21;&#x4E86;&#x3002;</p>
<hr>
<p>&#x518D;&#x4F86;&#x770B;&#x5716;&#x4E09;<br>
<img src="https://user-images.githubusercontent.com/18013815/34439739-08630a8c-eceb-11e7-9354-3b05259528a4.png" alt><br>
&#x9019;&#x5F35;&#x5716;&#x986F;&#x793A;&#x4E00;&#x822C;&#x624B;&#x6A5F;&#x8F09;&#x5165;&#x7DB2;&#x9801;&#x6BCF;&#x500B;&#x6B65;&#x9A5F;&#x6240;&#x9700;&#x7684;&#x6642;&#x9593;&#x3002;&#x9019;&#x908A;&#x6CE8;&#x610F;&#x5230; inter-group dependency &#x6240;&#x82B1;&#x7684;&#x6642;&#x9593;&#x6709;&#x9EDE;&#x9577;&#x3002;</p>
<hr>
<p>&#x5716;&#x56DB;&#x986F;&#x793A;&#x9023;&#x63A5;&#x4E0D;&#x540C;&#x7DB2;&#x8DEF;&#xFF0C;&#x6240;&#x5E36;&#x4F86;&#x7684;&#x5DEE;&#x7570;<br>
<img src="https://user-images.githubusercontent.com/18013815/34439787-7060d574-eceb-11e7-98cd-0ee3a6270d09.png" alt><br>
&#x4E59;&#x592A;&#x7DB2;&#x8DEF;&#x9019;&#x908A;&#x4E0B;&#x8F09;&#x901F;&#x5EA6;&#x662F; 1GB&#xFF0C; 3G &#x7DB2;&#x8DEF;&#x4E0B;&#x8F09;&#x901F;&#x5EA6;&#x5927;&#x7D04; 40 MB&#xFF0C;Adverse &#x8A2D;&#x5B9A;&#x60C5;&#x6CC1;&#x70BA;&#x6A94;&#x6848;&#x9023;&#x7D50;&#x82B1; 400 ms &#x4E0B;&#x8F09;&#x901F;&#x5EA6; 500 KB&#x3002;<br>
N1&#x3001;G1 &#x500B;&#x4EE3;&#x8868;&#x4E0D;&#x540C;&#x6B3E;&#x624B;&#x6A5F;&#xFF0C;&#x9019;&#x908A;&#x53EF;&#x4EE5;&#x4E0D;&#x7528;&#x7BA1;&#xFF0C;&#x4E3B;&#x8981;&#x662F;&#x770B;&#x7DB2;&#x8DEF;&#x9020;&#x6210;&#x5DEE;&#x7570;&#xFF0C;&#x767C;&#x73FE;&#x90FD;&#x662F;&#x8D85;&#x597D;&#x5E7E;&#x79D2;&#xFF0C;&#x76F8;&#x7576;&#x65BC; 20&#x3001;30%</p>
<hr>
<p>&#x518D;&#x4F86;&#x770B;&#x5982;&#x679C;&#x5C07;&#x8A08;&#x7B97;&#x6548;&#x80FD;&#x52A0;&#x5FEB;&#x6703;&#x600E;&#x9EBC;&#x6A23;<br>
<img src="https://user-images.githubusercontent.com/18013815/34439788-72df191e-eceb-11e7-8075-66447d797363.png" alt><br>
&#x9019;&#x908A;&#x5217;&#x51FA;&#x684C;&#x9762;&#x7248;&#x3001;&#x884C;&#x52D5;&#x7248;&#x7DB2;&#x7AD9;&#x7684;&#x6578;&#x64DA;&#xFF0C;&#x4F46;&#x4E0D;&#x8AD6;&#x54EA;&#x4E00;&#x7A2E;&#xFF0C;&#x5728;&#x54EA;&#x4E00;&#x500B;&#x6A21;&#x7D44;&#xFF08;&#x7248;&#x9762;&#x3001;&#x6E32;&#x67D3;&#x3001;style&#xFF09;&#x5C07;&#x4ED6;&#x901F;&#x5EA6;&#x52A0;&#x5230; 32 &#x500D;&#xFF0C;&#x5C0D;&#x6574;&#x9AD4;&#x6642;&#x9593;&#x7684;&#x5F71;&#x97FF;&#x5FAE;&#x4E4E;&#x5176;&#x5FAE;&#xFF0C;&#x6700;&#x591A;&#x5C31; 4&#xFF05;&#x3002;&#x4E8B;&#x5BE6;&#x4E0A;&#xFF0C;&#x624B;&#x6A5F;&#x8A08;&#x7B97;&#x6548;&#x80FD;&#x5DEE;&#x7570;&#x6700;&#x591A;&#x4E5F;&#x624D;2&#x3001;3&#x500D;&#x800C;&#x5DF2;&#x3002;&#x6240;&#x4EE5;&#x9019;&#x908A;&#x8B49;&#x660E; IR &#x5C0D;&#x65BC;&#x7DB2;&#x8DEF;&#x700F;&#x89BD;&#x901F;&#x5EA6;&#x5E7E;&#x4E4E;&#x6C92;&#x5F71;&#x97FF;&#x3002;</p>
<hr>
<p>&#x770B;&#x5230;&#x9019;&#x908A;&#x6709;&#x6C92;&#x6709;&#x6709;&#x9EDE; sense &#x4E86;&#xFF1F;</p>
<p>&#x6700;&#x5F8C;&#x4F86;&#x770B;&#x7DB2;&#x8DEF;&#x983B;&#x5BEC;&#x548C;&#x7DB2;&#x8DEF;&#x4F86;&#x56DE;&#x901A;&#x8A0A;&#x5EF6;&#x9072;(Round-trip time, RTT)&#x7684;&#x5F71;&#x97FF;<br>
<img src="https://user-images.githubusercontent.com/18013815/34440036-6436dd0a-eced-11e7-9c36-b519eb420c80.png" alt><br>
&#x76F4;&#x63A5;&#x767C;&#x73FE; RTT &#x5F71;&#x97FF;&#x6BD4;&#x5BEC;&#x983B;&#x66F4;&#x5927;&#x3002;&#x7B54;&#x6848;&#x547C;&#x4E4B;&#x6B32;&#x51FA;&#x4E86;&#xFF01;</p>
<hr>
<h2>&#x7D50;&#x8AD6;</h2>
<p>&#x5BE6;&#x969B;&#x7814;&#x7A76;&#x767C;&#x73FE;&#xFF0C;&#x5927;&#x591A;&#x6578;&#x6642;&#x9593;&#x90FD;&#x82B1;&#x5728; RTT &#x4E0A;&#x9762;&#x4E86;&#xFF0C;&#x5176;&#x6B21;&#x662F;&#x7DB2;&#x8DEF;&#x901F;&#x5EA6;&#x3002;&#x5176;&#x5BE6;&#x9019;&#x4E5F;&#x6EFF;&#x5408;&#x7406;&#x7684;&#xFF0C;&#x624B;&#x6A5F;&#x662F;&#x9023;&#x57FA;&#x5730;&#x53F0;&#xFF0C;&#x7DB2;&#x8DEF;&#x5EF6;&#x9072;&#x7A0B;&#x5EA6;&#x6BD4;&#x4E59;&#x592A;&#x7DB2;&#x8DEF;&#x56B4;&#x91CD;&#x5F88;&#x6B63;&#x5E38;&#xFF0C;&#x66F4;&#x4E0D;&#x8981;&#x8AAA; 3G&#xFF08;&#x751A;&#x81F3; 4G&#xFF09;&#x5BEC;&#x983B;&#x60F3;&#x8981;&#x8D0F;&#x904E;&#x5149;&#x7E96;&#x7DB2;&#x8DEF;&#x3002;&#x4E26;&#x4E14;&#x7576; RTT &#x8207;&#x7DB2;&#x8DEF;&#x901F;&#x5EA6;&#x5169;&#x8005;&#x52A0;&#x8D77;&#x4F86;&#x6642;&#xFF0C;&#x6548;&#x679C;&#x66F4;&#x660E;&#x986F;&#xFF0C;&#x4F60;&#x6703;&#x6709;&#x300C;&#x611F;&#x89BA;&#x300D;&#x5230;&#x600E;&#x9EBC;&#x597D;&#x300C;&#x5361;&#x300D;&#xFF1F;&#x6240;&#x4EE5;&#xFF0C;&#x5047;&#x8A2D;&#x4F60;&#x60F3;&#x8981;&#x4E0A;&#x7DB2;&#x5FEB;&#x4E00;&#x9EDE;&#xFF0C;&#x5176;&#x5BE6;&#x624B;&#x6A5F;&#x597D;&#x4E0D;&#x597D;&#x95DC;&#x4FC2;&#x5176;&#x5BE6;&#x4E0D;&#x662F;&#x5F88;&#x5927;&#x3002;&#xFF08;&#x4E0D;&#x904E;&#x5982;&#x679C;&#x60F3;&#x8981;&#x73A9; WebVR &#x7684;&#x8A71;&#xFF0C;&#x624B;&#x6A5F;&#x9084;&#x662F;&#x8981;&#x5F88;&#x597D;&#x5566;&#xFF5E;&#xFF09;</p>
<p>&#x4F60;&#x7B54;&#x5C0D;&#x4E86;&#x55CE;&#xFF1F;&#x60F3;&#x7576;&#x5E74;&#x6211;&#x4E5F;&#x6709;&#x770B;&#x767E;&#x842C;&#x5C0F;&#x5B78;&#x5802;&#xFF0C;&#x4E5F;&#x53EA;&#x8A18;&#x5F97;&#x5C0F;&#x897F;&#x74DC;&#x9019;&#x865F;&#x4EBA;&#x7269;&#x800C;&#x5DF2;&#x4E86;&#x3002; Orz</p>
<p>&#x6700;&#x5F8C;&#x9019;&#x7BC7;&#x8AD6;&#x6587;&#x7D50;&#x8AD6;&#x6709;&#x63D0;&#x51FA;&#x4E00;&#x4E9B;&#x89C0;&#x9EDE;&#xFF0C;&#x6211;&#x5C31;&#x4E0D;&#x7FFB;&#x8B6F;&#x4E86;&#xFF0C;&#x9644;&#x7D66;&#x5927;&#x5BB6;&#x53C3;&#x8003;&#xFF1A;</p>
<blockquote>
<p>The loading of multiple resources can be batched in various ways to hide the resource loading time. For example, Google normally batches multiplepictures into one and send itto the browserdirectly. This eliminates  multiple  RTTs needed to get several pictures. Furthermore, the batched loading can be supported by a proxy in the  cloud  in  order to suppress the long  RTT  of the wireless first hop. Finally, it can be supported by new ways of specifying webpage resourcesso that the browser can load  resources as soon as possible, such as Data URI scheme</p>
</blockquote>
<p>&#x5982;&#x679C;&#x9084;&#x6709;&#x8208;&#x8DA3;&#x7684;&#x8A71;&#xFF0C;&#x53EF;&#x4EE5;&#x770B;&#x9019;&#x500B;&#x63D0;&#x554F;&#x7684;<a href="https://serverfault.com/questions/387627/why-do-mobile-networks-have-high-latencies-how-can-they-be-reduced" target="_blank">&#x56DE;&#x7B54;</a>(why-do-mobile-networks-have-high-latencies-how-can-they-be-reduced)</p>
<p>&#x56DE;&#x7B54;&#x4E2D;&#x6709;&#x500B;&#x8868;&#x683C;&#x662F;&#xFF0C;&#x4E00;&#x500B; HTTP &#x8981;&#x6C42;&#x6240;&#x7D93;&#x904E;&#x7684;&#x5404;&#x9805;&#x5EF6;&#x9072;</p>
<table>
<thead>
<tr>
<th>RTT Things</th>
<th>3G</th>
<th>4G</th>
</tr>
</thead>
<tbody>
<tr>
<td>Control plane</td>
<td>200&#x2013;2,500 ms</td>
<td>50&#x2013;100 ms</td>
</tr>
<tr>
<td>DNS lookup</td>
<td>200 ms</td>
<td>100 ms</td>
</tr>
<tr>
<td>TCP handshake</td>
<td>200 ms</td>
<td>100 ms</td>
</tr>
<tr>
<td>TLS handshake</td>
<td>200&#x2013;400 ms</td>
<td>100&#x2013;200 ms</td>
</tr>
<tr>
<td>HTTP request</td>
<td>200 ms</td>
<td>100 ms</td>
</tr>
<tr>
<td>Total latency overhead</td>
<td>200&#x2013;3500 ms</td>
<td>100&#x2013;600 ms</td>
</tr>
</tbody>
</table>
<h2>5G &#x597D;&#x50CF;&#x4E5F;&#x8981;&#x51FA;&#x4F86;&#x4E86;&#x5594;&#xFF01;</h2>
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
                
