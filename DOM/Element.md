# Element元素基类

Element是最通用的基类，文档中的所有元素对象(即表示元素的对象)都继承该基类。它只有所有类型的元素共有的方法和属性。更具体的类从Element继承。例如，HTMLElement接口是HTML元素的基本接口，而SVGElement接口是所有SVG元素的基础。大多数功能都是在类层次结构的下面指定的。

Web平台领域之外的语言，比如通过XULElement接口实现的XUL，也实现了Element。

### 一、元素标签上的属性

#### 标签属性获取和设置——属性

#### （1）Element.attributes

**`Element.attributes`** 属性返回该元素所有属性节点的一个实时集合。该集合是一个 [`NamedNodeMap`](https://developer.mozilla.org/zh-CN/docs/Web/API/NamedNodeMap) 对象，不是一个数组，所以它没有 [`数组`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array) 的方法，其包含的 [`属性`](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr) 节点的索引顺序随浏览器不同而不同。更确切地说，`attributes` 是字符串形式的名/值对，每一对名/值对对应一个属性节点。

示例：

```html
    <div id="wrapper" style="color: aqua;" class="login">
        <p>1212</p>
    </div>
    <script>
        var domWrap = document.getElementById('wrapper');
        console.log(domWrap.attributes) 
    </script>
```

返回的是一个NameNodeMap对象：

```
{
	0: id
	1: style
	2: class
	length: 3
	class: class
	id: id
	style: style
	__proto__: NamedNodeMap
}
```

#### （2）Element.id

**id属性：获取或设置指定元素的id属性值。**

同一文档中，若 `id` 的值不是空字符串 `""`，便必须是唯一的；也就是说，不同元素的 ID 必须是不同的。这有助于让常用的 [`getElementById`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById) 方法通过 `id` 的值找到对应的单个元素

**注意：**虽然 ID 是区分大小写的, 但是不应该同时使用仅大小写有不同的 ID 值。

https://developer.mozilla.org/en-US/docs/Web/API/Element/id

#### （3）Element.className

**className** 获取或设置指定元素的class属性的值。

返回值是一个字符串变量,表示当前元素的`class`属性的值,可以是由空格分隔的多个`class`属性值。

使用名称`className`而不是`class`作为属性名,是因为"class" 在JavaScript中是个保留字.

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/className

#### （4）Element.tagName

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

#### 标签属性获取和设置——方法

**标签上自定义的属性，页面上会显示为小写！**

比如：标签属性LastName="zhu"，在页面上是

```html
<div lastname="zhu">
    
</div>
```

#### （1）Element.getAttribute()、Element.setAttribute()、Element.removeAttribute()、Element.hasAttribute()

**Element.getAttribute()——获取标签属性**

元素接口的getAttribute()方法返回元素上指定属性的值。如果给定的属性不存在，则返回值为null或""(空字符串);

https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute

**Element.setAttribute()——设置标签属性**

在指定元素上设置属性的值。如果该属性已经存在，则更新该值;否则，将使用指定的名称和值添加一个新属性。

https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute

**Element.removeAttribute()——移除标签属性**

元素方法removeAttribute()从元素中移除指定名称的属性。

https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttribute

**Element.hasAttribute()——判断标签属性**

方法的作用是:返回一个布尔值，指示指定的元素是否具有指定的属性。

https://developer.mozilla.org/en-US/docs/Web/API/Element/hasAttribute



#### （2）Element.getAttributeNode()、setAttributeNode() 、Element.removeAttributeNode()

**Element.getAttributeNode()**

以Attr节点的形式返回指定元素的指定属性。

```html
    <div id="wrapper" style="color: aqua;" class="login" lastname="zhu">
        <p>1212</p>
    </div>
    <script>
        var domWrap = document.getElementById('wrapper');
        domWrap.setAttribute('lastname', 'zhu');
        console.log(domWrap.getAttributeNode('id'))
        console.log(domWrap.getAttributeNode('style'))
        console.log(domWrap.getAttributeNode('class'))
        console.log(domWrap.getAttributeNode('LastName'))
    </script>
```

返回：Attr节点，以下返回值都是attr节点。

> id="wrapper"
>
> style="color: aqua;"
>
> class="login"
>
> lastname="zhu"

https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttributeNode



**Element.setAttributeNode()**

方法的作用是:为指定的元素添加一个新的Attr节点。

```js
element.setAttributeNode(attrNode);
```

```html
<div id="one" align="left">one</div>
<div id="two">two</div>
<script>
let d1 = document.getElementById('one');
let d2 = document.getElementById('two');
let a = d1.getAttributeNode('align');

d2.setAttributeNode(a.cloneNode(true));//克隆节点，才能设置到Element上。

console.log(d2.attributes[1].value);// Returns: 'left'
</script>
```

https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttributeNode



**Element.removeAttributeNode()**

元素对象的removeAttributeNode()方法从当前元素中删除指定的属性。

```
removedAttr = element.removeAttributeNode(attributeNode)
```

https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttributeNode



#### 处理元素属性的DOM方法

| 常用方法               | 直接处理Attr节点的DOM 1级方法(很少使用) |
| ---------------------- | --------------------------------------- |
| setAttribute (DOM 1)   | setAttributeNode                        |
| getAttribute(DOM 1)    | getAttributeNode                        |
| hasAttribute (DOM 2)   |                                         |
| removeAttribute(DOM 1) | removeAttributeNode                     |

示例：

```html
    <div id="wrapper" style="color: aqua;">
        <p>1212</p>
    </div>
    <script>
        var domWrap = document.getElementById('wrapper');
        domWrap.setAttribute('lastname', 'zhu');
        console.log(domWrap.getAttribute('id')) // warpper
        console.log(domWrap.hasAttribute('style')) // true
        domWrap.removeAttribute('style')
    </script>
```



### 二、操作元素标签自身——element.outerHTML、element.innerHTML

### 1、element.outerHTML

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



###  2、Element.innerHTML

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



### 三、操作元素标签相关的标签

ParentNode和ChildNode纯接口，实现这个纯接口的对象类型:CharacterData和Element。

即：Element上有对应的属性，对接口进行了实现。比如：Element上的previousElementSibling属性实现了ChildNode接口的previousElementSibling

### 1、previousElementSibling、 nextElementSibling 

兼容性IE9，支持性不是很好。需要看他们的pollfill，支持IE8。

返回前一个兄弟节点

**previousElementSibling** 返回当前元素在其父元素的子元素节点中的前一个元素节点,如果该元素已经是第一个元素节点,则返回`null,`该属性是只读的.

**nextElementSibling** 返回当前元素在其父元素的子元素节点中的后一个元素节点,如果该元素已经是最后一个元素节点,则返回`null,`该属性是只读的.

虽然是只读的，但是可以通过修改只读对象的属性，来改变前一个元素或后一个元素内容。

注意：下面代码生效和不生效

```html
    <div id="one" class="login" style="height: 200px!important;">one</div>
    <div id="two">two</div>
    <script>
        let two = document.getElementById('two');
        two.previousElementSibling = '<span>111</span>' //不生效
        two.previousElementSibling.style.backgroundColor = "#ccc"; //生效
    </script>
```

https://developer.mozilla.org/en-US/docs/Web/API/NonDocumentTypeChildNode/previousElementSibling



#### 2、ParentNode.firstElementChild、ParentNode.lastElementChild、ParentNode.children



**（1）ParentNode.children** 是一个只读属性，返回 一个Node的子[`elements`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) ，是一个动态更新的 [`HTMLCollection`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCollection)。

**ParentNode.firstElementChild** 只读属性，返回对象的第一个子 [`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/元素), 如果没有子元素，则为null。

示例：

```html
    <ul id="foo">
        <li>First  (1)</li>
        <li>Second (2)</li>
        <li>Third  (3)</li>
      </ul>
      
      <script>
      var foo = document.getElementById('foo');
      
      console.log(foo.firstElementChild.textContent);// First  (1)
      console.log(foo.lastElementChild.textContent) //Third  (3)
      console.log(foo.children)
      //结果
      HTMLCollection(3) [li, li, li]
		0: li
		1: li
		2: li
		length: 3
		__proto__: HTMLCollection
```

**兼容性IE9，支持IE和Safari的pollfill：**https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/firstElementChild#polyfill_for_ie8_ie9_and_safari



https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/firstElementChild

#### （2）ParentNode.lastElementChild

**ParentNode.lastElementChild** 只读属性 返回对象的最后一个子[`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)，如果没有子元素，则返回 `null`。

下面的代码在Internet Explorer和Safari中添加了对Document和DocumentFragment的lastElementChild()支持。

**pollfill**：https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/lastElementChild#polyfill



https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/lastElementChild

#### （3）ParentNode.children

**兼容性：**兼容性IE9，ie6、ie7和ie8都支持，但错误地包含了注释节点。

ParentNode属性children是一个只读属性，它返回一个活的HTMLCollection，其中包含调用它的节点的所有子元素。

HTMLCollection是一个活动的、有序的DOM元素集合，这些元素是node的子元素。可以通过使用集合上的item()方法或使用JavaScript数组样式的符号来访问集合中的各个子节点。

**pollfill：Adds Document & DocumentFragment support for IE9 & Safari.**

https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children#polyfill



https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/children





### 四、元素标签滚动

#### 1、滚动属性



**Element.scrollTop** 属性可以获取或设置一个元素的内容垂直滚动的像素数。

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



#### 2、滚动方法——Element上这三个方法兼容性极差

##### （1）scroll

元素界面的scroll()方法将元素滚动到给定元素内的一组特定坐标。

```
element.scroll(x-coord, y-coord)
```

https://developer.mozilla.org/en-US/docs/Web/API/Element/scroll

##### （2）scrollTo

元素界面的scrollTo()方法滚动到给定元素内的一组特定坐标。

```
element.scrollTo(x-coord, y-coord)
```

https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollTo

##### （3）scrollBy

元素界面的scrollBy()方法按给定的数量滚动一个元素。

```
element.scrollBy(x-coord, y-coord);
```

https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollBy



1Element.clientWidth、

内联元素以及没有 CSS 样式的元素的 `clientWidth` 属性值为 0。`Element.clientWidth` 属性表示元素的内部宽度，以像素计。该属性包括内边距 padding，但不包括边框 border、外边距 margin 和垂直滚动条（如果有的话）。

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



### 插入HTML：

1Element.insertAdjacentElement()、Element.insertAdjacentHTML()、Element.insertAdjacentText()



https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML



### querySelector选择器



https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector