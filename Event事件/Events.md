## 浏览器常用事件Events

事件对象上有一些公有的属性，特殊的属性，有的事件对象也是继承别的事件对象。

```html
bubbles: true    是否冒泡
cancelBubble: false  是否取消了冒泡
cancelable: true    是否取消了对该对象的该事件的监听
```

阻止默认行为：event.preventDefault()

取消事件冒泡：

#### 一、页面加载时的事件和页面卸载时的事件

深入完成之前两篇文章。。。

#### 二、鼠标键盘事件

剪切复制粘贴、keydown keypress keyup、鼠标事件、鼠标拖放事件、



1、copy：当用户通过浏览器的用户界面启动复制操作时，将触发 **`copy`** 事件。

https://developer.mozilla.org/zh-CN/docs/Web/API/Window/copy_event  这个是window的copy事件

还有Element的copy事件：https://developer.mozilla.org/en-US/docs/Web/API/Element/copy_event

copy事件对象event中（该事件对象继承了ClipboardEvent）有个clipboardData对象：https://developer.mozilla.org/en-US/docs/Web/API/ClipboardEvent/clipboardData

该对象的原型上有DataTransfer对象，DataTransfer对象的setData方法和getData方法，可以被clipboardData对象所继承使用：

copy内容是浏览器的安全策略的部分，是浏览器自身实现的。copy事件只是监听该事件，但是copy的内容是不可以监听到的。

```html
contenteditable="true"
```

HTML的标签属性，使元素内容可编辑，比如：

```html
<div class="source" contenteditable="true">Try copying text from this box...</div>
```

**直接copy页面内容是怎么做的？**

浏览器操作系统的功能

**防止copy页面内容**

有些网页防止内容被copy，是如何处理的？

Event.preventDefault() 可以阻止事件的默认行为，即防止页面内容被复制。canceling the event's default action using `event.prventDefault()`

