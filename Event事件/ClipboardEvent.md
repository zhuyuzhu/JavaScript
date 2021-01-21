# ClipboardEvent：copy cut paste event

### Abstract（摘要）

操作系统的copy、cut、paste操作，不管是哪个版本的浏览器，都对操作系统实现了赋值剪切粘贴的操作。都可以把浏览器内容进行copy、可以将可编辑文本内容cut。将数据copy cut paste到其他软件上。这是操作系统的默认行为。

而关于copy、cut、paste事件的监听，浏览器监听了这些事件后，可以禁用默认行为，或修改事件操作的内容；比如有些网站禁止复制页面内容，知乎网页版在复制内容时，会额外的添加该文章的作者权限信息。

不同浏览器在监听这三个事件有所不同，比如：

兼容性：caniuse官网上显示不兼容IE，但是在IE浏览器上测试，三个事件兼容IE9，都可以监听到这三个事件。

还有event上携带的信息也有所差异，等等。



### copy、cut、paste存值和取值

- **copy event**

  - 当用户执行复制操作时，触发copy事件 ，比如：Ctrl+C复制文本、右键复制文本

  - 该事件的默认行为：将所选内容（如果有）复制的系统剪切板上。可以通过event.preventDefault()阻止默认行为。

- **cut event**

  - 用户执行一个cut操作时，触发浏览器的cut事件；只有当用户在可编辑元素上执行cut操作时，才能将选中的内容剪切到系统剪切板上，否则无法剪切内容。

  - **如果用户cut不可编辑的元素内容，会触发cut事件，但系统剪切板不会获取数据。**

- **paste event**

  - 用户执行paste操作时，会触发浏览器的paste事件；只有在可编辑元素上执行paste事件时，才会将剪切板上的内容粘贴到可编辑标签上。



可以通过window.getSelection()方法获取selection对象，该对象可以捕获选中的内容，实际上和copy内容一致。

目前在Firefox, Edge (非 Chromium 版本) 及 Internet Explorer 中，`getSelection()` 对input和textarea元素不起作用。 [`HTMLInputElement.setSelectionRange()`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement/setSelectionRange) 或 `selectionStart` 及 `selectionEnd` 属性可用于解决此问题。

（1）如果想禁用copy操作，可以通过监听copy事件，禁止默认行为

```js
event.preventDefault()
```

（2）如果想获取copy操作的内容，或者对内容进行修改，可以通过监听copy事件，通过其他的对象和方法，对clipBorad系统剪切板进行操作。

如下：

#### 事件event上的clipboardData对象的setData、getData、clearData方法

**copy事件的event继承了ClipboardEvent事件**

```js
bubbles: true   //冒泡
cancelable: true   //能否取消
cancelBubble: false  //取消冒泡
//以上三个属性：可以冒泡、能够取消冒泡、但没有取消冒泡

clipboardData: DataTransfer //clipboardData属性继承DataTransfer对象
composed: true
currentTarget: null
defaultPrevented: false  //阻止默认事件
eventPhase: 0
isTrusted: true
path: (5) [div#wrap, body, html, document, Window] //标签path路径
returnValue: true
srcElement: div#wrap
target: div#wrap   //事件源对象
timeStamp: 2053.404999896884  //时间戳——从监听到该事件，到该事件触发的时间，单位ms
type: "copy"  //事件类型
__proto__: ClipboardEvent //继承的原型对象
```

以上可以看到：

该事件无法获取copy的数据，但是可以通过 `window.getSelection()` 获取选中的数据。

#### IE9、Firefox、Safari、Chrome和Opera支持：window.getSelection()。

但是非chrome浏览器的input和textarea标签，不能通过window.getSelection().toString()方法获取选中的文本。

```js
var wrap = document.getElementById("wrap");
wrap.oncopy = function(event){
    const selectObj = window.getSelection();
    console.log(selectObj.toString())//获取选中的内容
}
```

需要兼容非chrome浏览器的input和textarea元素的选择文本，如下：

#### setSelectionRange 和select方法：选中，页面上有选中效果，而非获取选中的值

**作用：点击按钮复制内容时，页面有选中效果。**



**（1）HTMLInputElement.setSelectionRange  设置选中范围——兼容性IE9** 

**`HTMLInputElement.setSelectionRange`** 方法用于**设定**input或 textarea元素中当前选中文本的起始和结束位置。

该方法比较笨，用于**选中**input或textarea标签的指定index范围的内容。



在较新的浏览器中，你可以通过一个可选的 selectionDirection 来指定文本选中的方向。比如通过点击和拖动从结束位置往起始位置选中一个字符串。

每次调用这个这个方法都会更新 `HTMLInputElement` 的 `selectionStart`, `selectionEnd` 和 `selectionDirection` 属性。

要注意的是，`selectionStart`, `selectionEnd` 属性和 `setSelectionRange` 方法只能应用于input类型为文本、搜索、链接、电话号码和密码的输入。Chrome 从版本 33 开始会在访问其余类型的这些属性和方法时抛出异常。例如，输入类型为数字时会抛出：“不能从'HTMLInputElement'中读取'selectionStart'属性：输入元素的类型('number')不支持选择（Failed to read the 'selectionStart' property from 'HTMLInputElement': The input element's type ('number') does not support selection）”。

