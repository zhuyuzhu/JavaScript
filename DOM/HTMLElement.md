# HTMLElement

HTMLElement 接口表示所有的 [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) 元素。一些HTML元素直接实现了HTMLElement接口，其它的间接实现HTMLElement接口。

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



#### HTMLElement.contentEditable——标签属性

兼容性IE6

**`HTMLElement.contentEditable`** 属性用于表明元素是否是可编辑的。该枚举属性（enumerated attribute）可以具有下面的几种值之一：

- `"true"` 表明该元素可编辑。
- `"false"` 表明该元素不可编辑。
- `"inherit"` 表明该元素继承了其父元素的可编辑状态。

注意：在 IE 浏览器中，`contenteditable` 不能直接用在 table、tbody、td、th、tr 等标签上。一个可编辑的 span或者 div 标签可以放在表格单元格内部。

https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/contentEditable

#### HTMLElement.isContentEditable 

兼容IE6

HTMLElement.isContentEditable只读属性返回一个布尔值，如果元素设置了contentEditable为true，则返回true，否则返回false。

示例：input框返回false

```html
    <div class="wrap">
        <div class="child" dir="rtl" contenteditable="true">123456</div>
        <span dir="rtl">123</span>
        <input type="text" dir="rtl" value="123">
    </div>
      
    <script>
        var wrap = document.getElementsByClassName('wrap')[0]
        var child = document.getElementsByClassName('child')[0]
        var input = document.querySelector('input');
        console.log(child.isContentEditable) //true
        console.log(input.isContentEditable) //false

    </script>
```





#### HTMLElement.dir——标签属性

**HTMLElement.dir**   标签属性获取或设置当前元素内容的文本写入方向。——在标签上设置了该值，才会返回对应的值。否则返回null。

元素的文本编写方向性是指文本的方向(用于支持不同的语言系统)。阿拉伯语和希伯来语是使用RTL方向性的典型语言。

一个图像可以有它的dir属性设置为“rtl”，在这种情况下，HTML属性标题和alt将被格式化并定义为“rtl”

当一个表的目录设置为“rtl”时，列顺序从右到左排列。

当一个元素的dir设置为"auto"时，该元素的方向将根据它的第一个强方向性字符确定，或者默认为其父元素的方向性。

浏览器可能允许用户改变<input>和<textarea>s的方向，以帮助创作内容。Chrome和Safari在输入字段的上下文菜单中提供了一个方向选项，而Internet Explorer和Edge使用组合键Ctrl +左Shift和Ctrl +右Shift。Firefox使用Ctrl/Cmd + Shift + X，但没有更新dir属性值。

语法：

```js
var currentWritingDirection = elementNodeReference.dir;
elementNodeReference.dir = newWritingDirection;
```

dir的可能值是ltr，从左到右，rtl，从右到左，以及auto，用于指定元素的方向必须基于元素的内容确定。

示例：效果内容从右排列

```html
        <div class="child" dir="rtl">123456</div>
        <span dir="rtl">123</span>
        <input type="text" dir="rtl" value="123">
```



https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dir



#### HTMLElement.offsetHeight、HMTLElement.offsetWidth —— border-box的宽高

兼容性IE6

**HTMLElement.offsetHeight**仅读属性，返回元素的高，包括padding和border，是一个整数值。

通常，offsetHeight是以像素为单位测量元素的CSS高度，包括任何边框、padding和水平滚动条(如果呈现)。

它不包括伪元素的高度，比如::before或::after。

对于文档主体对象，测量值包括总线性内容高度，而不是元素的CSS高度。扩展到其他线性内容下面的浮动元素将被忽略。

如果元素是隐藏的，比如：通过style.display设置的值为node，那么返回的值是0

上面的例子显示了一个适合窗口的滚动条和偏移量。然而，不可滚动的元素可能有很大的偏移值，比可见内容大得多。这些元素通常包含在可滚动元素中;因此，这些不可滚动的元素可能完全或部分不可见，这取决于可滚动容器的scrollTop设置。

注意：offsetHeight 是由MSIE首先引入的DHTML对象模型的一个属性。它有时被称为元素的物理/图形尺寸，或**元素的边框框高度（border-box）**。



**示例：打印HTMLElement.offsetWidth**

父元素div的border-box

子元素div的border-box

```css
    div.wrap {
        height: 200px;
        width: 200px;
        overflow: auto;
        padding-top: 100px;
        border: 1px solid black;
    }
    div.child {
        height: 100px;
        width: 500px;
        background-image: linear-gradient(45deg, blue, green);
        padding-right: 50px;
        margin-top: 20px;
    }
```



```html
    <div class="wrap">
        <div class="child" dir="rtl" contenteditable="true">123456</div>
    </div>
      
    <script>
        var wrap = document.getElementsByClassName('wrap')[0]
        var child = document.getElementsByClassName('child')[0]
        console.log(child.offsetWidth) //550
        console.log(wrap.offsetWidth) //202

    </script>
```



offsetHeight：https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight

offsetWidth：https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetWidth



### 定位值属性

#### HTMLElement.offsetParent

HTMLElement.offsetParent只读属性返回对最接近(在包含层次结构中最接近)**定位的(具有position属性的元素)**祖先元素的引用。如果没有定位的祖先元素，则返回最近的祖先td、th、table，如果没有祖先表元素则返回body。

https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetParent

offsetParent是有用的，因为offsetTop和offsetLeft是相对于它的填充边的。



#### HTMLElement.offsetTop

HTMLElement.offsetTop只读属性，返回当前元素的外边框相对于offsetParent节点顶部的内边框的距离。

注意：

如果元素是display:none ，他的属性将在Webkit上返回null（元素或者祖先元素的style.display是none）或者 如果元素本身的style.position是fixed

IE9上，这个属性将返回null，如果元素本身的style.position被设置为“fixed”。(使用display:none不会影响此浏览器。)

https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText

#### HTMLElement.offsetLeft

HTMLElement.offsetLeft是 read-only属性，返回HTMLElement中当前元素的左上角向左偏移的像素数。offsetParent节点。

对于块级元素，offsetTop, offsetLeft, offsetWidth和offsetHeight描述一个元素相对于offsetParent的边框。

然而，对于inline-level元素(如跨度)，可以从一行到下一个包装,offsetTop和offsetLeft描述第一个边界框的位置(使用Element.getClientRects()来获得它的宽度和高度),而offsetWidth和offsetHeight描述边界边界框的尺寸(用Element.getBoundingClientRect()来获得它的位置)。因此，具有offsetLeft、offsetTop、offsetwwidth和offsetHeight的左侧、顶部、宽度和高度的框将不会成为带有换行文本的span的边界框。

返回值：一个整数，表示从相对位置最近的父元素向左的偏移量(以像素为单位)。

https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetLeft



HTMLElement上的事件属性（GlobalEventHandlers接口提供）

句柄事件和事件 给元素事件监听提供了多样性。有些事件更适合用句柄事件、有些更适合使用event事件

