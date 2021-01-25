# Element元素基类

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList

ParentNode：https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/children

文档中指的Element，就是获取该元素（dom）。上面的文章中，Element上有属性、方法、事件、继承、DOM的相关页面

可以深入

Element是最通用的基类，文档中的所有元素对象(即表示元素的对象)都继承该基类。它只有所有类型的元素共有的方法和属性。更具体的类从Element继承。例如，HTMLElement接口是HTML元素的基本接口，而SVGElement接口是所有SVG元素的基础。大多数功能都是在类层次结构的下面指定的。

### 一、元素标签上的属性

#### 1、Element.attributes

**`Element.attributes`** 属性返回该元素所有属性节点的一个实时集合。该集合是一个 [`NamedNodeMap`](https://developer.mozilla.org/zh-CN/docs/Web/API/NamedNodeMap) 对象，不是一个数组，所以它没有 [`数组`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array) 的方法，其包含的 [`属性`](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr) 节点的索引顺序随浏览器不同而不同。更确切地说，`attributes` 是字符串形式的名/值对，每一对名/值对对应一个属性节点。



https://developer.mozilla.org/zh-CN/docs/Web/API/Element/attributes

#### 2、Element.id

**id属性：获取或设置指定元素的id属性值。**

同一文档中，若 `id` 的值不是空字符串 `""`，便必须是唯一的；也就是说，不同元素的 ID 必须是不同的。这有助于让常用的 [`getElementById`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById) 方法通过 `id` 的值找到对应的单个元素

**注意：**虽然 ID 是区分大小写的, 但是不应该同时使用仅大小写有不同的 ID 值。

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/id

#### 3、Element.className

**className** 获取或设置指定元素的class属性的值。

返回值是一个字符串变量,表示当前元素的`class`属性的值,可以是由空格分隔的多个`class`属性值。

使用名称`className`而不是`class`作为属性名,是因为"class" 在JavaScript中是个保留字.

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/className

#### 4、Element.tagName

返回当前元素的标签名，返回值都是大写。

在HTML文档中, `tagName`会返回其大写形式. 对于元素节点来说,`tagName属性`的值和[nodeName](https://developer.mozilla.org/zh-cn/DOM/Node.nodeName)属性的值是相同的。

在XML (或者其他基于XML的语言,比如XHTML,xul)文档中,`tagName的值会`保留原始的大小写。

比如：

```js
var span = document.getElementById("born");
alert(span.tagName);
```

在XHTML中 (或者其他的XML格式文件中), 会弹出小写的"span".而在HTML中, 会弹出大写的"SPAN".

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/tagName

#### 操作标签属性的方法：

1、Element.getAttribute()



**`getAttribute()`** 返回元素上一个指定的属性值。如果指定的属性不存在，则返回  `null` 或 `""` （空字符串）；

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getAttribute

2、Element.getAttributeNode()

返回指定元素的指定属性节点

当在一个被标记为HTML文档的DOM中的HTML元素上调用这个方法时， getAttributeNode会将参数转变为小写形式。



### 5、previousElementSibling、 nextElementSibling 、lastElementChild

兼容性IE9，支持性不是很好。需要看他们的pollfill。

返回前一个兄弟节点

**previousElementSibling** 返回当前元素在其父元素的子元素节点中的前一个元素节点,如果该元素已经是第一个元素节点,则返回`null,`该属性是只读的.

**nextElementSibling** 返回当前元素在其父元素的子元素节点中的后一个元素节点,如果该元素已经是最后一个元素节点,则返回`null,`该属性是只读的.

**ParentNode.lastElementChild** 只读属性 返回对象的最后一个子[`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)，如果没有子元素，则返回 `null`。

**ParentNode.firstElementChild** 只读属性，返回对象的第一个子 [`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/元素), 如果没有子元素，则为null。

**ParentNode.children** 是一个只读属性，返回 一个Node的子[`elements`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) ，是一个动态更新的 [`HTMLCollection`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCollection)。

https://developer.mozilla.org/zh-CN/docs/Web/API/NonDocumentTypeChildNode/previousElementSibling

https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/firstElementChild

https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/lastElementChild

https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/children

6、element.outerHTML

 [`element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) DOM接口的`outerHTML`属性获取描述元素（包括其后代）的序列化HTML片段。它也可以设置为用从给定字符串解析的节点替换元素。

要仅获取元素内容的HTML表示形式或替换元素的内容，请使用 [`innerHTML`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/innerHTML) 属性

返回值，内容包含描述元素及其后代的序列化HTML片段。

读取outerHTML的值将返回一个DOMString，其中包含元素及其后代的HTML序列化。设置outerHTML的值，用解析指定的htmlString构造的新DOM树替换元素及其所有后代。

在设置outerHTML替换该元素时，实际上是通过元素的父元素来进行添加的。所以如果元素没有父元素执行Element.outerHTML会报错。

比如：通过createElement创建的元素；

实时的获取DOM，比如ID值代表的DOM就是实时的，而getELementBy...不是实时的，



**报错：**

尝试使用无效的HTML字符串设置outerHTML。

尝试在文档的直接子元素(比如Document. documentelement)上设置outerHTML。

注意：如果元素没有父元素，设置它的outerHTML属性不会改变它或它的后代元素。许多浏览器也会抛出异常。例如:

```js
var div = document.createElement("div");
div.outerHTML = "<div class=\"test\">test</div>";
console.log(div.outerHTML); // output: "<div></div>"
```



另外，当元素在文档中被替换时，设置了outerHTML属性的变量仍然保留对原始元素的引用：——实际上是操作的父元素对应的子元素的位置，而不是修改element.outerHMTL引用值。

```js
var p = document.getElementsByTagName("p")[0];
console.log(p.nodeName); // shows: "P"
p.outerHTML = "<div>This div replaced a paragraph.</div>";
console.log(p.nodeName); // still "P";
```



返回值将包含html转义的属性:

```js
var anc = document.createElement("a");
anc.href = "https://developer.mozilla.org?a=b&c=d";
console.log(anc.outerHTML); // output: "<a href='https://developer.mozilla.org?a=b&amp;c=d'></a>"
```



https://developer.mozilla.org/zh-CN/docs/Web/API/Element/outerHTML



1element.innerHTML

**`Element.innerHTML`** 属性设置或获取HTML语法表示的元素的后代。

[`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString) 包含元素后代的HTML序列。设置元素的 `innerHTML` 将会删除所有该元素的后代并以上面给出的 htmlString 替代。

如果要向一个元素中插入一段 HTML，而不是替换它的内容，那么请使用 [`insertAdjacentHTML()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML) 方法。

当插入纯文本时，建议不要使用 `innerHTML` 。取而代之的是使用 [`Node.textContent`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent) ，它不会把给定的内容解析为 HTML，它仅仅是将原始文本插入给定的位置。



 当父元素是 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 时，设置 `innerHTML` 将会提示不允许修改。

设置 `innerHTML` 的值可以让你轻松地将当前元素的内容替换为新的内容。

举个例子来说，你可以通过文档 [`body`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/body) 属性删除 body 的全部内容。

```js
document.body.innerHTML = "";
```

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/innerHTML

### 元素滚动属性



`**Element.scrollTop**` 属性可以获取或设置一个元素的内容垂直滚动的像素数。

**`Element.scrollLeft`** 属性可以读取或设置元素滚动条到元素左边的距离。

注意如果这个元素的内容排列方向（[`direction`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/direction)） 是`rtl` (right-to-left) ，那么滚动条会位于最右侧（内容开始处），并且`scrollLeft`值为0。此时，当你从右到左拖动滚动条时，scrollLeft会从0变为负数。

**`Element.scrollHeight`** 这个只读属性是一个元素内容高度的度量，包括由于溢出导致的视图中不可见内容。

`scrollHeight `的值等于该元素在不使用滚动条的情况下为了适应视口中所用内容所需的最小高度。 没有垂直滚动条的情况下，scrollHeight值与元素视图填充所有内容所需要的最小值[`clientHeight`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientHeight)相同。包括元素的padding，但不包括元素的border和margin。scrollHeight也包括 [`::before`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before) 和 [`::after`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after)这样的伪元素。

**`Element.scrollWidth`** 这个只读属性是元素内容宽度的一种度量，包括由于overflow溢出而在屏幕上不可见的内容。

`scrollWidth`值等于元素在不使用水平滚动条的情况下适合视口中的所有内容所需的最小宽度。 宽度的测量方式与[`clientWidth`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientWidth)相同：它包含元素的内边距，但不包括边框，外边距或垂直滚动条（如果存在）。 它还可以包括伪元素的宽度，例如[`::before`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before)或[`::after`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after)。 如果元素的内容可以适合而不需要水平滚动条，则其`scrollWidth`等于[`clientWidth`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientWidth)



https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollHeight

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollLeft

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollTop

https://developer.mozilla.org/zh-CN/docs/Web/API/element/scrollWidth



1Element.clientWidth、

内联元素以及没有 CSS 样式的元素的 `**clientWidth**` 属性值为 0。`**Element.clientWidth**` 属性表示元素的内部宽度，以像素计。该属性包括内边距 padding，但不包括边框 border、外边距 margin 和垂直滚动条（如果有的话）。

该属性值会被四舍五入为一个整数。如果你需要一个小数值，可使用 [`element.getBoundingClientRect()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)。

2、Element.clientHeight

这个属性是只读属性，对于没有定义CSS或者内联布局盒子的元素为0，否则，它是元素内部的高度(单位像素)，包含内边距，但不包括水平滚动条、边框和外边距。

`clientHeight` 可以通过 CSS `height` + CSS `padding` - 水平滚动条高度 (如果存在)来计算.

> **备注:** 此属性会将获取的值四舍五入取整数。 如果你需要小数结果, 请使用 [`element.getBoundingClientRect()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect).
>
> 备注：上面的有问题 因为使用element.getBoundingClientRect()只能获取元素的width / height，但是这个值是 offsetWidth / offsetHeight ，包括边框的长度，所以不能获取clientWidth / clientHeight



3、Element.clientLeft

表示一个元素的左边框的宽度，以像素表示。如果元素的文本方向是从右向左（RTL, right-to-left），并且由于内容溢出导致左边出现了一个垂直滚动条，则该属性包括滚动条的宽度。`clientLeft` 不包括左外边距和左内边距。`clientLeft` 是只读的。



4、Element.clientTop

一个元素顶部边框的宽度（以像素表示）。不包括顶部外边距或内边距。`clientTop` 是只读的。

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientWidth

