# EventTarget

**EventTarget**是一个由对象实现的DOM接口，这些对象可以接收事件，并可能有针对事件的监听器。

Element、Document、Window是最常见的事件目标，但是其他对象也可以是事件目标。例如XMLHttpRequest、AudioNode、AudioContext等

许多事件目标(包括Element、Document和Window)也支持通过onevent属性和属性设置事件处理程序。



### EventTarget.addEventListener()

**兼容性：**兼容IE9。旧版本的IE（IE6——IE11）支持一个等价的、专有的eventtarget.dethevent()方法。

EventTarget方法addEventListener()设置了一个函数，当指定的事件被传递到目标时，该函数将被调用。常见的目标是元素、文档和窗口，但是目标可以是支持事件的任何对象(如XMLHttpRequest)。

addEventListener()通过为调用它的EventTarget上的指定事件类型的事件监听器列表添加实现EventListener的函数或对象来工作。

**语法：**

```js
target.addEventListener(type, listener [, useCapture]);
```

**参数：**

type：事件类型的字符串

listener：当所监听的事件类型触发时，会接收到一个事件通知（实现了 [`Event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event) 接口的对象）对象。`listener` 必须是一个实现了 [`EventListener`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventListener) 接口的对象，或者是一个[函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions)。

`useCapture` 可选

事件是否捕获，默认是false（冒泡）如果是true是捕获。

[`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Boolean)，在DOM树中，注册了listener的元素， 是否要先于它下面的EventTarget，调用该listener。 当useCapture(设为true) 时，沿着DOM树向上冒泡的事件，不会触发listener。当一个元素嵌套了另一个元素，并且两个元素都对同一事件注册了一个处理函数时，所发生的事件冒泡和事件捕获是两种不同的事件传播方式。事件传播模式决定了元素以哪个顺序接收事件。进一步的解释可以查看 [事件流](http://www.w3.org/TR/DOM-Level-3-Events/#event-flow) 及 [JavaScript Event order](http://www.quirksmode.org/js/events_order.html#link4) 文档。 如果没有指定， `useCapture` 默认为 false 。



### EventTarget.dispatchEvent

**兼容性：**兼容IE9。注意旧版本的IE（IE6——IE11）支持一个相同的方法——EventTarget.fireEvent()

向一个指定的事件目标派发一个[事件](https://developer.mozilla.org/zh-CN/docs/Web/API/Event), 并以合适的顺序**同步调用**目标元素相关的事件处理函数。标准事件处理规则(包括事件捕获和可选的冒泡过程)同样适用于通过手动的使用`dispatchEvent()`方法派发的事件。

**注意：**与由DOM触发并通过事件循环异步调用事件处理程序的“本机”事件不同，dispatchEvent()是同步调用事件处理程序的。在调用dispatchEvent()之后，所有适用的事件处理程序将在代码继续之前执行并返回。

dispatchEvent()是创建-初始化-分派流程的最后一步，它用于将事件分派到实现的事件模型中。可以使用事件构造函数创建事件。

https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/dispatchEvent



### EventTarget.removeEventListener()

**兼容性：**兼容IE9，旧版本的IE（IE6——IE11）支持一个等价的、专有的Eventtarget.dethevent()方法。

移除使用 [`EventTarget.addEventListener()`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener) 方法添加的事件。使用事件类型，事件侦听器函数本身，以及可能影响匹配过程的各种可选择的选项的组合来标识要删除的事件侦听器。

添加事件或者是对某个事件进行监听

**语法：对应移除**

```js
target.removeEventListener(type, listener[, useCapture]);
```

https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/removeEventListener



### Creating and triggering events

本文演示了如何创建和分派DOM事件。这些事件通常称为**合成事件**，而不是浏览器本身触发的事件。

#### Creating custom event（创建自定义事件）

（1）Event构造函数——兼容性Edge12

事件可以通过Event构造函数创建一个自定义事件

```js
const event = new Event('build');
// Listen for the event.
elem.addEventListener('build', function (e) { /* ... */ }, false);
// Dispatch the event.
elem.dispatchEvent(event);
```

（1）document.createEvent() 和 Event.initEvent() 

由document.createEvent()方法创建一个event实例，实例调用initEvent方法创建自定义事件。

```js
    var customEvent = document.createEvent('Event');
    // Define that the event name is 'build'.
    customEvent.initEvent('build', true, true);
```

initEvent的兼容性IE11

event.initevent()方法用于初始化使用Document.createEvent()创建的事件的值。

语法：

```js
event.initEvent(type, bubbles, cancelable);
```

type：自定义的事件类型，字符串值

bubbles：是一个布尔值，决定事件是否应该在事件链中向上冒泡。一旦设置，只读属性事件。泡沫将赋予它价值。

cancelable：是一个布尔值，定义是否可以取消事件。一旦设置，只读属性事件。cancelable会给出它的值。



在Firefox 17之前，在事件分派之后调用这个方法会引发异常，而不是什么都不做。

**Deprecated：**不推荐使用此功能。尽管一些浏览器可能仍然支持它，但它可能已经从相关的web标准中删除，可能正在被删除的过程中，或者可能只是为了兼容而保留。避免使用它，并在可能的情况下更新现有代码;请参阅本页底部的兼容性表，以指导您的决定。请注意，此功能可能在任何时候停止工作。

https://developer.mozilla.org/en-US/docs/Web/API/Event/initEvent



自定义事件：CustomEvent.initCustomEvent 

https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/initCustomEvent





https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events

