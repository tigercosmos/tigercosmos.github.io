---
title: Mozilla / Servo 瀏覽器引擎開發環境架設
date: 2017-12-19 21:45:06
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x9023;&#x7E8C;&#x597D;&#x5E7E;&#x5929;&#x6BD4;&#x8F03;&#x786C;&#x7684;&#x89E3;&#x8AAA;&#x6587;&#x7AE0;&#xFF0C;&#x4ECA;&#x5929;&#x63D2;&#x5165;&#x4E00;&#x7BC7;&#x6BD4;&#x8F03;&#x8F15;&#x9B06;&#x7684;&#x6587;&#x7AE0;&#x3002;&#x96D6;&#x7136;&#x662F;&#x4ECB;&#x7D39; Servo&#xFF0C;&#x5176;&#x5BE6;&#x672C;&#x7BC7;&#x4E5F;&#x53EF;&#x4EE5;&#x7576;&#x4F5C; Rust &#x7684;&#x74B0;&#x5883;&#x67B6;&#x8A2D;&#xFF0C;&#x56E0;&#x70BA;&#x4F7F;&#x7528; Rust &#x7B2C;&#x4E00;&#x540D;&#x7684;&#x5C08;&#x6848;&#x662F; Servo&#xFF0C;&#x4F60;&#x8AAA;&#x5462;&#xFF1F;&#xFF38;&#xFF24;</p>
<h2>Servo</h2>
<blockquote>
<p>&#x6B64;&#x5C08;&#x6848;&#x7531; Mozilla &#x8D0A;&#x52A9;&#xFF0C;&#x4E26;&#x4EE5;&#x5168;&#x65B0;&#x7684;&#x7CFB;&#x7D71;&#x7D1A;&#x7A0B;&#x5F0F;&#x8A9E;&#x8A00; Rust &#x7DE8;&#x5BEB;&#xFF0C;Servo &#x5C08;&#x6848;&#x65E8;&#x5728;&#x5BE6;&#x73FE;&#x66F4;&#x597D;&#x7684;&#x5E73;&#x884C;&#x5316;&#x3001;&#x5B89;&#x5168;&#x6027;&#x3001;&#x6A21;&#x7D44;&#x5316;&#x4EE5;&#x53CA;&#x9AD8;&#x6548;&#x80FD;&#x3002;</p>
</blockquote>
<p>&#x60F3;&#x4E86;&#x89E3;&#x66F4;&#x591A;&#x53EF;&#x4EE5;&#x9032;<a href="https://servo.org/zh-TW/index.html" target="_blank">&#x5B98;&#x7DB2;</a>&#x770B;&#xFF0C;&#x958B;&#x73A9;&#x7B11;&#x7684; 030 &#xFF0C;&#x60F3;&#x5F9E;&#x5B98;&#x7DB2;&#x4E86;&#x89E3;&#x9084;&#x4E0D;&#x5982;&#x8A02;&#x95B1;&#x6211;&#x7684;&#x6587;&#x7AE0; XD &#x6211;&#x662F;&#x8AAA;&#x771F;&#x7684;&#xFF0C;&#x5B98;&#x7DB2;&#x771F;&#x7684;&#x6C92;&#x5565;&#x5167;&#x5BB9;&#xFF0C;&#x4E0D;&#x904E;&#x9084;&#x662F;&#x8981;&#x63A8;&#x92B7;&#x4E00;&#x4E0B;&#xFF0C;&#x56E0;&#x70BA;&#x662F;&#x6211;&#x7FFB;&#x8B6F;&#x7684;&#x5594;&#xFF01;</p>
<p>Servo &#x8A73;&#x7D30;&#x5728;&#x5E79;&#x561B;&#xFF0C;&#x6280;&#x8853;&#x7D30;&#x7BC0;&#x3001;&#x7A81;&#x7834;&#x7559;&#x5230;&#x4EE5;&#x5F8C;&#x7684;&#x6587;&#x7AE0;&#x518D;&#x8AAA;&#x3002; &#x6C6A;&#xFF01;&#x6C6A;&#xFF01;</p>
<p><img src="https://download.servo.org/doge-tiny.png" alt="servo"></p>
<h2>Rust</h2>
<p>&#x56E0;&#x70BA; Servo &#x5E7E;&#x4E4E;&#x90FD;&#x662F;&#x7528; Rust &#x5BEB;&#x7684;&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x5F88;&#x5927;&#x90E8;&#x5206;&#x5728;&#x8A2D;&#x5B9A;&#x8A9E;&#x8A00;&#x7684;&#x74B0;&#x5883;&#x3002;</p>
<blockquote>
<p>Rust&#x662F;&#x4E00;&#x500B;&#x7531; Mozilla &#x4E3B;&#x5C0E;&#x958B;&#x767C;&#x7684;&#x901A;&#x7528;&#x3001;&#x7DE8;&#x8B6F;&#x578B;&#x7A0B;&#x5F0F;&#x8A9E;&#x8A00;&#x3002;&#x5B83;&#x7684;&#x8A2D;&#x8A08;&#x6E96;&#x5247;&#x70BA;&#x300C;&#x5B89;&#x5168;&#xFF0C;&#x4E26;&#x884C;&#xFF0C;&#x5BE6;&#x7528;&#x300D;&#x652F;&#x63F4;&#x51FD;&#x6578;&#x5F0F;&#x3001;&#x5E73;&#x884C;&#x5316;&#x3001;&#x7A0B;&#x5E8F;&#x5F0F;&#x4EE5;&#x53CA;&#x7269;&#x4EF6;&#x5C0E;&#x5411;&#x7684;&#x7A0B;&#x5F0F;&#x8A2D;&#x8A08;&#x98A8;&#x683C;&#x3002;</p>
</blockquote>
<h2>Envornment</h2>
<p>&#x5B89;&#x88DD; <a href="https://github.com/servo/servo" target="_blank">Servo</a> &#x7684;&#x74B0;&#x5883;&#x53C3;&#x8003; <code>README</code> &#x505A;&#x5C31;&#x597D;&#xFF0C;&#x56E0;&#x70BA;&#x5404;&#x7CFB;&#x7D71;&#x505A;&#x6CD5;&#x5DEE;&#x7570;&#x5F88;&#x5927;&#xFF0C;&#x76F4;&#x63A5;&#x7167;&#x6587;&#x4EF6;&#x505A;&#x6700;&#x5FEB;&#x3002;&#x4E0D;&#x904E;&#x9019;&#x908A;&#x9084;&#x662F;&#x8CBC;&#x4E0A; macOS, Ubuntu, Windows &#x7684;&#x505A;&#x6CD5;&#x3002;</p>
<h3>&#x53D6;&#x5F97; Servo</h3>
<pre><code>git clone https://github.com/servo/servo
cd servo
</code></pre>
<h3>macOS</h3>
<p>&#x9996;&#x5148;&#x4F60;&#x8981;&#x6709; <code>brew</code>&#xFF0C;&#x53EF;&#x4EE5;&#x900F;&#x904E; App Store &#x4E0B;&#x8F09; XCode&#xFF0C;&#x5C31;&#x6703;&#x9806;&#x4FBF;&#x4E00;&#x8D77;&#x88DD;&#x4E86;</p>
<pre><code>brew install automake pkg-config python cmake yasm
pip install virtualenv
brew install openssl
export OPENSSL_INCLUDE_DIR=&quot;$(brew --prefix openssl)/include&quot;
export OPENSSL_LIB_DIR=&quot;$(brew --prefix openssl)/lib&quot;
</code></pre>
<pre><code>./mach build -d
</code></pre>
<h3>Ubuntu</h3>
<pre><code class="language-sh">sudo apt install git curl freeglut3-dev autoconf libx11-dev \
    libfreetype6-dev libgl1-mesa-dri libglib2.0-dev xorg-dev \
    gperf g++ build-essential cmake virtualenv python-pip \
    libssl1.0-dev libbz2-dev libosmesa6-dev libxmu6 libxmu-dev \
    libglu1-mesa-dev libgles2-mesa-dev libegl1-mesa-dev \
    pulseaudio dbus-x11 libavcodec-dev libavformat-dev \
    libavutil-dev libswresample-dev  libswscale-dev libdbus-1-dev \
    libpulse-dev clang
