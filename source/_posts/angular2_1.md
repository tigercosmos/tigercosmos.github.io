---
title: TypeScript -- Angular 2 的寫作靈魂
date: 2016-12-17 23:47:29
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<p><img src="http://naywinmyint.com/content/images/2016/04/typescript-1.jpg" alt></p>
<h2>&#x524D;&#x8A00;</h2>
<p>&#x9019;&#x7CFB;&#x5217;&#x6A19;&#x984C;&#x4E0D;&#x662F; Angular 2&#x4E4B; 30&#x5929;&#x9081;&#x5411;&#x795E;&#x4E4E;&#x5947;&#x8E5F;&#x4E4B;&#x8DEF;&#x55CE;&#xFF1F;&#x600E;&#x9EBC;&#x624D;&#x7B2C;&#x4E8C;&#x5929;&#x6A19;&#x984C;&#x5C31;&#x662F; TypeScript(&#x4E4B;&#x5F8C;&#x7C21;&#x7A31; TS)&#x4E86;&#x5462;&#xFF1F;&#x600E;&#x9EBC;&#x6709;&#x7A2E;&#x639B;&#x7F8A;&#x982D;&#x8CE3;&#x72D7;&#x8089;&#x7684;&#x611F;&#x89BA;&#x5462;&#xFF1F;XD &#x5148;&#x524D;&#x63D0;&#x5230; Angular 2&#x5F88;&#x91CD;&#x8981;&#x7684;&#x4E00;&#x74B0;&#x4FBF;&#x662F;&#x5B83;&#x63A1;&#x7528; TS&#x7576;&#x4F5C;&#x958B;&#x767C;&#x8A9E;&#x8A00;&#xFF0C;&#x5982;&#x679C; Angular&#x662F;&#x4E00;&#x500B;&#x7DB2;&#x9801;&#x524D;&#x7AEF;&#x7684;&#x7CBE;&#x9748;&#xFF0C;&#x90A3; TS&#x5C31;&#x662F;&#x4ED6;&#x7684;&#x9748;&#x9B42;&#x5566;&#xFF01;<br>
&#x4E8B;&#x5BE6;&#x4E0A;&#x96D6;&#x7136;&#x4F60;&#x4E5F;&#x53EF;&#x4EE5;&#x5B8C;&#x5168;&#x4F7F;&#x7528;&#x7D14; JavaScript(&#x4E4B;&#x5F8C;&#x7C21;&#x7A31;JS)&#x4F86;&#x958B;&#x767C;&#xFF0C;&#x56E0;&#x70BA; TS&#x672C;&#x8EAB;&#x5C31;&#x5B8C;&#x5168;&#x76F8;&#x5BB9; JS&#xFF0C;&#x4F46;&#x8EAB;&#x70BA; Super&#x7248;&#x7684; JS&#xFF0C;&#x5927;&#x5BB6;&#x90FD;&#x5728;&#x7528;&#x4E86;(&#x5C24;&#x5176;&#x8001;&#x5927;&#x54E5;&#x5FAE;&#x8EDF;&#x8DDF; Google)&#xFF0C;&#x5C1A;&#x672A;&#x6210;&#x70BA;&#x795E;&#x4E4E;&#x5176;&#x6280;&#x7684;&#x6211;&#x5011;&#xFF0C;&#x8DDF;&#x8457;&#x5F37;&#x8005;&#x7684;&#x65B9;&#x6CD5;&#x4E00;&#x8D77;&#x4FEE;&#x9053;&#x6E96;&#x6C92;&#x932F;&#x3002;&#x6240;&#x4EE5;&#x9996;&#x5148;&#x6211;&#x5011;&#x8981;&#x5148;&#x628A; TS&#x5F04;&#x6E05;&#x695A;&#xFF0C;&#x4E0D;&#x7BA1;&#x662F;&#x8A9E;&#x6CD5;&#x3001;&#x8B8A;&#x6578;&#x3001;&#x51FD;&#x6578;&#x3001;&#x98A8;&#x683C;&#x7B49;&#x7B49;&#x4E4B;&#x985E;&#x7684;&#xFF0C;&#x90FD;&#x8981;&#x6709;&#x6240;&#x4E86;&#x89E3;&#xFF0C;&#x9019;&#x6A23;&#x5C0D;&#x65BC;&#x4E4B;&#x5F8C;&#x958B;&#x767C; Angular&#x53EA;&#x6703;&#x6709;&#x76CA;&#x7121;&#x5BB3;&#xFF0C;&#x66F4;&#x4F55;&#x6CC1;&#x5B78;&#x7FD2;&#x65B0;&#x7684;&#x4E8B;&#x60C5;&#x662F;&#x591A;&#x9EBC;&#x4EE4;&#x4EBA;&#x958B;&#x5FC3;&#x7684;&#x4E8B;&#x5462;&#xFF01;</p>
<h2>TypeScript</h2>
<p>&#x63A5;&#x8457;&#x5C31;&#x4F86;&#x8A8D;&#x8B58;&#x4E00;&#x4E0B; TS&#x662F;&#x751A;&#x9EBC;&#x5427;&#xFF01;</p>
<h3>&#x7DE3;&#x8D77;</h3>
<p>TS&#x662F;&#x70BA;&#x4E86;&#x89E3;&#x6C7A; JS&#x8AF8;&#x591A;&#x7684;&#x554F;&#x984C;&#xFF0C;&#x4F8B;&#x5982;&#x8CC7;&#x6599;&#x578B;&#x5225;(typing)&#x3001;&#x540D;&#x7A31;&#x7A7A;&#x9593;(namescpace)&#x4EE5;&#x53CA;&#x96F6;&#x788E;&#x7684;&#x7709;&#x7709;&#x89D2;&#x89D2;&#xFF0C;&#x800C;&#x4E14;&#x7531;&#x65BC;&#x7576;&#x521D;&#x8A2D;&#x8A08; JS&#x7684;&#x968E;&#x6BB5;&#x904E;&#x65BC;&#x5009;&#x4FC3;&#xFF0C;&#x52A0;&#x4E0A;&#x6C92;&#x6709;&#x5148;&#x4F8B;&#x53EF;&#x4EE5;&#x53C3;&#x8003;(&#x7B2C;&#x4E00;&#x500B;&#x540C;&#x6642;&#x517C;&#x5177;&#x51FD;&#x6578;&#x7A0B;&#x5F0F;&#x548C;&#x7269;&#x4EF6;&#x5C0E;&#x5411;&#x7A0B;&#x5F0F;&#x7684;&#x8A9E;&#x8A00;)&#xFF0C;&#x7E3D;&#x7E3D;&#x539F;&#x56E0;&#x8B93;&#x5927;&#x5BB6;&#x5C0D; JS&#x4E0D;&#x592A;&#x6EFF;&#x610F;&#xFF0C;&#x65BC;&#x662F;&#x5C31;&#x6709;&#x5F88;&#x591A;&#x6539;&#x5584; JS&#x7684;&#x8A9E;&#x8A00;&#x8A95;&#x751F;&#xFF0C;&#x5B83;&#x5011;&#x90FD;&#x5E0C;&#x671B;&#x6E1B;&#x8F15; JS&#x958B;&#x767C;&#x4EBA;&#x54E1;&#x7684;&#x8CA0;&#x64D4;&#xFF0C;&#x6539;&#x7528;&#x4E00;&#x4E9B;&#x7D50;&#x69CB;&#x826F;&#x597D;&#x6216;&#x662F;&#x66F4;&#x8F15;&#x9B06;&#x7684;&#x8A9E;&#x8A00;&#x4F86;&#x958B;&#x767C;&#x61C9;&#x7528;&#x7A0B;&#x5F0F;(Script#&#x3001;CoffeeScript)&#xFF0C;&#x518D;&#x900F;&#x904E;&#x5404;&#x81EA;&#x7684;&#x7DE8;&#x8B6F;&#x5668;&#x4F86;&#x7522;&#x51FA; JS&#x7A0B;&#x5F0F;&#x78BC;&#xFF0C; TS&#x4E5F;&#x662F;&#x5176;&#x4E2D;&#x4E00;&#x500B;&#x3002;</p>
<h3>&#x8A9E;&#x6CD5;</h3>
<p>&#x63A5;&#x8457;&#x5C31;&#x4F86;&#x5FEB;&#x901F;&#x5165;&#x9580;&#x5427;&#xFF01;&#x8B93;&#x6211;&#x5011;&#x770B;&#x770B; TypeScript&#x6709;&#x90A3;&#x4E9B;&#x7279;&#x6B8A;&#x7684;&#x5730;&#x65B9;&#x3002;</p>
<h4>const &amp; let</h4>
<p>&#x56B4;&#x683C;&#x8AAA;&#x8D77;&#x4F86;&#x9019;&#x4E0D;&#x7B97;&#x662F; TS&#x7279;&#x6B8A;&#x7684;&#x6771;&#x897F;&#xFF0C;&#x5728; ES6&#x4E2D;&#x5C0D;&#x65BC;&#x5BA3;&#x544A;&#x8B8A;&#x6578;&#x5F97;&#x66F4;&#x660E;&#x78BA;&#x898F;&#x7BC4;&#x3002;</p>
<pre><code>const cannotChange = 9; // &#x53EA;&#x8981;&#x6539;&#x8B8A;&#x9019;&#x500B;&#x5E38;&#x6578;&#xFF0C;&#x7A0B;&#x5F0F;&#x6703;&#x51FA;&#x932F;
let canChange = [{&apos;a&apos;: &apos;1&apos;}, {&apos;b&apos;: &apos;2&apos;}]; //&#x5728;&#x4E0D;&#x6539;&#x8B8A;&#x5BA3;&#x544A;&#x7684;&#x8CC7;&#x6599;&#x578B;&#x5225;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x53EF;&#x4EE5;&#x6539;&#x8B8A;&#x9019;&#x500B;&#x53C3;&#x6578;
</code></pre>
<p><code>var</code>&#x96D6;&#x7136;&#x9084;&#x662F;&#x80FD;&#x7528;&#xFF0C;&#x4F46;&#x80FD;&#x4E0D;&#x7528;&#x76E1;&#x91CF;&#x4E0D;&#x8981;&#x7528;&#xFF0C;&#x8D8A;&#x660E;&#x78BA;&#x7684;&#x898F;&#x7BC4;&#x5C0D;&#x7A0B;&#x5F0F;&#x5E6B;&#x52A9;&#x8D8A;&#x597D;&#x3002;</p>
<h4>&#x8CC7;&#x6599;&#x578B;&#x5225;(typing)</h4>
<p>&#x4EE5;&#x5F80;&#x5728; JS &#x5BA3;&#x544A;&#x8B8A;&#x6578;&#x662F;&#x4E0D;&#x9700;&#x8981;&#x5BA3;&#x544A;&#x578B;&#x5225;&#x7684;&#xFF0C;<code>var</code> &#x5C31;&#x662F;&#x842C;&#x80FD;&#xFF0C;&#x7269;&#x4EF6;&#x53EF;&#x4EE5;&#x8B8A;&#x6578;&#x5B57;&#xFF0C;&#x5B57;&#x4E32;&#x53EF;&#x4EE5;&#x8B8A;&#x5E03;&#x6797;&#xFF0C;&#x5728;&#x7D55;&#x5927;&#x591A;&#x6578;&#x7684;&#x60C5;&#x6CC1;&#x4E0B;&#xFF0C;&#x9019;&#x6A23;&#x8B8A;&#x4F86;&#x8B8A;&#x53BB;&#x5176;&#x5BE6;&#x4E0D;&#x597D;&#xFF0C;&#x96D6;&#x7136;&#x8AAA;&#x4E0D;&#x7528;&#x5BA3;&#x544A;&#x578B;&#x5225;&#x5F88;&#x65B9;&#x4FBF;&#xFF0C;&#x4F46;&#x5C31;&#x7B97;&#x518D;&#x7D30;&#x5FC3;&#x9084;&#x662F;&#x6709;&#x51FA;&#x932F;&#x7684;&#x4E00;&#x5929;&#xFF0C;&#x6240;&#x4EE5; TS&#x53C8;&#x5F37;&#x5236;&#x898F;&#x5B9A;&#x8981;&#x5BA3;&#x544A;&#x578B;&#x5225;&#x4E86;&#x3002;<br>
&#x4EE5;&#x4E0B;&#x662F;&#x6240;&#x6709;&#x578B;&#x5225;&#x7BC4;&#x4F8B;&#xFF1A;</p>
<pre><code>//Number 
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;

