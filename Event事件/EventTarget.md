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

**向一个指定的事件目标派发一个事件实例对象**， 并以合适的顺序**同步调用**目标元素相关的事件处理函数。标准事件处理规则(包括事件捕获和可选的冒泡过程)同样适用于通过手动的使用`dispatchEvent()`方法派发的事件。

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



### Creating and triggering events——创建和触发事件

本文演示了如何创建和分派DOM事件。这些事件通常称为**合成事件**，而不是浏览器本身触发的事件。

**浏览器对自定义事件的发展如下：**

兼容性如下，虽然浏览器的发展还保留了旧的方法，但标准上已经弃用了旧方法

CustomEvent.initCustomEvent方法（IE9——IE11）——> Event.initEvent方法（IE11）——CustomEvent构造函数（Edge12——Edge18）——Event构造函数（Edge12）

#### 1、document.createEvent() 结合 CustomEvent.initCustomEvent——兼容性IE9

**CustomEvent.initCustomEvent()**方法初始化CustomEvent对象。如果事件已经被分派，则此方法不执行任何操作。

以这种方式初始化的事件必须是用Document.createEvent()方法创建的。需要注意createEvent方法可以创建哪些类型的事件，请在Document文档中查看对createEvent方法的介绍。

**deprecated 废弃：**不要再使用这个方法，因为它已被弃用。

**注意：**与其使用该特性，不如使用特定的事件构造函数，如CustomEvent()。关于创建和触发事件的页面提供了关于如何使用这些事件的更多信息。

**使用：**

```js
        var wrap = document.getElementsByClassName('wrap')[0];
        var customEvent = document.createEvent('CustomEvent'); //指定事件接口类型
        customEvent.initCustomEvent('build', false, false, null); //注意：只有CustomEvent上有initCustomEvent方法
        console.log(customEvent)

        wrap.addEventListener('build', function (e) {
            console.log(e);
        }, false);

       document.querySelector('input').onfocus = function(){
        wrap.dispatchEvent(customEvent);
       }
```

**上述代码：**如果document.createEvent必须指定CustomEvent对象，得到的CustomEvent对象上的原型上有initCustomEvent 方法。如果指定的是其他事件接口类型，没有initCustomEvent方法。

得到的customEvent事件实例对象：

```
CustomEvent : {
	bubbles: false
	cancelBubble: false
	cancelable: false
	composed: false
	currentTarget: null
	defaultPrevented: false
	detail: null
	eventPhase: 0
	isTrusted: false
	path: []
	returnValue: true
	srcElement: null
	target: null
	timeStamp: 8.550000027753413
	type: "build"
	__proto__: CustomEvent
}
```

**语法：**

```js
event.initCustomEvent(type, canBubble, cancelable, detail);
```

> type：事件类型，任意自定义的事件类型。类似click等事件
>
> canBubble：能否可以冒泡，默认false
>
> cancelable：是否取消冒泡，默认false
>
> detail：事件初始化时传入的数据

**Chrome：**canBubble、cancelable和detail是可选参数，默认值分别为false、false和null。

地址：https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/initCustomEvent



#### 2、document.createEvent() 结合 Event.initEvent() ——initEvent方法的兼容性IE11

由document.createEvent()方法创建一个Event接口事件实例，实例调用initEvent方法创建自定义事件。

```js
    var customEvent = document.createEvent('Event');
    // Define that the event name is 'build'.
    customEvent.initEvent('build', true, true);
```

event.initevent()方法用于初始化使用Document.createEvent()创建的事件的值。

语法：

```js
event.initEvent(type, bubbles, cancelable);
```

> type：自定义的事件类型，字符串值
>
> bubbles：是一个布尔值，决定事件是否应该在事件链中向上冒泡。一旦设置，只读属性事件。泡沫将赋予它价值。
>
> cancelable：是一个布尔值，定义是否可以取消事件。一旦设置，只读属性事件。cancelable会给出它的值。



在Firefox 17之前，在事件分派之后调用这个方法会引发异常，而不是什么都不做。

