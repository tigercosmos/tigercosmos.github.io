---
title: 瀏覽器開發進階實戰（二）XML Serialize for HTML
date: 2017-12-26 20:53:22
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---

                    
&#x4ECA;&#x5929;&#x7E7C;&#x7E8C;&#x4EE5;<a href="https://github.com/servo/servo" target="_blank">Servo</a> &#x5C08;&#x6848;&#x4F86;&#x8A0E;&#x8AD6;&#x5982;&#x4F55;&#x5BE6;&#x4F5C;&#x3002;</p>
<p>&#x6211;&#x5011;&#x5148;&#x524D;&#x63D0;&#x5230; html &#x6703;&#x9700;&#x8981;&#x88AB; parse&#xFF0C;&#x800C;&#x53CD;&#x904E;&#x4F86;&#x7684;&#x52D5;&#x4F5C;&#x5C31;&#x662F; serialize &#x4E86;&#x3002;</p>
<p>&#x4EE5;&#x4E0B;&#x64F7;&#x53D6; <a href="https://w3c.github.io/DOM-Parsing/#widl-Element-innerHTML" target="_blank">W3C</a> &#x7684;&#x8AAA;&#x660E;&#xFF1A;<br>
(&#x5C31;&#x4E0D;&#x7FFB;&#x8B6F;&#x4E86; :P&#xFF09;</p>
<hr>
<p>For example: the innerHTML API is a common way to both parse and serialize a DOM (it does both). If a particular Node, has the following in-memory DOM:</p>
<pre><code>HTMLDivElement (nodeName: &quot;div&quot;)
&#x2503;
&#x2523;&#x2501; HTMLSpanElement (nodeName: &quot;span&quot;)
&#x2503;  &#x2503;
&#x2503;  &#x2517;&#x2501; Text (data: &quot;some &quot;)
&#x2503;
&#x2517;&#x2501; HTMLElement (nodeName: &quot;em&quot;)
   &#x2503;
   &#x2517;&#x2501; Text (data: &quot;text!&quot;)
</code></pre>
<p>And the HTMLDivElement node is stored in a variable myDiv, then to serialize myDiv&apos;s children simply get (read) the Element&apos;s innerHTML property (this triggers the serialization):</p>
<pre><code>var serializedChildren = myDiv.innerHTML;
// serializedChildren has the value:
// &quot;&lt;span&gt;some &lt;/span&gt;&lt;em&gt;text!&lt;/em&gt;&quot;
</code></pre>
<p>To parse new children for myDiv from a string (replacing its existing children), simply set the innerHTML property (this triggers parsing of the assigned string):</p>
<pre><code>myDiv.innerHTML = &quot;&lt;span&gt;new&lt;/span&gt;&lt;em&gt;children!&lt;/em&gt;&quot;;
</code></pre>
<hr>
<p>&#x4ECA;&#x5929;&#x8981;&#x505A;&#x7684;&#x4E8B;&#x60C5;&#x4E5F;&#x4E0D;&#x662F;&#x592A;&#x96E3;&#xFF0C;parser &#x5DF2;&#x7D93;&#x6709;&#x5BEB;&#x597D;&#x7684; <a href="https://github.com/servo/html5ever" target="_blank">html5ever</a> &#x5C08;&#x9580;&#x8655;&#x7406; html&#x3001;xml &#x7684;&#x89E3;&#x6790;&#x548C;&#x5E8F;&#x5217;&#x5316;&#x3002;&#x6211;&#x5011;&#x8981;&#x505A;&#x7684;&#x5C31;&#x662F;&#x628A;&#x5B83;&#x5F15;&#x5165; <code>Element</code> &#x88E1;&#x9762;&#xFF0C;&#x8B93; element &#x80FD;&#x5920;&#x505A;&#x89E3;&#x6790;&#x548C;&#x5E8F;&#x5217;&#x5316;&#x3002;</p>
<p>&#x53EF;&#x4EE5;&#x770B;<a href="https://github.com/servo/servo/commit/06759fd0fd4e6a1b905cb93fb023b389d7f73bc3" target="_blank">&#x9019;&#x500B; commit</a>&#xFF0C;&#x662F;&#x628A; xml &#x5E8F;&#x5217;&#x5316;&#x5F15;&#x5165;&#x5230; Element &#x7684;&#x6A21;&#x7D44;&#x4E2D;&#x3002;</p>
<pre><code>pub fn xmlSerialize(&amp;self, traversal_scope: XmlTraversalScope) -&gt; Fallible&lt;DOMString&gt; {
        let mut writer = vec![];
        match xmlSerialize::serialize(&amp;mut writer,
                        &amp;self.upcast::&lt;Node&gt;(),
                        XmlSerializeOpts {
                            traversal_scope: traversal_scope,
                            ..Default::default()
                        }) {
            Ok(()) =&gt; Ok(DOMString::from(String::from_utf8(writer).unwrap())),
            Err(_) =&gt; panic!(&quot;Cannot serialize element&quot;),
        }
}
</code></pre>
<p>innerHTML</p>
<pre><code>/// &lt;https://w3c.github.io/DOM-Parsing/#widl-Element-innerHTML&gt;
fn GetInnerHTML(&amp;self) -&gt; Fallible&lt;DOMString&gt; {
    let qname = QualName::new(self.prefix().clone(),
                              self.namespace().clone(),
                              self.local_name().clone());
    if document_from_node(self).is_html_document() {
        return self.serialize(ChildrenOnly(Some(qname)));
    } else {
        return self.xmlSerialize(XmlChildrenOnly(Some(qname)));
    }
}
</code></pre>
<p>outerHTML</p>
<pre><code>// https://dvcs.w3.org/hg/innerhtml/raw-file/tip/index.html#widl-Element-outerHTML
fn GetOuterHTML(&amp;self) -&gt; Fallible&lt;DOMString&gt; {
    if document_from_node(self).is_html_document() {
        return self.serialize(IncludeNode);
    } else {
        return self.xmlSerialize(XmlIncludeNode);
    }
}
</code></pre>
<hr>
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
                
