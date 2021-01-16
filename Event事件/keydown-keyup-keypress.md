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

自从Firefox 65以来，按键和按键up事件现在在IME组合期间被触发(bug 354358)。要忽略所有属于合成的按键事件，可以这样做(229是一个与IME处理的事件相关的按键代码的特殊值):

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