https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault

 **Internet Explorer 8 及更早 IE 版本不支持 [addEventListener()](https://www.runoob.com/jsref/met-element-addeventlistener.html) 方法。**

document.getSelection()是什么？

```js
const selection = document.getSelection();
```

参考 ：https://segmentfault.com/q/1010000010177464

https://www.cnblogs.com/qingqingzou-143/p/6702535.html



cut：**`cut`**当用户通过浏览器的用户界面启动“剪切”操作时，将触发该事件。



paste：**`paste`**当用户通过浏览器的用户界面发起“粘贴”操作时，将触发该事件。



keydown：键盘按下键时会触发该事件。与[`keypress`](https://developer.mozilla.org/en-US/docs/Web/API/Document/keypress_event)事件不同`keydown`，所有键都会触发该事件，无论它们是否产生字符值。

https://developer.mozilla.org/en-US/docs/Web/API/Document/keydown_event

keypress：**`keypress`**当按下产生字符值的键时，将触发该事件。产生字符值的键的示例是字母，数字和标点键。不产生字符值的键的例子是修饰键如Alt，Shift，Ctrl，或Meta。

不再推荐**使用**此功能。尽管某些浏览器可能仍支持它，但它可能已经从相关的Web标准中删除，正在被删除或仅出于兼容性目的而保留。避免使用它，并尽可能更新现有代码；请参阅此页面底部的[兼容性表](https://developer.mozilla.org/en-US/docs/Web/API/Document/keypress_event#Browser_compatibility)以指导您做出决定。请注意，此功能可能随时停止起作用。

因此您应该使用`beforeinput`或`keydown`代替

https://developer.mozilla.org/en-US/docs/Web/API/Document/keypress_event

keyup：**`keyup`**释放键时将触发该事件。

https://developer.mozilla.org/en-US/docs/Web/API/Document/keyup_event



MouseEvent：**`MouseEvent`** 接口指用户与指针设备( 如鼠标 )交互时发生的事件。使用此接口的常见事件包括：`click`，`dblclick`，`mouseup`，`mousedown`。

`MouseEvent` 派生自 [`UIEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent)，[`UIEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent) 派生自 [`Event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event)。

https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent



click：`click`当指针位于元素内部时，同时按下并释放定点设备按钮（例如鼠标的主鼠标按钮）时，元素将接收事件。如果在一个元素上按下按钮，并且在释放按钮之前将指针移到该元素之外，则会在包含两个元素的最特定祖先元素上触发该事件。

`click`在`mousedown`和`mouseup`事件都触发后按此顺序触发。

https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event

dblclick：**`dblclick`**双击定点设备按钮（例如鼠标的主按钮）时，将触发该事件。也就是说，在很短的时间内快速单击单个元素两次。

`dblclick`经过两次触发[`click`](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event)事件（并且通过扩展，两双后[`mousedown`](https://developer.mozilla.org/en-US/docs/Web/API/Element/mousedown_event)和[`mouseup`](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseup_event)事件）。

https://developer.mozilla.org/en-US/docs/Web/API/Element/dblclick_event

contextmenu：**`contextmenu`**当用户尝试打开上下文菜单时，将触发该事件。通常，通过单击鼠标右键或按上下文菜单键来触发此事件。在后一种情况下，上下文菜单显示在焦点元素的左下角，除非该元素是树，在这种情况下，上下文菜单显示在当前行的左下角。

任何未禁用的右键单击事件（通过调用事件的[`preventDefault()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)方法）将导致在`contextmenu`目标元素上触发事件。

https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event

mousedown：当指针位于元素内部时，按下定点设备按钮时将**`mousedown`**触发该事件[`Element`](https://developer.mozilla.org/en-US/docs/Web/API/Element)。

https://developer.mozilla.org/en-US/docs/Web/API/Element/mousedown_event

mouseup：当指针在元素中时， `mouseup`事件在指针设备（如鼠标或触摸板）按钮放开时触发。`mouseup` 事件与[`mousedown`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/mousedown_event) 事件相反

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseup_event

mouseenter：鼠标进入

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event

mouseleave：鼠标离开

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseleave_event

mousemove：鼠标在元素上移动时触发

https://developer.mozilla.org/en-US/docs/Web/API/Element/mousemove_event

mouseover：鼠标移到元素或其子元素素时

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseover_event

mouseout：鼠标移出该元素或其子元素时

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/mouseout_event

wheel：滚轮事件，当滚动鼠标滚轮或操作其它类似输入设备时会触发**滚轮事件**。滚轮事件替换了已被弃用的非标准[`mousewheel`](https://developer.mozilla.org/zh-CN/docs/Web/API/Mousewheel)事件。

拖放事件：最好还是用插件，compatibility还可以啊

drag：当元素或者选择的文本被拖动时触发 `drag` 事件 (每几百毫秒触发一次)。在此过程中持续触发，每350ms触发一次

https://developer.mozilla.org/en-US/docs/Web/API/Document/drag_event

dragstart：当用户开始拖动一个元素或者一个选择文本的时候 `dragstart` 事件就会触发

https://developer.mozilla.org/en-US/docs/Web/API/Document/dragstart_event

dragend：拖放事件在拖放操作结束时触发(通过释放鼠标按钮或单击escape键)

https://developer.mozilla.org/en-US/docs/Web/API/Document/dragend_event

dragenter：当拖动的元素或被选择的文本进入有效的放置目标时， `dragenter` 事件被触发。

https://developer.mozilla.org/en-US/docs/Web/API/Document/dragenter_event

dragleave：当一个被拖动的元素或者被选择的文本离开一个有效的拖放目标时，将会触发`dragleave` 事件。

https://developer.mozilla.org/en-US/docs/Web/API/Document/dragleave_event

dragover：当元素或者选择的文本被拖拽到一个有效的放置目标上时，触发 `dragover `事件(每几百毫秒触发一次)。

这个事件在可被放置元素的节点上触发。在此过程中持续触发，每350ms触发一次

https://developer.mozilla.org/en-US/docs/Web/API/Document/dragover_event

放下的事件：drop

**`当一个元素或是选中的文字被拖拽释放到一个有效的释放目标位置时，drop`** 事件被抛出。



#### 三、CSS事件

#### 四、表单事件

submit：当表单提交的时候触发submit事件。注意submit事件只能作用于form元素，不能作用于button或者<input type="submit">

reset：当表单被重置时触发`reset`事件

以上都是html5事件，支持

#### 五、输入框事件

input事件

change事件

invalid事件：值的检查时间

https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement/invalid_event

聚焦离焦：

focus：focus事件在元素获取焦点时触发. 这个事件和 [`focusin`](https://developer.mozilla.org/en-US/docs/Mozilla_event_reference/focusin) 最大的区别仅仅在于后者会事件冒泡.

blur：当一个元素失去焦点的时候 blur 事件被触发。它和 [`focusout`](https://developer.mozilla.org/en-US/docs/Mozilla_event_reference/focusout) 事件的主要区别是 focusout 支持冒泡。

focusin

focusout



媒体事件——音视频

进度条事件——上传下载资源



浏览器window事件：

resize：文档视图调整大小时会触发 **resize** 事件。由于resize事件可以以较高的速率触发, 因此事件处理程序不应该执行计算开销很大的操作

scroll：文档视图或者一个元素在滚动时，会触发元素的**`scroll`**事件。

hashchange：当URL的片段标识符更改时，将触发**hashchange**事件 (跟在＃符号后面的URL部分，包括＃符号)

https://developer.mozilla.org/en-US/docs/Web/API/Window/hashchange_event

#### 额外

MDN not Found页面：https://developer.mozilla.org/zh-CN/docs/Web/Reference/Events/auxclick

实现B站的视频播放功能；

localStorage

cookie、session、token