</code></pre>
<pre><code>./mach build -d
</code></pre>
<h3>Windows</h3>
<p>&#x539F;&#x672C;&#x6587;&#x4EF6;&#x662F;&#x5BEB;&#x88DD; VS2017&#xFF0C;&#x9019;&#x908A;&#x6211;&#x5EFA;&#x8B70;&#x88DD; <a href="https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=BuildTools&amp;rel=15" target="_blank">VS2017 build tool</a> &#x5C31;&#x597D;&#x3002;&#x9019;&#x662F;&#x6211;&#x82B1;&#x5F88;&#x591A;&#x6642;&#x9593;&#x5F97;&#x51FA;&#x7684;&#x5FC3;&#x5F97;&#xFF0C;&#x5B98;&#x65B9;&#x6587;&#x4EF6;&#x7684;&#x9019;&#x500B;&#x65B9;&#x6848;&#x4E5F;&#x662F;&#x6211;&#x6539;&#x7684;&#x3002;&#x4E0D;&#x904E;&#x5F8C;&#x4F86;&#x6211;&#x90FD;&#x4E0D;&#x7528; Windows &#x958B;&#x767C;&#x4E86;&#x3002;</p>
<ol>
<li>&#x4E0B;&#x8F09;&#x5B89;&#x88DD; Build Tools for Visual Studio 2017</li>
<li>&#x5B89;&#x88DD; python2.7 x86-x64 and <code>pip install virtualenv</code>
</li>
<li>
<code>Run mach.bat build -d</code> &#x5C31;&#x53EF;&#x4EE5;&#x7DE8;&#x8B6F;&#x4E86;</li>
</ol>
<h2>Rust</h2>
<h3>Rust</h3>
<ol>
<li>&#x7528; <code>rustup</code> &#x5DE5;&#x5177;&#x4E0B;&#x8F09;&#x5B89;&#x88DD;&#x6700;&#x5FEB;&#xFF0C;&#x7B49;&#x540C; <code>nvm</code> &#x5B89;&#x88DD; <code>node</code>
<pre><code class="language-sh">`curl https://sh.rustup.rs -sSf | sh`
</code></pre>
</li>
<li>
<code>rustup</code> &#x4F86;&#x5B89;&#x88DD; <code>rust</code> <code>2.1.1</code> &#x7248;&#x672C;
<pre><code class="language-sh">rustup install 2.1.1
</code></pre>
</li>
</ol>
<h3>IDE</h3>
<ul>
<li>&#x4E0B;&#x8F09; <a href="code.visualstudio.com" target="_blank">VSCode</a>&#xFF0C;&#x4F60;&#x7576;&#x7136;&#x53EF;&#x4EE5;&#x7528; Vim&#xFF0C;&#x4F46;&#x4EE5;&#x4E0B;&#x7684;&#x529F;&#x80FD;&#x5C31;&#x901A;&#x901A;&#x4E0D;&#x80FD;&#x7528;</li>
<li>&#x5728;&#x5916;&#x639B;&#x4E2D;&#x5B89;&#x88DD; Rusty Code</li>
</ul>
<p><code>cargo</code> &#x662F; <code>rust</code> &#x7684;&#x5957;&#x4EF6;&#x7BA1;&#x7406;&#x5668;&#xFF0C;&#x9019;&#x908A;&#x6211;&#x5011;&#x8981;&#x5B89;&#x88DD; <code>racer</code> &#x624D;&#x80FD;&#x81EA;&#x52D5;&#x63D0;&#x4F9B;&#x8A9E;&#x6CD5;&#x5EFA;&#x8B70;</p>
<ul>
<li>
<code>cargo install racer</code><br>
&#x5B89;&#x88DD; <code>rustfmt</code> &#x662F;&#x81EA;&#x52D5;&#x5C0D;&#x9F4A;&#x7A0B;&#x5F0F;&#x78BC;&#x7684;&#x5DE5;&#x5177;&#xFF0C;&#x8B93;&#x4E4B;&#x5F8C; VScode &#x652F;&#x63F4;&#x300C;&#x81EA;&#x52D5;&#x5C0D;&#x9F4A;&#x300D;&#x52D5;&#x4F5C;</li>
<li>
<code>cargo install rustfmt</code>
</li>
</ul>
<p>&#x70BA;&#x4E86;&#x8B93; <code>racer</code> &#x53EF;&#x4EE5;&#x6B63;&#x5E38;&#x57F7;&#x884C;&#xFF0C;&#x6211;&#x5011;&#x8981;&#x53D6;&#x5F97; <code>Rust</code> &#x7684; repo&#xFF0C;&#x6211;&#x5011;&#x628A;&#x5B83;&#x653E;&#x5728; home</p>
<pre><code>cd ~
git clone https://github.com/rust-lang/rust.git
</code></pre>
<p>&#x63A5;&#x8005;&#x66F4;&#x6539; VSCode &#x7684; <code>setting.json</code>&#xFF0C;&#x5DE6;&#x4E0B;&#x89D2;&#x6709;&#x500B;&#x9F52;&#x8F2A;&#xFF0C;&#x9EDE;&#x64CA;&#x5C31;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x3002;&#x52A0;&#x5165;&#x9019;&#x5169;&#x884C;&#x3002;</p>
<pre><code>{
  &quot;rust.rustLangSrcPath&quot;: &quot;/Users/XXXX/home/rust/src&quot;,
  &quot;rust.formatOnSave&quot;: true
}
</code></pre>
<ul>
<li>&#x6700;&#x5F8C;&#x5728; VSCode &#x5916;&#x639B;&#x4E0B;&#x8F09; TOML extension&#xFF0C;&#x8B93;&#x4ED6;&#x53EF;&#x4EE5;&#x652F;&#x63F4; <code>.toml</code> &#x6A94;&#x6848;&#x3002;&#x9019;&#x76F8;&#x7576;&#x65BC; node &#x4E2D; <code>json</code> &#x7684;&#x529F;&#x80FD;&#x3002;</li>
</ul>
<hr>
<p>&#x63A5;&#x8457;&#x4F60;&#x5C31;&#x53EF;&#x4EE5;&#x4EAB;&#x53D7; rust &#x7684; IDE &#x74B0;&#x5883;&#x56C9;&#xFF01;&#x958B;&#x767C; Servo &#x4E5F;&#x8B8A;&#x66F4;&#x52A0;&#x8F15;&#x9B06;&#xFF0C;&#x4E8B;&#x5BE6;&#x4E0A;&#x56E0;&#x70BA; Servo &#x6A94;&#x6848;&#x5DF2;&#x7D93;&#x975E;&#x5E38;&#x591A;&#xFF0C;&#x4E0D;&#x4F7F;&#x7528;&#x667A;&#x6167;&#x9023;&#x7D50;&#x7684;&#x529F;&#x80FD;&#x627E;&#x51FD;&#x6578;&#x5B9A;&#x7FA9;&#x6703;&#x627E;&#x5230;&#x6B7B;&#xFF0C;&#x6B64;&#x5916;&#x8A9E;&#x6CD5;&#x652F;&#x63F4;&#x5C0D;&#x958B;&#x767C;&#x4F86;&#x8AAA;&#x53EA;&#x6703;&#x66F4;&#x65B9;&#x4FBF;&#x3002;</p>
<p>&#x5E0C;&#x671B;&#x5C0D;&#x5927;&#x5BB6;&#x6709;&#x5E6B;&#x52A9;&#xFF0C;&#x5927;&#x5BB6;&#x660E;&#x5929;&#x898B;&#xFF01;</p>
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
                
