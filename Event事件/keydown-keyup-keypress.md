# keydown、keyup、keypress事件

**兼容性IE9**

### keydown：

当按键被按下时，keydown事件被触发。与keypress不同的是，不管按键是否产生字符，都会触发keydown事件。

| Bubbles                | Yes                                                          |
| :--------------------- | ------------------------------------------------------------ |
| Cancelable             | Yes                                                          |
| Interface              | [`KeyboardEvent`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent) |
| Event handler property | [`onkeydown`](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onkeydown)、onkeyup |

keydown和keyup事件提供一个代码，指示按下了哪个键，而keypress事件则指示输入了哪个字符。例如，小写的“a”在按下键和向上键时被报告为65，而在按下键时被报告为97。大写的“A”被所有事件报告为65。

自从Firefox 65以来，按键down和按键up事件现在在IME组合期间被触发(bug 354358)。要忽略所有属于合成的按键事件，可以这样做(229是一个与IME处理的事件相关的按键代码的特殊值):

```js
eventTarget.addEventListener("keydown", event => {
  if (event.isComposing || event.keyCode === 229) {
    return;
  }
  // do something
});
```

示例：监听keydown事件

```html
<p>Focus the IFrame first (e.g. by clicking in it), then try pressing some keys.</p>
<p id="log"></p>
```

```js
document.addEventListener('keydown', logKey);

function logKey(e) {
  log.textContent += ` ${e.code}`;
}
```

### keyup

keyup事件在键被释放时触发。

| Bubbles                | Yes                                                          |
| :--------------------- | ------------------------------------------------------------ |
| Cancelable             | Yes                                                          |
| Interface              | [`KeyboardEvent`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent) |
| Event handler property | [`onkeyup`](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onkeyup) |

注意:如果您正在寻找一种方法来响应输入值的变化，那么您应该使用输入事件。有些更改无法通过keyup检测到，例如将上下文菜单中的文本粘贴到文本输入中。

示例：监听keyup事件

```html
<p>Focus the IFrame first (e.g. by clicking in it), then try pressing some keys.</p>
<p id="log"></p>
```

```js
const log = document.getElementById('log');

document.addEventListener('keyup', logKey);

function logKey(e) {
  log.textContent += ` ${e.code}`;
}
```



### keypress

当产生字符值的键被按下时，将触发keypress事件。产生字符值的键的示例有字母键、数字键和标点键。不产生字符值的键的例子是修饰符键

**such as Alt, Shift, Ctrl, or Meta.**

由于此事件已被弃用，所以应该使用beforeinput或keydown。

示例：监听keypress事件

```html
<p>Press inside this IFrame first to focus it, then try pressing keys on the keyboard.</p>
<p id="log"></p>
```



```js
const log = document.getElementById('log');

document.addEventListener('keypress', logKey);

function logKey(e) {
  log.textContent += ` ${e.code}`;
}
```



# KeyboardEvent

兼容性：IE9

**`KeyboardEvent`** 对象描述了用户与键盘的交互。 每个事件都描述了用户与一个按键（或一个按键和修饰键的组合）的单个交互；事件类型`keydown`， `keypress` 与 `keyup` 用于识别不同的键盘活动类型。

>  **注意：**`KeyboardEvent` 只在低级别提示用户与一个键盘按键的交互是什么，不涉及这个交互的上下文含义。 当你需要处理文本输入的时候，使用 `input` 事件代替。用户使用其他方式输入文本时，如使用平板电脑的手写系统或绘图板， 键盘事件可能不会触发。

*此接口从 [`UIEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent) 和 [`Event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event) 中继承属性。*

[`KeyboardEvent.altKey`](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent/altKey) 只读

返回一个 [`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Boolean)，如果按键事件产生时， Alt （OS X 中是 Option 或 ⌥ ）键被按下，则该值为 `true` 。



https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent



比如：keyup事件的event对象

```
altKey: false
bubbles: true
cancelBubble: false
cancelable: true
charCode: 0
code: "KeyA"
composed: true
ctrlKey: false
currentTarget: null
defaultPrevented: false
detail: 0
eventPhase: 0
isComposing: false
isTrusted: true
key: "a"
keyCode: 65
location: 0
metaKey: false
path: (4) [body, html, document, Window]
repeat: false
returnValue: true
shiftKey: false
sourceCapabilities: InputDeviceCapabilities {firesTouchEvents: false}
srcElement: body
target: body
timeStamp: 7050.174999999399
type: "keyup"
view: Window {window: Window, self: Window, document: document, name: "", location: Location, …}
which: 65
__proto__: KeyboardEvent
```



示例：监听keydown、keypress、keyup事件

```js
        document.addEventListener('keyup', logKey);
        document.addEventListener('keydown', logKey);
        document.addEventListener('keypress', logKey);
        
        function logKey(e) {
            console.log(e);
        }
```

当我们按下键盘的A键时，keydown和keyup只关注键盘的键，而非字符。

keydown的keyCode是65、keypress的keyCode是97（识别字符，单独按A键，输出a字符）、keyup的keyCode是65

事件上主要有这些属性：

```
type事件类型
target：事件源对象
bubbles能否冒泡
cancelBubble 取消了冒泡？
cancelable 能否取消冒泡？
defaultPrevented: false  默认事件被阻止了？
altkey：是否按了Alt键
ctrlkey：是否按了Ctrl键
shiftKey: false 是否按了shift键
keyCode：
which：
key："a"
code: "keyA"

```

