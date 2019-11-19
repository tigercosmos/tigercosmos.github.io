---
title: 站在巨人的肩膀上，一覽瀏覽器引擎研究
date: 2017-12-20 22:08:08
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
<h2>&#x700F;&#x89BD;&#x5668;&#x76F8;&#x95DC;&#x7814;&#x7A76;</h2>
<p>&#x4ECA;&#x5929;&#x4F86;&#x8AC7;&#x8AC7;&#x700F;&#x89BD;&#x5668;&#x7684;&#x5B78;&#x8853;&#x7814;&#x7A76;&#xFF0C;&#x63D0;&#x4F9B;&#x5927;&#x5BB6;&#x4E00;&#x4E9B;&#x8AD6;&#x6587;&#x53C3;&#x8003;&#x3002;</p>
<pre><code>&#x300C;
    &#x5982;&#x679C;&#x8AAA;&#x6211;&#x80FD;&#x770B;&#x7684;&#x66F4;&#x9060;&#x4E00;&#x4E9B;&#xFF0C;&#x90A3;&#x662F;&#x56E0;&#x70BA;&#x6211;&#x7AD9;&#x5728;&#x5DE8;&#x4EBA;&#x7684;&#x80A9;&#x8180;&#x4E0A;&#x3002;
                                                    &#x300D; -- &#x725B;&#x9813;
