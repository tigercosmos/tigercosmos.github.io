---
title: 瀏覽器引擎處理 CSS 的簡易版（三）
date: 2017-12-18 22:46:13
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x660E;&#x5929;&#x4E00;&#x6A23;&#x8A0E;&#x8AD6; robinson &#x9019;&#x500B;&#x300C;&#x73A9;&#x5177;&#x300D;&#x5C08;&#x6848;&#x3002;&#x8B93;&#x6211;&#x5011;&#x4F86;&#x76F4;&#x63A5;&#x770B; <a href="https://github.com/mbrubeck/robinson/blob/master/src/style.rs" target="_blank">robinson/src/style.rs</a> &#x9019;&#x908A;&#x5982;&#x4F55;&#x5BE6;&#x4F5C; style&#x3002;&#x5982;&#x679C;&#x4F60;&#x9084;&#x6C92;&#x770B;&#x904E; CSS &#x7CFB;&#x5217;&#x7684;&#x524D;&#x5169;&#x90E8;&#x5206;&#xFF0C;&#x5EFA;&#x8B70;&#x4F60;&#x5148;&#x770B;&#x4E00;&#x4E0B;&#x3002;&#x5982;&#x679C;&#x662F;&#x7CFB;&#x5217;&#x7684;&#x65B0;&#x8B80;&#x8005;&#xFF0C;&#x5EFA;&#x8B70;&#x4F60;&#x5F9E;&#x7B2C;&#x4E00;&#x7BC7;&#x958B;&#x59CB;&#x8B80;&#x3002;</p>
<p>&#x9019;&#x908A;&#x8981;&#x6CE8;&#x610F;&#x4E00;&#x4E0B;&#xFF0C;&#x6211;&#x5011;&#x6628;&#x5929;&#x63D0;&#x5230;&#x7684;&#x56DB;&#x500B;&#x7279;&#x6027;&#xFF0C;&#x5728;&#x9019;&#x908A;&#x90FD;&#x6C92;&#x6709;&#x5BE6;&#x4F5C;&#xFF0C;&#x9019;&#x908A;&#x505A;&#x7684;&#x90E8;&#x5206;&#x53EA;&#x662F;&#x6700;&#x7C21;&#x55AE;&#x7684;&#xFF0C;&#x628A; CSS &#x7D81;&#x5B9A; DOM&#x3002;&#x4E5F;&#x5C31;&#x662F;&#x8B93; DOM &#x80FD;&#x6709;&#x984F;&#x8272;&#x3001;&#x5927;&#x5C0F;&#x4E4B;&#x985E;&#x7684;&#x6A23;&#x5B50;&#x3002;</p>
<h2>&#x7A0B;&#x5F0F;</h2>
<p><em><strong>&#x9019;&#x908A;&#x7A0B;&#x5F0F;&#x78BC;&#x4E0D;&#x4E0A;&#x8272;&#xFF08; ITHelp &#x4E0D;&#x652F;&#x63F4; Rust ORZ&#xFF09;</strong></em></p>
<p>&#x9019;&#x908A;&#x6211;&#x5011;&#x5B9A;&#x7FA9;&#x4E00;&#x500B; <code>StyledNode</code> &#x4F5C;&#x70BA; style tree &#x7684;&#x7BC0;&#x9EDE;&#x3002;&#x9084;&#x8A18;&#x5F97; DOM tree + CSS tree = style tree &#x55CE;&#xFF1F;</p>
<pre><code class="language-rust">pub fn style_tree&lt;&apos;a&gt;(root: &amp;&apos;a Node, stylesheet: &amp;&apos;a Stylesheet) 
-&gt; StyledNode&lt;&apos;a&gt; {

    StyledNode {
        node: root,
        specified_values: match root.node_type {
            NodeType::Element(ref elem) =&gt; 
                specified_values(elem, stylesheet),
            NodeType::Text(_) =&gt; HashMap::new()
        },
        children: root.children
                      .iter()
                      .map(|child| style_tree(child, stylesheet))
                      .collect(),
    }
    
}
</code></pre>
<p>&#x6BCF;&#x500B;&#x7BC0;&#x9EDE;&#x5C0D;&#x61C9;&#x7684; DOM &#x548C; style &#x7684;&#x5C6C;&#x6027;</p>
<pre><code class="language-rust">/// A node with associated style data.

pub struct StyledNode&lt;&apos;a&gt; {
    pub node: &amp;&apos;a Node,
    pub specified_values: PropertyMap,
    pub children: Vec&lt;StyledNode&lt;&apos;a&gt;&gt;,
}
</code></pre>
<hr>
<p>&#x63A5;&#x8457;&#x5F9E; CSS tree &#x4E2D;&#xFF0C;&#x904D;&#x4F48;&#x7684;&#x5C0B;&#x627E;&#x5C0D;&#x61C9;&#x7684; DOM&#xFF0C;&#x70BA;&#x4EC0;&#x9EBC;&#x5F9E; CSS tree &#x800C;&#x4E0D;&#x662F; DOM tree &#x5462;&#xFF1F;&#x56E0;&#x70BA; CSS &#x4E00;&#x5B9A;&#x6703;&#x6709;&#x5C0D;&#x61C9;&#x7684; DOM &#xFF08;&#x9664;&#x975E;&#x662F;&#x7121;&#x6548; CSS&#xFF09;&#xFF0C;&#x800C; DOM &#x4E0D;&#x4E00;&#x5B9A;&#x6703;&#x6709;&#x5C0D;&#x61C9;&#x7684; CSS&#xFF0C;&#x6240;&#x4EE5;&#x5F9E; CSS &#x627E; DOM &#x6548;&#x7387;&#x6BD4;&#x8F03;&#x9AD8;&#x3002;</p>
<p>&#x9084;&#x8A18;&#x5F97;&#x6211;&#x5011; CSS &#x6A21;&#x7D44;&#x505A;&#x904E;&#x7684;&#x4E8B;&#x60C5;&#x55CE;&#xFF1F; Stylesheet &#x88E1;&#x9762;&#x6709;&#x5F88;&#x591A; rules&#xFF0C;&#x6BCF;&#x500B; rules &#x88E1;&#x9762;&#x53C8;&#x6709;&#x5F88;&#x591A; selectors&#xFF0C;&#x5C0D;&#x61C9;&#x5404;&#x81EA;&#x7684;&#x503C;&#x3002;</p>
<p>&#x6240;&#x4EE5;&#x9019;&#x908A;&#x76F4;&#x63A5;&#x904D;&#x4F48; Stylesheet&#xFF0C;&#x9019;&#x6642;&#x5019;&#x6BCF;&#x6AA2;&#x67E5;&#x4E00;&#x500B; rule &#x6703;&#x547C;&#x53EB; <code>match_rule</code>&#xFF0C;&#x6BCF;&#x6B21; <code>match_rule</code> &#x6703;&#x518D;&#x6AA2;&#x67E5; selectors&#x3002;</p>
<pre><code class="language-rust">// Find all CSS rules that match the given element.

fn matching_rules&lt;&apos;a&gt;(elem: &amp;ElementData, stylesheet: &amp;&apos;a Stylesheet) -&gt; Vec&lt;MatchedRule&lt;&apos;a&gt;&gt; {
    stylesheet.rules.iter()
              .filter_map(|rule| match_rule(elem, rule))
              .collect()
}
</code></pre>
<pre><code class="language-rust">// If `rule` matches `elem`, return a `MatchedRule`. 
// Otherwise return `None`.

fn match_rule&lt;&apos;a&gt;(elem: &amp;ElementData, rule: &amp;&apos;a Rule) 
-&gt; Option&lt;MatchedRule&lt;&apos;a&gt;&gt; {
    rule.selectors.iter()
        .find(|selector| matches(elem, *selector))
        .map(|selector| (selector.specificity(), rule))
}
</code></pre>
<hr>
<p>&#x85C9;&#x7531;&#x4E4B;&#x524D;&#x5728; DOM &#x6A21;&#x7D44;&#x505A;&#x7684;&#xFF0C;&#x9019;&#x908A;&#x53EF;&#x4EE5;&#x8F15;&#x9B06;&#x53D6;&#x5F97; DOM &#x7684; CSS &#x662F;&#x4EC0;&#x9EBC;&#x3002;</p>
<pre><code>impl ElementData {
    pub fn id(&amp;self) -&gt; Option&lt;&amp;String&gt; {
        self.attributes.get(&quot;id&quot;)
    }

    pub fn classes(&amp;self) -&gt; HashSet&lt;&amp;str&gt; {
        match self.attributes.get(&quot;class&quot;) {
            Some(classlist) =&gt; classlist.split(&apos; &apos;).collect(),
            None =&gt; HashSet::new()
        }
    }
}
</code></pre>
<p>&#x518D;&#x85C9;&#x7531; <code>matches</code> &#x7531; selector &#x53BB;&#x5C0D;&#x61C9; DOM &#x7684; CSS&#xFF0C;&#x5982;&#x679C;&#x6709;&#x5339;&#x914D;&#x5C31;&#x56DE;&#x50B3;</p>
<pre><code>/// Selector matching:
fn matches(elem: &amp;ElementData, selector: &amp;Selector) -&gt; bool {
    match *selector {
        Selector::Simple(ref simple_selector) =&gt; 
            matches_simple_selector(elem, simple_selector)
    }
}

fn matches_simple_selector(elem: &amp;ElementData, selector: &amp;SimpleSelector) -&gt; bool {
    // Check type selector
    if selector.tag_name.iter().any(|name| elem.tag_name != *name) {
        return false
    }

    // Check ID selector
    if selector.id.iter().any(|id| elem.id() != Some(id)) {
        return false;
    }

    // Check class selectors
    let elem_classes = elem.classes();
    if selector.class.iter().any(|class| !elem_classes.contains(&amp;**class)) {
        return false;
    }

    // We didn&apos;t find any non-matching selector components.
    true
}
</code></pre>
<hr>
<p>&#x6700;&#x5F8C;&#x6211;&#x5011;&#x5C31;&#x8B93;&#x672C;&#x6587;&#x4E00;&#x958B;&#x59CB;&#x63D0;&#x5230;&#x7684; <code>style_tree</code>  &#x85C9;&#x7531;&#x57F7;&#x884C; <code>specified_values</code> &#x53D6;&#x5F97;&#x6A39;&#x88E1;&#x9762;&#x7684;&#x6578;&#x503C;&#xFF0C;&#x53D6;&#x5F97;&#x65B9;&#x5F0F;&#x662F;&#x9760;&#x4E0A;&#x9762;&#x63D0;&#x5230;&#x7684; <code>matching_rules</code>&#x3002;</p>
<pre><code>/// Apply styles to a single element, returning the specified styles.
fn specified_values(elem: &amp;ElementData, stylesheet: &amp;Stylesheet) -&gt; PropertyMap {
    let mut values = HashMap::new();
    let mut rules = matching_rules(elem, stylesheet);

    // Go through the rules from lowest to highest specificity.
    rules.sort_by(|&amp;(a, _), &amp;(b, _)| a.cmp(&amp;b));
    for (_, rule) in rules {
        for declaration in &amp;rule.declarations {
            values.insert(declaration.name.clone(), declaration.value.clone());
        }
    }
    values
}
</code></pre>
<hr>
<p>&#x4EE5;&#x4E0A;&#x5C31;&#x662F;&#x7C21;&#x55AE;&#x7684; style tree &#x5BE6;&#x4F5C;&#x65B9;&#x5F0F;&#xFF0C;&#x5176;&#x5BE6;&#x773C;&#x5C16;&#x7684;&#x8A71;&#x5C31;&#x53EF;&#x4EE5;&#x767C;&#x73FE;&#x6C92;&#x4EC0;&#x9EBC;&#x6280;&#x8853;&#xFF0C;&#x7B49;&#x65BC;&#x5C31;&#x662F;&#x597D;&#x5E7E;&#x500B;&#x8FF4;&#x5708;&#x53BB;&#x505A;&#x5339;&#x914D;&#xFF0C;&#x53EA;&#x662F;&#x5BEB;&#x6CD5;&#x6BD4;&#x8F03;&#x597D;&#x770B;&#x800C;&#x5DF2;&#x3002;&#x9019;&#x7A2E;&#x5BEB;&#x6CD5;&#x662F;&#x5B8C;&#x5168;&#x7DDA;&#x6027;&#xFF0C;&#x975E;&#x5E38;&#x6C92;&#x6548;&#x7387;&#xFF0C;&#x6700;&#x65B0;&#x7684; Servo &#x7684; Stylo &#x5C31;&#x91DD;&#x5C0D;&#x9019;&#x90E8;&#x4EFD;&#x505A;&#x9AD8;&#x6548;&#x80FD;&#x7684;&#x512A;&#x5316;&#xFF0C;&#x5176;&#x4E2D;&#x4E00;&#x9805;&#x5C31;&#x662F;&#x5E73;&#x884C;&#x5316;&#x8655;&#x7406;&#x6A39;&#x3002;</p>
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
                
