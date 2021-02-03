# Event

**`Event`** 接口表示在 DOM 中出现的事件。

一些事件是由用户触发的，例如鼠标或键盘事件；而其他事件常由 API 生成，例如指示动画已经完成运行的事件，视频已被暂停等等。事件也可以通过脚本代码触发，例如对元素调用 `HTMLElement.click()` 方法，或者定义一些自定义事件，再使用 `EventTarget.dispatchEvent()` 方法将自定义事件派发往指定的目标（target）。

有许多不同类型的事件，其中一些使用基于 `Event` 主接口的二次接口。`Event` 本身包含适用于所有事件的属性和方法。

很多DOM元素可以被设计接收(或者监听) 这些事件, 并且执行代码去响应（或者处理）它们。通过`EventTarget.addEventListener()`方法可以将事件处理函数绑定到不同的[HTML elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)上 (比如`<button>`, `<div>`, `<span>`等等) 。这种绑定事件处理函数的方式基本替换了老版本中使用HTML [event handler attributes](https://developer.mozilla.org/en-US/docs/HTML/Global_attributes)来绑定事件处理函数的方式。除此之外，通过正确使用[`removeEventListener()`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)方法，这些事件处理函数也能被移除。

**Note:** 一个元素可以绑定多个事件处理函数，甚至是同一种类型的事件。尤其是这种分离的，并且相互独立的代码模块对同一个元素绑定事件处理函数，每一个模块代码都有着独立的目的。（比如，一个网页同时有着广告模块和统计模块同时监听视频播放元素）

当有很多嵌套的元素，并且每一个元素都有着自己的事件处理函数，事件处理过程会变得非常复杂。尤其当一个父元素和子元素绑定有相同类型的事件处理函数的时候。因为结构上的重叠，事件处理函数可能会依次被触发，触发的顺序取决于[事件冒泡和事件捕获](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#Event_bubbling_and_capture)在每一个元素上的设置情况。



### 基于Event的接口

下面是主要基于`Event`接口的接口列表，每一个接口都设置了指向各自的MDN API说明的文档链接。需要注意的是，所有的事件接口名称都是以“Event”结尾的。

- [`ClipboardEvent`](https://developer.mozilla.org/en-US/docs/Web/API/ClipboardEvent)
- [`CustomEvent`](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent)
- [`DragEvent`](https://developer.mozilla.org/en-US/docs/Web/API/DragEvent)
- [`ErrorEvent`](https://developer.mozilla.org/en-US/docs/Web/API/ErrorEvent)
- [`MouseEvent`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent)
- [`UIEvent`](https://developer.mozilla.org/en-US/docs/Web/API/UIEvent)
- [`WheelEvent`](https://developer.mozilla.org/en-US/docs/Web/API/WheelEvent)



#### Event()构造函数

Event()构造函数创建新的Event事件。



#### Event上的常见属性

```json
bubbles: true
cancelBubble: false
cancelable: true
composed: false
currentTarget: null
defaultPrevented: false
eventPhase: 0
isTrusted: false
path: (5) [div.wrap, body, html, document, Window]
returnValue: true
srcElement: div.wrap
target: div.wrap
timeStamp: 6.624999921768904
type: "build"
```

**属性都是只读的**

[`Event.bubbles`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/bubbles)    一个布尔值，用来表示该事件是否会在 DOM 中冒泡。

[`Event.cancelBubble`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/cancelBubble)   

[`Event.stopPropagation()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopPropagation) 的历史别名。在事件处理器函返回之前，将此属性的值设置为 `true`，亦可阻止事件继续冒泡。

[`Event.cancelable`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/cancelable)   一个布尔值，表示事件是否可以取消。

[`Event.composed`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/composed)   一个布尔值，表示事件是否可以穿过 Shadow DOM 和常规 DOM 之间的隔阂进行冒泡。

[`Event.deepPath`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/deepPath)   一个由事件流所经过的 DOM [`节点`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)组成的[`数组`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)。

[`Event.defaultPrevented`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/defaultPrevented)   一个布尔值，表示 [`event.preventDefault()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/preventDefault) 方法是否取消了事件的默认行为。

[`Event.eventPhase`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/eventPhase)     表示事件流正被处理到了哪个阶段。

[`Event.returnValue`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/returnValue)      旧版 Internet Explorer 引入的一个非标准历史属性，为保证依赖此属性的网页正常运作，此属性最终被收入规范。可用 [`Event.preventDefault()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/preventDefault) 与 [`Event.defaultPrevented`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/defaultPrevented) 代替，但由于已进入规范，也可以使用此属性。

[`Event.timeStamp`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/timeStamp)   事件创建时的时间戳（精度为毫秒）。按照规范，这个时间戳是 Unix 纪元起经过的毫秒数，但实际上，在不同的浏览器中，对此时间戳的定义也有所不同。另外，规范正在将其修改为 [`DOMHighResTimeStamp`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMHighResTimeStamp)。

[`Event.target`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/target)    对事件原始目标的引用，这里的原始目标指最初派发（dispatch）事件时指定的目标。

[`Event.type`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/type)    事件的类型，不区分大小写。

[`Event.isTrusted`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/isTrusted)    表示事件是由浏览器（例如用户点击）发起的，还是由脚本（使用事件创建方法，例如 [`Event.initEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/initEvent)）发出的。



#### Event方法

[`event.initEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/initEvent)

为通过 `document.createEvent()` 创建的事件初始化。该方法对已经被派发的事件无效。

[`event.preventDefault`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/preventDefault)

取消事件（如果该事件可取消）。

[`event.stopPropagation`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopPropagation)

停止冒泡，阻止事件在 DOM 中继续冒泡。



Event地址：https://developer.mozilla.org/en-US/docs/Web/API/Event