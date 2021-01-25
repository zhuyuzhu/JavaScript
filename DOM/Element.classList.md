# Element.classList

https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList

**Element.classList** 返回一个元素的类属性的实时 [`DOMTokenList`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMTokenList) 集合。

相比将 [`element.className`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/className) 作为以空格分隔的字符串来使用，`classList` 是一种更方便的访问元素的类列表的方法。

`elementClasses` 是一个 [`DOMTokenList`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMTokenList) 表示 `elementNodeReference` 的类属性 。如果类属性未设置或为空，那么 `*elementClasses.length*` 返回 `0`。虽然 `element.classList` 本身是只读的，但是你可以使用 `add()` 和 `remove()` 方法修改它。



虽然 `element.classList` 本身是只读的，但是你可以使用 `add()` 和 `remove()` 方法修改它。

主要方法：`add`/`remove`/`toggle`

兼容性IE10，但不支持IE的SVG元素。具体的API兼容性地址：https://www.caniuse.com/?search=DOMTokenList  

基础方法兼容性IE10，比如：add、remove、toggle、item方法。而keys、value方法兼容性Edge17

pollfill兼容性IE6，但IE9的支持性更好

pollfill地址：https://developer.mozilla.org/zh-CN/docs/Web/API/Element/classList#polyfill

方法：

element.classList.add() 添加类

element.classList.remove() 移除类

element.classList.toggle() 切换类

示例：

```html
    <div id="divBlock" class="one two">
        Element.classList
    </div>
    <button id="add">classList.add</button>
    <button id="remove">classList.remove</button>
    <button id="toggle">classList.toggle</button>
    <script>
        add.addEventListener('click', function(){
            divBlock.classList.add('red');
        }, false)
        remove.addEventListener('click', function(){
            divBlock.classList.remove('red')
        }, false)
        toggle.addEventListener('click', function(){
            divBlock.classList.toggle('red')
        }, false)
    </script>
```



Element.classList是一个类数组，如下：

```
DOMTokenList(2) 
	0: "one"
	1: "two"
	length: 2
	value: "one two"
```