**Deprecated：**不推荐使用此功能。尽管一些浏览器可能仍然支持它，但它可能已经从相关的web标准中删除，可能正在被删除的过程中，或者可能只是为了兼容而保留。避免使用它，并在可能的情况下更新现有代码;请参阅本页底部的兼容性表，以指导您的决定。请注意，此功能可能在任何时候停止工作。

https://developer.mozilla.org/en-US/docs/Web/API/Event/initEvent



#### 3、CustomEvent()——兼容性（Edge12——Edge18）

构造方法 CustomerEvent() 创建一个新的 [`CustomEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/CustomEvent) 对象。

**语法：**

```js
event = new CustomEvent(type, customEventInit);
```

> type：一个表示 event 名字的字符串，类似click
>
> customEventInit：一个对象，
>
> {
>
>   bubbles 一个布尔值，表示该事件能否冒泡。注意：chrome默认为不冒泡。
>
>   cancelable 一个布尔值，表示该事件是否可以取消。
>
>   detail：可选的默认值是 null 的任意类型数据，是一个与 event 相关的值
>
> }

**深入探讨customEventInit的参数：**

chrome浏览器默认不设置bubbles，值为false，不冒泡。其他浏览器呢？

detail作为事件对象上的属性，可以是任意值。

**使用：**detail可以是任意值，示例中是一个对象。

```js
        var wrap = document.getElementsByClassName('wrap')[0];
        var customevent = new CustomEvent('build', {
            bubbles: false,
            cancelable: false,
            detail: {
                name: "zhu",
                age: 25
            }
        })
        wrap.addEventListener('build', function(event){
            console.log(event);
        })
        document.body.onclick = function(){
            wrap.dispatchEvent(customevent)
        }
```

**打印结果：注意detail的值，以及bubbles和cancelable值**

```json
{
    bubbles: false
    cancelBubble: false
    cancelable: false
    composed: false
    currentTarget: null
    defaultPrevented: false
    detail: {name: "zhu", age: 25}
    eventPhase: 0
    isTrusted: false
    path: (5) [div.wrap, body, html, document, Window]
    returnValue: true
    srcElement: div.wrap
    target: div.wrap
    timeStamp: 8.344999980181456
    type: "build"
    __proto__: CustomEvent
}
```



https://developer.mozilla.org/zh-CN/docs/Web/API/CustomEvent/CustomEvent



#### 4、Event()——兼容性（Edge12）

**Event()** 构造函数, 创建一个新的事件对象Event。

语法：

```js
event = new Event(type, eventInit);
```

> type：一个表示 event 名字的字符串，类似click
>
> eventInit：一个对象
>
> {
>
> bubbles：可选，默认值为 `false`，表示该事件是否冒泡。
>
> cancelable：可选，默认值为 `false`， 表示该事件能否被取
>
> composed：可选，默认值为 `false`，指示事件是否会在影子DOM根节点之外触发侦听器。
>
> }

事件可以通过Event构造函数创建一个自定义事件

```js
        var wrap = document.getElementsByClassName('wrap')[0];
        var customevent = new Event('build',{
            bubbles: true,
            cancelable: true,
            composed: false
        })
        wrap.addEventListener('build', function(event){
            console.log(event);
        })
        document.onclick = function(){
            wrap.dispatchEvent(customevent);
        }
```

打印结果：注意composed值。

```json
{
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
    timeStamp: 7.5400000205263495
    type: "build"
    __proto__: Event
}
```

https://developer.mozilla.org/zh-CN/docs/Web/API/Event/Event



#### 总结如下：

- 添加自定义事件数据data，使用CustomEvent()构造函数，其中的detail可以设置数据。

- 创建自定义事件的旧方式，documen.createEvent() 结合 CustomEvent.initCustomEvent()方法或Event.initEvent()方法

- ES6以后推荐使用Event()构造函数来创建自定义事件，不兼容IE，支持Edge12

- 使用EventTarget对象上的addEventListener方法进行监听和dispatchEvent方法触发事件



https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events

