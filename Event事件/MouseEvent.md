# MouseEvent：

### click、dblclick、

### mousedown、mouseup、mouseenter、mouseleave、mouseover、mouseout、mousemove、contextmenu



### 一、MouseEvent事件

地址：https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent

**`MouseEvent`** 接口指用户与指针设备( 如鼠标 )交互时发生的事件。使用此接口的常见事件包括：`click`，`dblclick`，`mouseup`，`mousedown`。

`MouseEvent` 派生自 [`UIEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent)，[`UIEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent) 派生自 [`Event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event)。

虽然 `MouseEvent.initMouseEvent() `方法保持向后兼容性，但是应该使用 `MouseEvent()` 构造函数创建一个 `MouseEvent` 对象。

一些具体的事件都派生自 `MouseEvent`：[`WheelEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/WheelEvent) 和[`DragEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/DragEvent)。

#### 属性：以下属性兼容IE9



#### 点击事件定位坐标

- 屏幕[`screenX`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/screenX)只读、屏幕[`screenY`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/screenY)只读

鼠标指针相对于全局（屏幕）的X Y坐标；



- 客户端[`clientX`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/clientX)只读、客户端[`clientY`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/clientY)只读

**`MouseEvent.clientX`** 是只读属性， 它提供事件发生时的应用客户端区域的水平坐标 (与页面坐标不同)。例如，不论页面是否有水平滚动，当你点击客户端区域的左上角时，鼠标事件的 `clientX` 值都将为 0 。



- 文档[`pageX`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/pageX)只读、文档[`pageY`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/pageY)只读

鼠标指针相对于整个文档的X Y坐标；

 `pageX` 返回的相对于整个文档的x（水平）坐标以像素为单位的只读属性。

这个属性将基于文档的边缘，考虑任何页面的水平方向上的滚动。举个例子，如果页面向右滚动 200px 并出现了滚动条，这部分在窗口之外，然后鼠标点击距离窗口左边 100px 的位置，pageX 所返回的值将是 300。

- 元素内边距 [`offsetX`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/offsetX)只读、元素内边距[`offsetY`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/offsetY)只读

规定了事件对象与目标节点的padding边缘（padding edge）在 X Y 轴方向上的偏移量。



#### [`button`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/button)只读

**`MouseEvent.button`**是只读属性，它返回一个值，代表用户按下并触发了事件的鼠标按键。

这个属性只能够表明在触发事件的单个或多个按键按下或释放过程中哪些按键被按下了。因此，它对判断`mouseenter`, `mouseleave`, `mouseover`, `mouseout` `mousemove`这些事件并不可靠。

用户可能会改变鼠标按键的配置，因此当一个事件的**`MouseEvent.button`**值为0时，它可能不是由物理上设备最左边的按键触发的。但是对于一个标准按键布局的鼠标来说就会是左键。

**注意：**[`MouseEvent.buttons`](https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent/buttons) 属性可指示任意鼠标事件中鼠标的按键情况，因此不要把它和MouseEvent.button属性弄混淆了。

**返回值：**

一个数值，代表按下的鼠标按键：

- `0`：主按键，通常指鼠标左键或默认值（译者注：如document.getElementById('a').click()这样触发就会是默认值）
- `1`：辅助按键，通常指鼠标滚轮中键
- `2`：次按键，通常指鼠标右键
- `3`：第四个按钮，通常指浏览器后退按钮
- `4`：第五个按钮，通常指浏览器的前进按钮

对于配置为左手使用的鼠标，按键操作将正好相反。此种情况下，从右至左读取值。

#### [`which`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/which) 只读

**非标准** ：该特性是非标准的，请尽量不要在生产环境中使用它！

只读属性 **MouseEvent.which** 显示了鼠标事件是由哪个鼠标按键被按下所触发的。其他获得该信息的标准属性是 [`MouseEvent.button`](https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent/button) 与 [`MouseEvent.buttons`](https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent/buttons) 。

**返回值：**

表示一个特定按键的数字：

- `0`: 无
- `1`: 左键
- `2`: 中间滚轮（如果有的话）
- `3`: 右键

如果鼠标被设置为适用于左利手人士使用，那么引发的动作恰好相反。在这种情况下，该值应该从右往左看。



#### [`buttons`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/buttons) 只读

当鼠标事件触发的时，如果多个鼠标按钮被按下（如果有的话），将会返回一个或者多个代表鼠标按钮的数字。

只读属性**`MouseEvent.buttons`**`指示事件触发时哪些鼠标按键被按下。`

每一个按键都用一个给定的数（见下文）表示。如果同时多个按键被按下，buttons 的值为各键对应值做与计算（+）后的值。例如，如果右键（2）和滚轮键（4）被同时按下，buttons 的值为 2 + 4 = 6。

**注意：**属性 MouseEvent.button 和 MouseEvent.buttons 是不同的。MouseEvent.buttons 可指示任意鼠标事件中鼠标的按键情况，而 MouseEvent.button 只能保证在由按下和释放一个或多个按键时触发的事件中获得正确的值。

**返回值：**

一个数字，用来标识鼠标按下的一个或者多个按键。如果按下的键为多个，则值等于所有按键对应数值进行或(|)运算的结果。

- `0 ` : 没有按键或者是没有初始化
- `1 ` : 鼠标左键
- `2 ` : 鼠标右键
- `4 ` : 鼠标滚轮或者是中键
- `8 ` : 第四按键 (通常是“浏览器后退”按键)
- `16` : 第五按键 (通常是“浏览器前进”)



#### [`altKey`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/altKey)只读、[`ctrlKey`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/ctrlKey)只读、[`shiftKey`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/shiftKey)只读、[`metaKey`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/metaKey)只读

**`MouseEvent.altKey`** ：当鼠标事件触发时，如果`Alt键 `被按下，则返回 true，否则返回false。

**`MouseEvent.ctrlKey`**：当鼠标事件触发时，如果`Ctrl键` 被按下，则返回 true，否则返回false。

**`MouseEvent.shiftKey` **：当鼠标事件触发时，如果`Shift键` 被按下，则返回 true，否则返回false。

**`MouseEvent.metaKey`** ：当鼠标事件触发时，如果`Meta键` 被按下，则返回 true，否则返回false。

**备注：**在 MAC 键盘上，表示 Command 键（⌘），在 Windows键盘上，表示 Windows 键（⊞）。



### 二、click事件和dblclick事件

#### 1、click事件

地址：https://developer.mozilla.org/zh-CN/docs/Web/API/Element/click_event

当定点设备的按钮（通常是鼠标左键）在一个元素上被按下和放开时，`click`事件就会被触发。

特点：必须在目标元素上按下鼠标，必须在目标元素上抬起鼠标键，抬起时触发click事件，且坐标位置是鼠标抬起时的位置。

**bug**

Internet Explorer 8 & 9存在一个漏洞，具有经[`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color)样式计算为[`transparent`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#transparent_keyword)的元素覆盖在其它元素顶端时，不会收到`click`事件。取而代之，所有`click`事件将被触发于其底下的元素。参见[this live example](http://jsfiddle.net/YUKma/show/)样例。

已知会触发此漏洞的情景：

- 仅对于IE9：
  - 设置`background-color: rgba(0,0,0,0)`
  - 设置`opacity: 0` 并且明确指定[`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color)而不是[`transparent`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#transparent_keyword)
- 对于IE8和IE9：设置`filter: alpha(opacity=0);`并且明确指定[`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color)而不是[`transparent`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#transparent_keyword)

safari手机版会有一个bug，当点击事件不是绑定在交互式的元素上（比如说HTML的div），并且也没有直接的事件监听器绑定在他们自身。可以戳 [链接](http://jsfiddle.net/cvrhulu/k9t0sdnf/show/) 查看演示。也可以看 [Safari 的可点击元素](https://developer.apple.com/library/safari/documentation/appleapplications/reference/safariwebcontent/HandlingEvents/HandlingEvents.html#//apple_ref/doc/uid/TP40006511-SW6) 和 [点击元素的定义](https://developer.apple.com/library/safari/documentation/appleapplications/reference/safariwebcontent/HandlingEvents/HandlingEvents.html#//apple_ref/doc/uid/TP40006511-SW7).

解决方法如下：

- 为其元素或者祖先元素，添加cursor: pointer的样式，使元素具有交互式点击
- 为需要交互式点击的元素添加`onclick="void(0)"的属性，但并不包括body元素`
- `使用可点击元素如<a>,代替不可交互式元素如div`
- 不使用click的事件委托。

Safari 手机版里，以下元素不会受到上述bug的影响：

- <a> 需要href链接
- <area> 需要href
- <button>
- <img>
- <input>
- <label> 需要与form控制器连接
- 这份清单并不完整，你可以帮助MDN做扩展

#### 2、bdlclick事件  兼容性IE11

地址：https://developer.mozilla.org/en-US/docs/Web/API/Element/dblclick_event

在单个元素上单击两次鼠标的指针设备按钮 (通常是小鼠的主按钮) 时, 将触发 `dblclick` 事件。

示例：

```css
aside {
  background: #fe9;
  border-radius: 1em;
  display: inline-block;
  padding: 1em;
  transform: scale(.9);
  transform-origin: 0 0;
  transition: transform .6s;
  user-select: none;
}

.large {
  transform: scale(1.3);
}
```



```html
<aside>
  <h3>My Card</h3>
  <p>Double click to resize this object.</p>
</aside>

<script>
const card = document.querySelector('aside');

card.addEventListener('dblclick', function (e) {
  card.classList.toggle('large');
});
</script>
```

### mouse事件



#### 1、mousedown和mouseup事件 兼容性IE9

**mousedown**

当指针在元素内部时，按下指向设备的按钮时，将在元素上触发mousedown事件。

注意：这与点击事件的不同之处在于，点击是在完全点击动作发生后触发的；也就是说，鼠标按钮被按下并释放，而指针保持在同一个元素内。mousedown在按钮最初被按下时被触发。

https://developer.mozilla.org/en-US/docs/Web/API/Element/mousedown_event

**mouseup**

当指向设备(如鼠标或触控板)上的按钮被释放，而指针位于其中时，mouseup事件在元素上被触发。mouseup事件与mousedown事件对应。

mouseup只监听鼠标抬起时所在的元素和位置，不管鼠标在哪个元素下按下，当移动鼠标到指定元素上抬起时，都会触发该指定元素的mouseup事件。

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseup_event



#### 2、mouseenter和mouseleave事件  兼容性IE5.5  不冒泡

**mouseenter  鼠标移入元素**



https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event



**mouseleave  鼠标移出元素**

 

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseleave_event

**结合其对称事件, `mouseleave`, mouseenter DOM事件的行为方式与CSS [`:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover) 伪类非常相似。**

由于不冒泡，当鼠标移入或移出 父元素的可见视图时，才会触发mouseenter和mouseleave事件。

#### 3、mouseover和mouseout  mousemove事件  兼容性IE9  冒泡

**mouseover鼠标移至**

当鼠标移至元素上时触发

https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseover_event

**mouseout** 

当鼠标移出

由于冒泡，不管子元素在哪里，视图效果是否在父元素上，当移入或移除子元素时，都会触发父级的mouseover和mouseout事件

**mousemove**

当鼠标在元素上移动时，触发mousemove事件



由于冒泡，当鼠标在子元素上移动时，也会触发父元素的mousemove事件。

https://developer.mozilla.org/en-US/docs/Web/API/Element/mousemove_event



#### 4、contextmenu事件  兼容性IE9 冒泡

当用户试图打开上下文菜单时，触发contextmenu事件。此事件通常由单击鼠标右键或按下上下文菜单键触发。在后一种情况下，上下文菜单显示在焦点元素的左下角，除非元素是树，在这种情况下，上下文菜单显示在当前行的左下角。

任何未禁用的右键单击事件(通过调用事件的preventDefault()方法)都将导致在目标元素上触发contextmenu事件。



https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event



#### 5、滚轮事件WheelEvent 兼容性IE9

**WheelEvent** 接口表示用户滚动鼠标滚轮或类似输入设备时触发的事件。

API接口继承：WheelEvent——MouseEvent——UIEvent——Event

**属性：**该API接口继承了父接口的属性

[`WheelEvent.deltaX`](https://developer.mozilla.org/zh-CN/docs/Web/API/WheelEvent/deltaX) 只读

返回`double`值，该值表示滚轮的横向滚动量。

[`WheelEvent.deltaY`](https://developer.mozilla.org/zh-CN/docs/Web/API/WheelEvent/deltaY) 只读

返回`double`值，该值表示滚轮的纵向滚动量。

[`WheelEvent.deltaZ`](https://developer.mozilla.org/zh-CN/docs/Web/API/WheelEvent/deltaZ) 只读

返回`double`值，该值表示滚轮的z轴方向上的滚动量。

**方法：**WheelEvent本身没有新增方法，方法继承他的父接口。

https://developer.mozilla.org/zh-CN/docs/Web/API/WheelEvent

#### wheel 滚轮事件

当用户旋转指向设备(通常是鼠标)上的滚轮按钮时，将触发滚轮事件。

此事件取代了非标准的弃用mousewheel事件。

**注意：**不要混淆`滚轮事件wheel`和`滚动事件scroll`。wheel事件的默认操作是特定于实现的，并不需要分派滚动事件。即使如此，wheel事件中的delta值也不一定反映内容的滚动方向。因此，不要依赖wheel事件的delta*属性来获取滚动方向。相反，在滚动事件中检测目标的scrollLeft和scrollTop值的变化。

**注意事项：** 请勿想当然依据滚轮方向（即该事件的各delta属性值）来推断文档内容的滚动方向，因标准未定义滚轮事件具体会引发什么样的行为，引发的行为实际上是各浏览器自行定义的。即便滚轮事件引发了文档内容的滚动行为，也不表示滚轮方向和文档内容的滚动方向一定相同。因而通过该滚轮事件获知文档内容滚动方向的方法并不可靠。要获取文档内容的滚动方向，可在文档内容滚动事件（`scroll`）中监视[`scrollLeft`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollLeft)和[`scrollTop`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollTop)二值变化情况，即可推断出滚动方向了。

MDN中文文档写的比较详细，具体的请查看该文档。。（未完待续）

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/wheel_event

示例：滚轮缩放元素

注意：Internet Explorer仅通过addEventListener暴露wheel事件；DOM对象上没有onwheel属性。



#### scroll 滚动事件 兼容性IE9

文档视图或者一个元素在滚动时，会触发元素的**`scroll`**事件。

**注意：**在 iOS UIWebViews中， 滚动进行时不会触发 `scroll` 事件；只有当滚动结束后事件才会被触发。参见 [Bootstrap issue #16202](https://github.com/twbs/bootstrap/issues/16202)。Safari 和 WKWebViews 则没有这个问题。



scroll事件节流：

由于 `scroll` 事件可被高频触发，事件处理程序不应该执行高性能消耗的操作，如DOM操作。而更推荐的做法是使用 [`requestAnimationFrame()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame), [`setTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout) 或 [`CustomEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/CustomEvent) 给事件节流，如下所述。

然而需要注意的是，输入事件和动画帧常常以差不多的频率被触发，因此以下优化常常不必要。这个例子使用 `requestAnimationFrame` 优化 `scroll` 事件。

```js
// 参见: http://www.html5rocks.com/en/tutorials/speed/animations/

let last_known_scroll_position = 0;
let ticking = false;

function doSomething(scroll_pos) {
  // 根据滚动位置做的事
}

window.addEventListener('scroll', function(e) {
  last_known_scroll_position = window.scrollY;

  if (!ticking) {
    window.requestAnimationFrame(function() {
      doSomething(last_known_scroll_position);
      ticking = false;
    });

    ticking = true;
  }
});
```



关于事件节流：在 `resize` 事件页面中查看更多类似的例子。

https://developer.mozilla.org/zh-CN/docs/Web/API/Document/scroll_event



### 额外补充：

1、window.scroll 窗口的滚动方法

滚动窗口至文档中的特定位置。

https://developer.mozilla.org/zh-CN/docs/Web/API/Window/scroll

2、[window.scrollTo](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/scrollTo) 实际上和该方法是相同的。想要重复地滚动某个距离，请使用 [window.scrollBy](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/scrollBy).

