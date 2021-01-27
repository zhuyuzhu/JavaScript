# HTMLElementObject

1、获取该标签dom对象

Chrome打印出的标签dom对象是：包含了所有子元素的标签

IE和Edge打印出的标签dom对象是：只有该标签

需要注意的是：这个是标签对象，虽然控制台可以打印出来。但是这是对象，是不可以调用toString()或String()方法的。

```
Chrome浏览器：
	<div id="d">
        <div>
            <div class="1">
                <p>11111</p>
            </div>
        </div>
    </div>
    
而IE和Edge
<div id="d"></div>
```



div标签dom对象——HTMLDivElement——Element——Node——EventTarget——Object

dom对象的原型HTMLDivElement对象上有很多的属性和方法，可以让DOM对象继承。

比如：

https://www.runoob.com/jsref/dom-obj-all.html

HTMLDivElement和Element对象属性和方法差不多。

Node：

> 1. ATTRIBUTE_NODE: 2
> 2. CDATA_SECTION_NODE: 4
> 3. COMMENT_NODE: 8
> 4. DOCUMENT_FRAGMENT_NODE: 11
> 5. DOCUMENT_NODE: 9
> 6. DOCUMENT_POSITION_CONTAINED_BY: 16
> 7. DOCUMENT_POSITION_CONTAINS: 8
> 8. DOCUMENT_POSITION_DISCONNECTED: 1
> 9. DOCUMENT_POSITION_FOLLOWING: 4
> 10. DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC: 32
> 11. DOCUMENT_POSITION_PRECEDING: 2
> 12. DOCUMENT_TYPE_NODE: 10
> 13. ELEMENT_NODE: 1
> 14. ENTITY_NODE: 6
> 15. ENTITY_REFERENCE_NODE: 5
> 16. NOTATION_NODE: 12
> 17. PROCESSING_INSTRUCTION_NODE: 7
> 18. TEXT_NODE: 3
> 19. appendChild: *ƒ appendChild()*
> 20. baseURI: (...)
> 21. childNodes: (...)
> 22. cloneNode: *ƒ cloneNode()*
> 23. compareDocumentPosition: *ƒ compareDocumentPosition()*
> 24. contains: *ƒ contains()*
> 25. firstChild: (...)
> 26. getRootNode: *ƒ getRootNode()*
> 27. hasChildNodes: *ƒ hasChildNodes()*
> 28. insertBefore: *ƒ insertBefore()*
> 29. isConnected: (...)
> 30. isDefaultNamespace: *ƒ isDefaultNamespace()*
> 31. isEqualNode: *ƒ isEqualNode()*
> 32. isSameNode: *ƒ isSameNode()*
> 33. lastChild: (...)
> 34. lookupNamespaceURI: *ƒ lookupNamespaceURI()*
> 35. lookupPrefix: *ƒ lookupPrefix()*
> 36. nextSibling: (...)
> 37. nodeName: (...)
> 38. nodeType: (...)
> 39. nodeValue: (...)
> 40. normalize: *ƒ normalize()*
> 41. ownerDocument: (...)
> 42. parentElement: (...)
> 43. parentNode: (...)
> 44. previousSibling: (...)
> 45. removeChild: *ƒ removeChild()*
> 46. replaceChild: *ƒ replaceChild()*
> 47. textContent: (...)

EventTarget：

> 1. addEventListener: *ƒ addEventListener()*
> 2. dispatchEvent: *ƒ dispatchEvent()*
> 3. removeEventListener: *ƒ removeEventListener()*

具体的属性和方法如下：

