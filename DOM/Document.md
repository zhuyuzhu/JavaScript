# Document

Document接口表示浏览器中加载的任何web页面，并作为进入web页面内容(即DOM树)的入口点。DOM树包括诸如<body>和等元素。它为文档document提供全局的功能，比如如何获取页面的URL和在文档中创建新元素。

Document接口描述了任何类型文档的通用属性和方法。根据文档的类型(例如HTML、XML、SVG等)，可以使用一个更大的API:带有“text/ HTML”内容类型的HTML文档也实现HTMLDocument接口，而XML和SVG文档实现XMLDocument接口。

document是整个文档页面对象。

### Document的属性



#### document.documentElement

返回一个文档的根元素，比如HTML文档中的html元素

https://developer.mozilla.org/en-US/docs/Web/API/Document/documentElement

#### document.head

兼容性IE9

文档接口的head只读属性返回当前文档的<head>元素

https://developer.mozilla.org/en-US/docs/Web/API/Document/head

#### document.body

返回文档的body元素。

#### document.title  

设置或修改当前文档的title值。

此属性适用于Gecko中的HTML、SVG、XUL和其他文档。

https://developer.mozilla.org/en-US/docs/Web/API/Document/title



#### document.designMode

**document.designMode**控制整个文档是否可编辑。取值为“on”和“off”

根据规范，该属性默认为“off”。Firefox遵循这一标准。

早期版本的Chrome和IE默认为“继承”。从Chrome 43开始，默认是“关闭”和“继承”不再支持。在IE6-10浏览器中，取值为大写。

https://developer.mozilla.org/en-US/docs/Web/API/Document/designMode



#### document.forms

仅读属性，返回一个HTMLCollection集合列表，关于在文档中的所有form表单。

HTMLCollection对象列出了文档的所有表单。集合中的每一项都是HTMLFormElement，代表一个<form>元素。

https://developer.mozilla.org/en-US/docs/Web/API/Document/forms

注意：类类似地，您可以使用HTMLFormElement访问表单组件用户输入元素的HTMLFormElement.elements的属性。

https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/elements

#### document.images

文档接口的images read-only属性返回当前HTML文档中图像的集合。

HTMLCollection提供当前文档中包含的所有图像的动态列表。集合中的每个条目都是一个HTMLImageElement，表示单个图像元素。

https://developer.mozilla.org/en-US/docs/Web/API/Document/images

#### document.links

文档接口的links是 read-only属性，返回文档中所有area元素和a元素的集合，并为href属性赋值

https://developer.mozilla.org/en-US/docs/Web/API/Document/links

#### document.scripts

document.scripts返回文档中的script元素的集合

https://developer.mozilla.org/en-US/docs/Web/API/Document/scripts



#### document.location

该document.location是 read-only属性返回一个location对象，该对象包含关于文档URL的信息，并提供了更改该URL和加载另一个URL的方法。

这意味着您可以使用document.location 在大多数情况下，就像字符串一样：document.location = 'http://www.example.com' 或则 document.location.href = 'http://www.example.com'，浏览器将会重新加载网站。

只检索URL作为字符串，即只读document.URL也可以使用属性。

https://developer.mozilla.org/en-US/docs/Web/API/Document/location

#### document.URL

文档接口的URL只读属性以字符串的形式返回文档location。——一个完整的URL地址字符串。

比如：

> document.URL
> "https://developer.mozilla.org/en-US/docs/Web/API/Document/URL"



https://developer.mozilla.org/en-US/docs/Web/API/Document/URL



### Document方法

#### document.createDocumentFragment()

创建一个新的空的DocumentFragment，其中可以添加DOM节点，以构建一个屏幕外的DOM树。

documentfragment是DOM节点对象，从来不是主DOM树的一部分。通常的用例是创建文档片段，将元素添加到文档片段，然后将文档片段添加到DOM树。

在DOM树中，文档片段被它的所有子片段所替换。

由于文档片段在内存中，而不是主DOM树的一部分，向它添加子元素不会导致页面回流（计算元素的位置和几何形状），

语法：

```js
var fragment = document.createDocumentFragment();
```



#### document.createElement()

在HTML文档中，document. createelement()方法创建由tagName指定的HTML元素，如果tagName无法识别，则创建一个HTMLUnknownElement。

语法：

```js
let element = document.createElement(tagName);
```

tagName：指定要创建的元素类型的字符串。所创建元素的nodeName用tagName的值初始化。不要在这个方法中使用限定名(如“html:a”)。当在HTML文档中调用时，createElement()会在创建元素之前将tagName转换为小写。在Firefox, Opera和Chrome中，createElement(null)的工作原理和createElement("null")一样。

示例：

```js
document.body.onload = addElement;

function addElement () {
  // create a new div element
  const newDiv = document.createElement("div");

  // and give it some content
  const newContent = document.createTextNode("Hi there and greetings!");

  // add the text node to the newly created div
  newDiv.appendChild(newContent);

  // add the newly created element and its content into the DOM
  const currentDiv = document.getElementById("div1");
  document.body.insertBefore(newDiv, currentDiv);
}
```



https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement

#### document.createEvent()

创建指定类型的事件。返回的对象应该首先初始化，然后可以传递给EventTarget.dispatchEvent。

语法：

```js
var event = document.createEvent(type);
```

- event 是创建的事件对象。
- 是表示要创建的事件类型的字符串。可能的事件类型包括`"UIEvents"`, `"MouseEvents"`, `"MutationEvents"`, and `"HTMLEvents"`

示例：创建一个事件，在某个元素上监听该类型的事件，当达到某个条件后触发该事件。

```js
// Create the event.
var event = document.createEvent('Event');

// Define that the event name is 'build'.
event.initEvent('build', true, true);

// Listen for the event.
elem.addEventListener('build', function (e) {
  // e.target matches elem
}, false);

// Target can be any Element or other EventTarget.
elem.dispatchEvent(event);
```

注意：

DOM标准中列出了适合传递给createEvent()的事件类型字符串-参见步骤2中的表。请记住，现在大多数事件对象都有构造函数，这是现代推荐的创建事件对象实例的方法。

Firefox，从67版开始，不再支持使用这种方法创建touch触摸事件。

Gecko支持一些非标准的事件对象别名，如下所示：

| Event Module          | Standard event object | Gecko also supports |
| :-------------------- | :-------------------- | :------------------ |
| Text event module     | `TextEvent`           | `TextEvents`        |
| Keyboard event module | `KeyboardEvent`       | `KeyEvents`         |
| Basic events module   | `Event`               | `Events`            |

##### 额外补充：监听和触发事件——可查看EventTarget对象

监听事件：addEventListener

触发事件：dispatchEvent

https://developer.mozilla.org/en-US/docs/Web/API/EventTarget

#### document.getElementById()

文档方法getElementById()返回一个元素对象，它表示id属性与指定字符串匹配的元素。因为元素id在指定时必须是唯一的，所以它们是快速访问特定元素的有用方法。

如果您需要访问一个没有ID的元素，您可以使用querySelector()来使用任何选择器查找该元素。

https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById

#### document.getElementsByClassName()

兼容性IE9

文档接口的getElementsByClassName方法返回一个数组样对象，包含所有具有给定类名的子元素。当在文档对象上调用时，将搜索完整的文档，包括根节点。

你也可以在任何元素上调用getElementsByClassName();它将只返回具有给定类名的指定根元素的后代元素。

比如：

```js
document.getElementsByClassName('test')
document.getElementsByClassName('red test')
document.getElementById('main').getElementsByClassName('test')
```

https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName



#### document.getElementsByTagName()

文档接口的getElementsByTagName方法返回具有给定标记名的元素的HTMLCollection。搜索完整的文档，包括根节点。返回的HTMLCollection是活动的，这意味着它自动更新自己以与DOM树保持同步，而不必再次调用document.getElementsByTagName()。

https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName



#### document.querySelector()

兼容性IE8

文档方法querySelector()返回文档中第一个与指定的选择器或一组选择器匹配的元素。如果没有找到匹配项，则返回null。

注意:匹配是使用深度优先的预先顺序遍历文档节点，从文档标记中的第一个元素开始，并按子节点的数量顺序遍历顺序节点。



#### document.querySelectorAll()

兼容性IE8

文档方法querySelectorAll()返回一个静态(非活动)节点列表，它表示与指定的一组选择器匹配的文档元素列表。

示例：

（1）获取文档中所有p元素的节点列表:

```js
const matches = document.querySelectorAll("p");
```

（2）这个例子返回了一个包含文档中所有div元素的列表，其class为note或alert:

```js
const matches = document.querySelectorAll("div.note, div.alert");
```

（3）在这里，我们得到一个p元素列表，它的直接父元素是div

```js
const container = document.querySelector("#test");
const matches = container.querySelectorAll("div.highlighted > p");
```

（4）使用一个属性选择器，返回一个文档中的iframe元素属性值为data-src的集合列表

```js
const matches = document.querySelectorAll("iframe[data-src]");
```

（5）这里，属性选择器用于返回ID为userlist的列表中包含的列表项的列表，该列表有一个data-active属性，其值为1:

```js
const container = document.querySelector("#userlist");
const matches = container.querySelectorAll("li[data-active='1']");
```



https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll



Document事件

document上也对事件进行了实现，兼容性也有有差异，有些事件更适合由document来监听，比如键盘key事件。但有些事件更适合让元素来监听。