//Stirng
let person: string = &quot;Mike&quot;; //&#x53EF;&#x4EE5;&#x7528; &quot;&quot;
let age: number = 37;
let sentence: string = `Oh, ${person} is ${age} years old.`; //&#x4E5F;&#x53EF;&#x4EE5;&#x7528; `${}`
//&#x4E0A;&#x9762;&#x7B49;&#x65BC; &quot;Oh, &quot; + person + &quot; is &quot; + age + &quot; years old.&quot;

//Array
let list: number[] = [1, 2, 3];

//Tuple
let x: [string, number]; // Array&#x4E2D;&#x5305;&#x542B;&#x4E0D;&#x540C;&#x578B;&#x5225;&#x7684;&#x8B8A;&#x6578;&#x7528; Tuple
x = [&quot;hello&quot;, 10]; // OK
x = [10, &quot;hello&quot;]; // Error
x[3] = true // Error &#x5F80;&#x5F8C;&#x7684;&#x8B8A;&#x6578;&#x53EA;&#x80FD;&#x662F;&#x4E00;&#x958B;&#x59CB;&#x8A2D;&#x5B9A;&#x7684; string &#x6216; number
</code></pre>
<h4>&#x578B;&#x5225;&#x8A3B;&#x91CB;(Type annotations)</h4>
<p>&#x4EE5;&#x5F80;&#x5728; JS&#x4E2D;&#x51FD;&#x6578;&#x7684;&#x53C3;&#x6578;&#x662F;&#x4E0D;&#x9700;&#x8981;&#x5BA3;&#x544A;&#x53C3;&#x6578;&#x7684;&#x578B;&#x5225;&#x3002;</p>
<h5>JS:</h5>
<pre><code>function greeter(person) {
    return &quot;Hello, &quot; + person;
}
</code></pre>
<p>&#x4F46;&#x662F;&#x9019;&#x6A23;&#x6C92;&#x4EBA;&#x77E5;&#x9053; <code>person</code>&#x662F;&#x751A;&#x9EBC;&#xFF0C;&#x5230;&#x5E95;&#x662F;&#x7269;&#x4EF6;&#x9084;&#x662F;&#x5B57;&#x4E32;&#xFF1F;</p>
<h5>TS:</h5>
<pre><code>function greeter(person: string) {
    return &quot;Hello, &quot; + person;
}
</code></pre>
<p>&#x6240;&#x4EE5; TS&#x5F37;&#x5236;&#x8981;&#x6C42;&#x53C3;&#x6578;&#x8981;&#x8A3B;&#x91CB;&#x578B;&#x5225; <code>person: string</code>&#x9019;&#x6A23;&#x4E00;&#x770B;&#x5C31;&#x77E5;&#x9053;&#x662F;&#x5B57;&#x4E32;&#xFF0C;&#x7576;&#x5C08;&#x6848;&#x8D8A;&#x505A;&#x8D8A;&#x5927;&#xFF0C;&#x51FD;&#x6578;&#x547C;&#x53EB;&#x51FD;&#x6578;&#x53C8;&#x5728;&#x547C;&#x53EB;&#x4E0B;&#x500B;&#x51FD;&#x6578;&#xFF0C;&#x53C3;&#x6578;&#x6EFF;&#x5929;&#x98DB;&#x7684;&#x6642;&#x5019;&#xFF0C;&#x624D;&#x4E0D;&#x6703;&#x641E;&#x932F;&#x8CC7;&#x6599;&#x578B;&#x5225;&#xFF0C;&#x53C8; debug&#x534A;&#x5929;&#x624D;&#x767C;&#x73FE;&#x662F;&#x8CC7;&#x6599;&#x7D66;&#x932F;&#xFF01;<br>
&#x8A3B;&#x91CB;&#x4E5F;&#x53EF;&#x4EE5;&#x653E;&#x5165;&#x6307;&#x5B9A;&#x578B;&#x614B;&#x7684;&#x7269;&#x4EF6;&#xFF0C;&#x5C31;&#x662F;&#x63A5;&#x4E0B;&#x4F86;&#x7684; Interface&#x3002;</p>
<h4>Interfaces</h4>
<p>interface &#x8B93;&#x53C3;&#x6578;&#x70BA;&#x7269;&#x4EF6;&#x6642;&#xFF0C;&#x6709;&#x66F4;&#x660E;&#x78BA;&#x7684;&#x7D50;&#x69CB;&#x578B;&#x614B;&#xFF0C;&#x800C;&#x4E0D;&#x662F;&#x53EA;&#x662F;&#x4E1F;&#x500B;&#x53C3;&#x6578;&#x8868;&#x793A;&#x70BA;&#x4E00;&#x500B;&#x7269;&#x4EF6;&#x3002;<br>
&#x7C21;&#x55AE;&#x7684;&#x7BC4;&#x4F8B;&#x61C9;&#x8A72;&#x53EF;&#x4EE5;&#x8B93;&#x5927;&#x5BB6;&#x61C2; interface &#x7684;&#x6982;&#x5FF5;&#x3002;</p>
<pre><code>interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return &quot;Hello, &quot; + person.firstName + &quot; &quot; + person.lastName;
}

var user = { firstName: &quot;Tiger&quot;, lastName: &quot;Liu&quot; };

console.log(greeter(user));
</code></pre>
<h4>&#x985E;&#x5225;(Classes)</h4>
<p>&#x4EE5;&#x5F80;&#x5728; ES5 &#x7684; JS &#x662F;&#x6C92;&#x8FA6;&#x6CD5;&#x50CF; C++&#x3001;JAVA&#x90A3;&#x6A23;&#x76F4;&#x63A5;&#x5BA3;&#x544A;&#x985E;&#x5225;&#x7684;&#xFF0C;JS&#x958B;&#x767C;&#x8005;&#x7576;&#x7136;&#x9084;&#x662F;&#x80FD;&#x900F;&#x904E;&#x4E00;&#x4E9B;&#x6280;&#x5DE7;&#x9054;&#x5230;&#x985E;&#x4F3C;&#x6548;&#x679C;&#xFF0C;&#x4F46;&#x5C31;&#x6BD4;&#x8F03;&#x9EBB;&#x7169;&#x4E5F;&#x5F88;&#x4E0D;&#x76F4;&#x89C0;&#x3002;&#x800C; ES6 &#x7248;&#x672C;&#x4E4B;&#x5F8C; JS &#x52A0;&#x5165;&#x985E;&#x5225;&#x7684;&#x8A9E;&#x6CD5;&#x7CD6;&#xFF0C;TS &#x4E2D;&#x5C31;&#x80FD;&#x7528;&#x76F8;&#x540C;&#x7684;&#x65B9;&#x5F0F;&#x5BA3;&#x544A;&#x985E;&#x5225;&#xFF0C;&#x7DE8;&#x8B6F;&#x6210; JS&#x5F8C;&#x5176;&#x5BE6;&#x5C31;&#x662F;&#x4EE5;&#x524D;&#x6211;&#x5011;&#x7528;&#x4F86;&#x6A21;&#x64EC;&#x985E;&#x5225;&#x7684;&#x6280;&#x5DE7;&#x5566;&#xFF01;XD</p>
<pre><code>class Student {
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = `${firstName} ${middleInitial} ${lastName}`;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person : Person) {
    return `Hello, ${person.firstName} ${person.lastName}`;
}

let user = new Student(&quot;Jane&quot;, &quot;M.&quot;, &quot;User&quot;);

console.log(greeter(user));
</code></pre>
<h4>&#x975C;&#x614B;&#x6210;&#x54E1;</h4>
<p>&#x985E;&#x5225;&#x7684;&#x975C;&#x614B;&#x6210;&#x54E1;&#xFF0C;&#x4ED6;&#x7684;&#x5C6C;&#x6027;&#x5B58;&#x5728;&#x65BC;&#x985E;&#x672C;&#x8EAB;&#xFF0C;&#x800C;&#x4E0D;&#x662F;&#x985E;&#x7684;&#x5BE6;&#x4F8B;&#x4E0A;</p>
<pre><code>class Human {
    static hands: number = 2;
    static legs: number = 2;
}
</code></pre>
<h4>&#x7E7C;&#x627F;</h4>
<p>&#x6709;&#x985E;&#x5225;&#x7684;&#x6982;&#x5FF5;&#xFF0C;&#x7576;&#x7136;&#x5C31;&#x6703;&#x6709;&#x7E7C;&#x627F;&#x7684;&#x6982;&#x5FF5;</p>
<pre><code>class Woman extends Human {
    static gender: string = &apos;female&apos;;
}
</code></pre>
<h4>Interface &#x9032;&#x968E;</h4>
<p>interface &#x4E5F;&#x53EF;&#x4EE5;&#x7528;&#x4F86;&#x5F37;&#x5236;&#x985E;&#x5225;&#x7B26;&#x5408;&#x7D04;&#x675F;</p>
<pre><code>interface Shape {
    area(): number;
}

class Circle implements Shape {
    radius: number;
    constructor(radius: number) {
        this.radius = radius;
    }
    area(): number {
        return this.radius * this.radius * 3.1415;
    }
}
</code></pre>
<p>interface &#x4E5F;&#x53EF;&#x4EE5;&#x7E7C;&#x627F;&#x5176;&#x4ED6;&#x7684; interface</p>
<pre><code>interface Shape {
    area(): number;
}

interface Color {
    RGB: string;
}

interface Thing extends Color, Shape {
}
</code></pre>
<h4>&#x8FED;&#x4EE3;</h4>
<p>&#x591A;&#x4E86; <code>let ... of ...</code> &#x7684;&#x7528;&#x6CD5;</p>
<pre><code>let list = [4, 5, 6];

for (let i in list) {
   console.log(i); // &quot;0&quot;, &quot;1&quot;, &quot;2&quot;,
}

for (let i of list) {
   console.log(i); // &quot;4&quot;, &quot;5&quot;, &quot;6&quot;
}
</code></pre>
<p><code>let ... of ...</code> &#x7684;&#x64CD;&#x4F5C;&#x5176;&#x5BE6;&#x9577;&#x9019;&#x6A23;</p>
<pre><code>let list = [4, 5, 6];
for (let _i = 0; _i &lt; list.length; _i++) {
    var num = list[_i];
    console.log(num);
}
</code></pre>
 <br>
                                                    </div>
                    </div>
                