</code></pre>
<p>&#x79D1;&#x6280;&#x7684;&#x65E5;&#x65B0;&#x6708;&#x7570;&#xFF0C;&#x662F;&#x7531;&#x7121;&#x6578;&#x4EBA;&#x5171;&#x540C;&#x52AA;&#x529B;&#x7684;&#x5FC3;&#x8840;&#xFF0C;&#x6211;&#x5011;&#x73FE;&#x5728;&#x4EAB;&#x53D7;&#x65B9;&#x4FBF;&#x7684;&#x8CC7;&#x8A0A;&#x670D;&#x52D9;&#xFF0C;&#x90FD;&#x662F;&#x7531;&#x524D;&#x4EBA;&#x4E00;&#x9EDE;&#x4E00;&#x6EF4;&#x7814;&#x7A76;&#x51FA;&#x4F86;&#xFF0C;&#x518D;&#x7531;&#x66F4;&#x591A;&#x4EBA;&#x5C07;&#x7814;&#x7A76;&#x518D;&#x7814;&#x7A76;&#xFF0C;&#x624D;&#x9054;&#x5230;&#x81F3;&#x4ECA;&#x6211;&#x5011;&#x6240;&#x770B;&#x5230;&#x7684;&#x9802;&#x5C16;&#x6280;&#x8853;&#x3002;</p>
<p>&#x700F;&#x89BD;&#x5668;&#x5982;&#x4F55;&#x4E0D;&#x662F;&#x5982;&#x6B64;&#xFF0C;&#x5F9E; IE&#x3001;Chrome&#x3001;Firefox &#x7B49;&#x7B49;&#x700F;&#x89BD;&#x5668;&#x4E2D;&#x6211;&#x5011;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x4E0D;&#x65B7;&#x9032;&#x6B65;&#x7684;&#x8173;&#x5370;&#xFF0C;&#x81F3;&#x4ECA; Firefox &#x63A8;&#x51FA;&#x300C;Firefox Quantum&#x300D;&#x6311;&#x6230;&#x7FA4;&#x96C4;&#x518D;&#x6230;&#x6700;&#x9AD8;&#x9EDE;&#xFF0C;&#x80CC;&#x5F8C;&#x5C31;&#x662F;&#x7531;&#x4E00;&#x5806;&#x7814;&#x7A76;&#x4EBA;&#x54E1;&#x4E0D;&#x65B7;&#x5C0B;&#x627E;&#x65B0;&#x7684;&#x65B9;&#x6CD5;&#x3001;&#x7406;&#x8AD6;&#x3001;&#x6280;&#x8853;&#x4F86;&#x7A81;&#x7834;&#x73FE;&#x72C0;&#x3002;Chrome &#x7684;&#x958B;&#x767C;&#x4EBA;&#x54E1;&#x7D55;&#x5C0D;&#x4E0D;&#x6703;&#x5750;&#x4EE5;&#x5F85;&#x6583;&#xFF0C;&#x4E0D;&#x4E45;&#x4E00;&#x5B9A;&#x6703;&#x63A8;&#x51FA;&#x80FD;&#x64E0;&#x4E0B; Firefox &#x7684;&#x65B0;&#x7248;&#x672C;&#xFF0C;&#x800C;&#x6211;&#x5011;&#x5247;&#x662F;&#x5728;&#x9019;&#x826F;&#x6027;&#x7AF6;&#x722D;&#x4E0B;&#x7684;&#x6700;&#x5927;&#x53D7;&#x76CA;&#x8005;&#x3002;&#x700F;&#x89BD;&#x7DB2;&#x7AD9;&#x98C6;&#x9AD8;&#x901F;&#xFF0C;&#x5C31;&#x50CF;&#x662F;&#x958B;&#x8CFD;&#x8ECA;&#x4E00;&#x6A23;&#x723D;&#xFF01;</p>
<p>&#x6709;&#x95DC;&#x65BC;&#x700F;&#x89BD;&#x5668;&#x7684;&#x76F8;&#x95DC;&#x7814;&#x7A76;&#x771F;&#x7684;&#x5F88;&#x5C11;&#xFF0C;&#x4E00;&#x822C;&#x767C; paper &#x90FD;&#x662F;&#x5927;&#x5B78;&#x3001;&#x7814;&#x7A76;&#x55AE;&#x4F4D;&#xFF0C;&#x4F46;&#x9019;&#x4E9B;&#x5730;&#x65B9;&#x5E7E;&#x4E4E;&#x6C92;&#x4EBA;&#x505A;&#x9019;&#x65B9;&#x9762;&#x7814;&#x7A76;&#x3002;&#x50CF;&#x6211;&#x60F3;&#x5728;&#x53F0;&#x5927;&#x627E;&#x6559;&#x6388;&#x7814;&#x7A76;&#x700F;&#x89BD;&#x5668;&#xFF0C;&#x770B;&#x4E86;&#x4E00;&#x4E0B;&#x8CC7;&#x5DE5;&#x7CFB;&#x7684;&#x6559;&#x6388;&#x80CC;&#x666F;&#xFF0C;&#x9802;&#x591A;&#x300C;&#x8EDF;&#x9AD4;&#x67B6;&#x69CB;&#x8A2D;&#x8A08;&#x300D;&#x9019;&#x500B;&#x7814;&#x7A76;&#x9818;&#x57DF;&#x6BD4;&#x8F03;&#x63A5;&#x8FD1;&#x4E00;&#x9EDE;&#x4E86;&#x3002;&#x700F;&#x89BD;&#x5668;&#x7814;&#x7A76;&#x5B8C;&#x5168;&#x4E0D;&#x662F;&#x986F;&#x5B78;&#xFF0C;&#x6A5F;&#x5668;&#x5B78;&#x7FD2;&#x3001;&#x8996;&#x89BA;&#x8FA8;&#x8B58;&#x9019;&#x65B9;&#x9762;&#x53CD;&#x800C;&#x4E00;&#x5806;&#x3002;&#x591A;&#x6578;&#x7684;&#x6280;&#x8853;&#x90FD;&#x662F;&#x7531;&#x700F;&#x89BD;&#x5668;&#x7684;&#x958B;&#x767C;&#x4EBA;&#x54E1;&#x81EA;&#x5DF1;&#x8A2D;&#x8A08;&#x51FA;&#x4F86;&#xFF0C;&#x537B;&#x4E5F;&#x4E0D;&#x6703;&#x53BB;&#x767C; paper&#x3002;&#x6211;&#x81EA;&#x5DF1;&#x8A8D;&#x70BA;&#x6BD4;&#x8F03;&#x53EF;&#x60DC;&#xFF0C;&#x96D6;&#x7136;&#x73FE;&#x5728;&#x90FD;&#x958B;&#x6E90;&#x4E86;&#xFF0C;&#x4F46;&#x5982;&#x679C;&#x6C92;&#x6709;&#x6587;&#x7AE0;&#x7279;&#x5225;&#x53BB;&#x89E3;&#x91CB;&#x6280;&#x8853;&#xFF0C;&#x6050;&#x6015;&#x5225;&#x4EBA;&#x4E5F;&#x5F88;&#x96E3;&#x53BB;&#x5B78;&#x7FD2;&#x3002;</p>
<h2>&#x700F;&#x89BD;&#x5668;&#x7684;&#x4E26;&#x884C;/&#x5E73;&#x884C;&#x5316;</h2>
<ul>
<li>
<a href="https://raw.githubusercontent.com/larsbergstrom/papers/master/icse16-servo-preprint.pdf" target="_blank">Engineering the Servo Web Browser Engine using Rust</a>
</li>
<li>
<a href="https://arxiv.org/abs/1505.07383" target="_blank">Experience Report: Developing the Servo Web Browser Engine using Rust</a>
</li>
<li>
<a href="https://www.tinmith.net/papers/cascaval-ppopp-2013.pdf" target="_blank">ZOOMM: A Parallel Web Browser Engine for Multicore Mobile Devices</a>
</li>
<li>
<a href="https://www.usenix.org/system/files/conference/hotpar12/hotpar12-final58.pdf" target="_blank">A Case for Parallelizing Web Pages</a>
</li>
<li>
<a href="https://research.microsoft.com/pubs/79655/gazelle.pdf" target="_blank">The Multi-Principal OS Construction of the Gazelle Web Browser</a>
</li>
</ul>
<h2>&#x700F;&#x89BD;&#x5668;&#x5DE5;&#x4F5C;&#x7684;&#x5E73;&#x884C;&#x5316;</h2>
<ul>
<li>
<a href="https://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=7396817" target="_blank">Parallel JavaScript Execution in Web Navigation Sequences</a>
</li>
<li>
<a href="https://dl.acm.org/citation.cfm?id=2555301" target="_blank">HPar: A practical parallel parser for HTML--taming HTML complexities for parallel parsing</a>
</li>
<li>
<a href="https://lmeyerov.github.io/projects/pbrowser/pubfiles/paper.pdf" target="_blank">Fast and Parallel Webpage Layout</a>
</li>
<li>
<a href="https://www.usenix.org/legacy/event/hotpar10/tech/full_papers/Badea.pdf" target="_blank">Towards Parallelizing the Layout Engine of Firefox</a>
</li>
</ul>
<h2>&#x700F;&#x89BD;&#x5668;&#x5DE5;&#x4F5C;&#x7684;&#x5206;&#x6790;&#x8207;&#x5EFA;&#x6A21;</h2>
<ul>
<li>
<a href="https://dl.acm.org/citation.cfm?id=2883014" target="_blank">An In-depth Study of Mobile Browser Performance</a>
</li>
<li>
<a href="https://www.sciencedirect.com/science/article/pii/S2210537916000081" target="_blank">Energy consumption and privacy in mobile Web browsing: Individual issues and connected solutions</a>
</li>
<li>
<a href="https://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=7140678" target="_blank">Concurrency in Mobile Browser Engines</a>
</li>
<li>
<a href="https://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=6327179" target="_blank">Exploiting Webpage Characteristics for Energy-Efficient Mobile Web Browsing</a>
</li>
<li>
<a href="https://www.yuhaozhu.com/pubs/isca14.pdf" target="_blank">WebCore: Architectural Support for Mobile Web Browsing</a>
</li>
<li>
<a href="https://www3.cs.stonybrook.edu/%7Earunab/papers/wprof.pdf" target="_blank">Demystifying Page Load Performance with WProf</a>
</li>
<li>
<a href="https://3nity.io/%7Evj/downloads/publications/zhu10hpca.pdf" target="_blank">High-Performance and Energy-Efficient Mobile Web Browsing on Big/Little Systems</a>
</li>
<li>
<a href="https://delivery.acm.org/10.1145/2530000/2525402/p3-larres.pdf?ip=169.234.217.188&amp;id=2525402&amp;acc=PUBLIC&amp;key=CA367851C7E3CE77%2EE385B6E260950907%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&amp;CFID=804568850&amp;CFTOKEN=79805568&amp;__acm__=1466664534_ac8d7658ff673120270c10e7287b5e46" target="_blank">A study of performance variations in the Mozilla Firefox web browser</a>
</li>
<li>
<a href="https://crypto.stanford.edu/~dabo/pubs/papers/browserpower.pdf" target="_blank">Who killed my battery?: Analyzing Mobile Browser Energy Consumption</a>
</li>
<li>
<a href="https://dl.acm.org/citation.cfm?id=2184508" target="_blank">Why are Web Browers Slow on Smartphones?</a>
</li>
<li>
<a href="https://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=5649419" target="_blank">A Limit Study of JavaScript Parallelism</a>
</li>
</ul>
<h2>&#x6539;&#x5584;&#x700F;&#x89BD;&#x5668;&#x7684;&#x6548;&#x7387;</h2>
<ul>
<li>
<a href="https://web.mit.edu/ravinet/www/polaris_nsdi16.pdf" target="_blank">Polaris: Faster Page Loads Using Fine-grained Dependency Tracking</a>
</li>
<li>
<a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&amp;arnumber=6776557" target="_blank">Energy-Aware Web Browsing on Smartphones</a>
</li>
<li>
<a href="https://delivery.acm.org/10.1145/2570000/2567971/p575-wang.pdf?ip=169.234.217.188&amp;id=2567971&amp;acc=ACTIVE%20SERVICE&amp;key=CA367851C7E3CE77%2EE385B6E260950907%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&amp;CFID=804568850&amp;CFTOKEN=79805568&amp;__acm__=1466664056_0298e63e62dbf74a962413739f521a82" target="_blank">Similarity-based web browser optimization</a>
</li>
<li>
<a href="https://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=6525571&amp;tag=1" target="_blank">Mobile Web Browser Optimizations in the Cloud Era: A Survey</a>
</li>
<li>
<a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&amp;arnumber=6689051" target="_blank">GPU acceleration for the web browser based evolutionary computing system</a>
</li>
<li>
<a href="https://delivery.acm.org/10.1145/1780000/1772741/p491-zhang.pdf?ip=169.234.16.99&amp;id=1772741&amp;acc=ACTIVE%20SERVICE&amp;key=CA367851C7E3CE77%2EE385B6E260950907%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&amp;CFID=773108184&amp;CFTOKEN=96473062&amp;__acm__=1461092571_faf3749e491f2a63796ae5bf811efc79" target="_blank">Smart Caching for Web Browsers</a>
</li>
</ul>
<h2>&#x4E00;&#x4E9B;&#x6587;&#x4EF6;</h2>
<ul>
<li>
<a href="https://www.usenix.org/legacy/event/hotpar10/tech/slides/badea.pdf" target="_blank">Towards parallelizing the layout engine of firefox</a>
</li>
<li>
<a href="https://lmeyerov.github.io/projects/pbrowser/hotpar09/paper.pdf" target="_blank">Parallelizing the web browser</a>
</li>
<li>
<a href="https://lmeyerov.github.io/projects/pbrowser/pubfiles/login.pdf" target="_blank">Rethinking Browser Performance</a>
</li>
<li>
<a href="https://parlab.eecs.berkeley.edu/sites/all/parlab/files/playout.pdf" target="_blank">Parallel Webpage Layout</a>
</li>
</ul>
<hr>
<p>&#x4EE5;&#x4E0A;&#x7684;&#x8CC7;&#x6599;&#x5F88;&#x591A;&#xFF0C;&#x5168;&#x90E8;&#x90FD;&#x770B;&#x8981;&#x82B1;&#x4E0D;&#x5C11;&#x6642;&#x9593;&#xFF0C;&#x4F46;&#x4E5F;&#x4EE3;&#x8868;&#x7DB2;&#x8DEF;&#x7684;&#x4E16;&#x754C;&#x5F88;&#x5BEC;&#x95CA;&#x3002;<br>
&#x5982;&#x679C;&#x4F60;&#x770B;&#x5B8C;&#x6709;&#x5FC3;&#x5F97;&#x6B61;&#x8FCE;&#x8207;&#x6211;&#x5206;&#x4EAB;&#xFF01;<br>
&#x66F4;&#x6B61;&#x8FCE;&#x4F60;&#x4E00;&#x8D77;&#x6295;&#x5165;&#x700F;&#x89BD;&#x5668;&#x7684;&#x7814;&#x7A76;&#xFF01;</p>
<p>&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x6211;&#x5011;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