**语法：**

```js
element.setSelectionRange(selectionStart, selectionEnd [, selectionDirection]);
```

- `selectionStart`

  被选中的第一个字符的位置索引，从0开始。如果这个值比元素的 `value` 长度还大，则会被看作 `value` 最后一个位置的索引。

- `selectionEnd`

  被选中的最后一个字符的 *下一个* 位置索引。如果这个值比元素的value长度还大，则会被看作value最后一个位置的索引。

- `selectionDirection` 可选

  一个表示选择方向的字符串，可能的值有：

- `"forward"`

- `"backward"`

- `"none"` 默认值，表示方向未知或不相关。

示例：

```js
function selectText() {
  const input = document.getElementById('text-box');
  input.focus();
  input.setSelectionRange(2, 5);

```

（2）如果你希望**全选**输入元素中的文本，你可以使用 [HTMLInputElement.select()](https://wiki.developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/select) 方法。

```js
function selectText() {
  const input = document.getElementById('text-box');
  input.focus();
  input.select();
}
```

当然HTMLInputElement.setSelectionRange也可以**获中**文本的所有内容：

```js
 element.setSelectionRange(0, element.value.length);
```

**TMLInputElement/setSelectionRange**：https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement/setSelectionRange



#### clipboardData系统剪切板——兼容性Edge12

操作系统默认情况下，进行copy、cut、paste操作，都是操作系统的实现。使用浏览器来监听这些事件后，可以通过阻止默认行为，进而无法将操作系统获取的内容存入系统剪切板或从系统剪切板获取内容。

- **浏览器的clipboardData对象存值：**只有在阻止默认行为后，可以将值存入的到系统剪切板上。——在阻止操作系统剪切板默认行为后，可以通过clipboardData对象往系统剪切板存入值。

- **浏览器的clipboardData对象取值：**直接可以从系统剪切板上获取值。

**——在系统阻止默认行为后，clipboardData对象setData方法生效。**

比如：示例中，copy可以存入111到系统剪切板，而cut事件却不可以。

```js
       var wrap = document.getElementById("wrap");
       wrap.oncopy = function(event){
           const selection = document.getSelection();
           event.clipboardData.setData("text/plain", 111)
           event.preventDefault(); //触发warp标签的copy事件时，将111存入系统剪切板
       }
       wrap.oncut = function(event) { 
           const selection = document.getSelection();
           event.clipboardData.setData("text/plain", 111) //由于没有阻止默认行为，无法将111存入系统剪切板
       }
```

**——getData方法可以直接获取系统剪切板的值。**

比如，下面代码可以直接获取系统剪切板的值

```js
       wrap.onpaste = function(event) {
           console.log(event.clipboardData.getData("text/plain"))
       }
```

**解释：**

"text/plain" 是往系统剪切板上添加对应格式的内容。

copy、cut、paste等可以操作剪切板，阻止默认行为后，设置或读取剪切板的内容。

copy复制的内容，默认行为会自动添加到剪切板上。cut剪切的内容，默认行为可编辑的元素内容会被剪切添加到剪切板上，不可编辑的元素内容，仅会触发编辑事件，无法添加到剪切板上。



只有阻止默认行为的情况下，对剪切板上添加新的内容才会生效，特指非编辑元素的cut事件。而copy和paste事件，默认情况下会设置和读取剪切板的数据，其实无需selection。但非编辑的cut事件无法设置剪切板数据。



该事件的默认操作是将当前选择（如果有）复制到系统剪贴板并将其从文档中删除。



此事件的处理程序可以通过调用事件的属性，并使用取消默认操作来*修改*剪贴板内容。

#### clipboardData属性：

https://developer.mozilla.org/en-US/docs/Web/API/ClipboardEvent/clipboardData

The `ClipboardEvent.clipboardData` property holds a [`DataTransfer`](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer) object。clipboardData属性继承了 DataTransfer对象

DataTransfer对象上有：setData、getData、clearData方法

- 指定应该从`cut`和`copy`事件处理程序将哪些数据放入剪贴板，通常是通过[`setData(format, data)`](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer/setData)调用；
- `paste`通常通过[`getData(format)`](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer/getData)调用从事件处理程序中获取要粘贴的数据。

见`cut`，`copy`以及 `paste`获取更多信息的事件文件。



### ClipboardEvent 操作DataTransfer对象的特点：

阻止默认copy cut事件，将值存在系统剪切板上。DataTransfer对象将值传输到系统剪切板上。



### 额外补充

（1）https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer/setData

setData的参数：

```js
setData(format, data)
```

format数据类型为`text/plain`和`text/uri-list`。



(2)可编辑属性：contenteditable，使得标签内容可以被编辑

```html
<div id="wrap" contenteditable="true"></div>
```





### 第三方库：clipboard.js

——实现的是：按钮操作赋值剪切内容



https://github.com/zenorocha/clipboard.js

