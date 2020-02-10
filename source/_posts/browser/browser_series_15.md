---
title: 瀏覽器開發進階實戰（二）XML Serialize for HTML
date: 2017-12-26 20:53:22
tags: [browser, 瀏覽器, 鐵人賽, 來做個網路瀏覽器吧！]
---
> 本系列目錄 [《來做個網路瀏覽器吧！》文章列表](/post/2018/02/browser/browser_series_33/)


                    
今天繼續以[Servo](https://github.com/servo/servo) 專案來討論如何實作。

我們先前提到 html 會需要被 parse，而反過來的動作就是 serialize 了。


以下擷取 [W3C](https://w3c.github.io/DOM-Parsing/#widl-Element-innerHTML) 的說明：
(就不翻譯了 :P）

---
For example: the innerHTML API is a common way to both parse and serialize a DOM (it does both). If a particular Node, has the following in-memory DOM:

    HTMLDivElement (nodeName: "div")
    ┃
    ┣━ HTMLSpanElement (nodeName: "span")
    ┃  ┃
    ┃  ┗━ Text (data: "some ")
    ┃
    ┗━ HTMLElement (nodeName: "em")
       ┃
       ┗━ Text (data: "text!")
  

And the HTMLDivElement node is stored in a variable myDiv, then to serialize myDiv's children simply get (read) the Element's innerHTML property (this triggers the serialization):

    var serializedChildren = myDiv.innerHTML;
    // serializedChildren has the value:
    // "<span>some </span><em>text!</em>"
  

To parse new children for myDiv from a string (replacing its existing children), simply set the innerHTML property (this triggers parsing of the assigned string):

    myDiv.innerHTML = "<span>new</span><em>children!</em>";
---

今天要做的事情也不是太難，parser 已經有寫好的 [html5ever](https://github.com/servo/html5ever) 專門處理 html、xml 的解析和序列化。我們要做的就是把它引入 `Element` 裡面，讓 element 能夠做解析和序列化。

可以看[這個 commit](https://github.com/servo/servo/commit/06759fd0fd4e6a1b905cb93fb023b389d7f73bc3)，是把 xml 序列化引入到 Element 的模組中。

```
pub fn xmlSerialize(&self, traversal_scope: XmlTraversalScope) -> Fallible<DOMString> {
        let mut writer = vec![];
        match xmlSerialize::serialize(&mut writer,
                        &self.upcast::<Node>(),
                        XmlSerializeOpts {
                            traversal_scope: traversal_scope,
                            ..Default::default()
                        }) {
            Ok(()) => Ok(DOMString::from(String::from_utf8(writer).unwrap())),
            Err(_) => panic!("Cannot serialize element"),
        }
}
```
innerHTML
```
/// <https://w3c.github.io/DOM-Parsing/#widl-Element-innerHTML>
fn GetInnerHTML(&self) -> Fallible<DOMString> {
    let qname = QualName::new(self.prefix().clone(),
                              self.namespace().clone(),
                              self.local_name().clone());
    if document_from_node(self).is_html_document() {
        return self.serialize(ChildrenOnly(Some(qname)));
    } else {
        return self.xmlSerialize(XmlChildrenOnly(Some(qname)));
    }
}
```
outerHTML
```
// https://dvcs.w3.org/hg/innerhtml/raw-file/tip/index.html#widl-Element-outerHTML
fn GetOuterHTML(&self) -> Fallible<DOMString> {
    if document_from_node(self).is_html_document() {
        return self.serialize(IncludeNode);
    } else {
        return self.xmlSerialize(XmlIncludeNode);
    }
}
```

---

希望有幫到大家，大家明天見！

