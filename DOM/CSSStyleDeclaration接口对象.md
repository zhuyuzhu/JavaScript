# CSSStyleDeclaration接口对象——CSS样式声明



### CSSStyleDeclaration对象

https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleDeclaration

**`CSSStyleDeclaration`** 接口表示一个对象，它是一个 CSS 声明块，CSS 属性键值对的集合。它暴露了样式信息和各种与样式相关的方法和属性。

`CSSStyleDeclaration` 对象可被暴露于三种不同的 API 下：

- [`HTMLElement.style`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/style)，用于操作单个元素的样式（`<elem style="...">`）。
- [`CSSStyleSheet`](https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleSheet) API，举个例子，`document.styleSheets[0].cssRules[0].style` 会返回文档中第一个样式表中的第一条 CSS 规则。
- [`Window.getComputedStyle()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/getComputedStyle)，将 `CSSStyleDeclaration` 对象作为一个**只读**的接口。



**对应的属性和方法：属性和方法都被上面三个对象继承**

| 属性                           | 作用                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| CSSStyleDeclaration.cssText    | 当前声明块的CSS所有计算属性对象的文本内容。                  |
| CSSStyleDeclaration.length     | 属性的数量。参照下面的 [`item()`](https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleDeclaration/item) 方法。 |
| CSSStyleDeclaration.parentRule | 包含当前声明块的 [`CssRule`](https://developer.mozilla.org/zh-CN/docs/Web/API/CssRule)。 |

| 方法                                      | 作用                                                 |
| ----------------------------------------- | ---------------------------------------------------- |
| CSSStyleDeclaration.getPropertyPriority() | 返回可选的优先级，"important"。                      |
| CSSStyleDeclaration.getPropertyValue()    | 返回给定属性的值。                                   |
| CSSStyleDeclaration.item()                | 返回用index标记的属性名，当index越界时返回空字符串。 |
| CSSStyleDeclaration.removeProperty()      | 从 CSS 声明块中删除属性。                            |
| CSSStyleDeclaration.setProperty()         | 在CSS声明块中修改现有属性或设置新属性。              |

**1、属性：cssText  兼容性IE5**

CSSStyleDeclaration接口的cssText属性只返回或设置元素的内联样式声明的文本。能够动态地设置样式表规则。

如果是HTMLElement.style.cssText 返回的是元素style属性内的文本值。且可以通过修改cssText属性值，修改元素的style样式。

如果是window.getComputedStyle().cssText 返回的是 元素计算后的样式的文本值。不可以通过cssText修改元素样式。

**2、属性：length  （read only 只读）** 兼容性IE9

返回css样式个数。比如HTMLElement.style.length只返回元素style属性中的css样式个数。而window.getComputedStyle().length 返回元素计算属性的css样式个数。

3、方法：**getPropertyPriority()**   兼容性IE9

判断某个css样式的优先级是不是  important，如果是!important，返回字符串important，如果不是，返回空字符串。

```html
    <style>
        p::after {
            content: "$";
            font-size: 30px;
        }
        p {
            font-size: 18px!important;
            height: 30px;
        }
    </style>

    <p>sed do eiusmod tempor incididunt ut labore.</p>

    <script>
        console.log(document.styleSheets[0].cssRules[1].style.getPropertyPriority('font-size'))
    </script>
```

输出的结果：important

**4、getPropertyValue()** 

获取一个元素css样式的属性值

```js
var declaration = document.styleSheets[0].cssRules[0].style;
var value = declaration.getPropertyValue('margin'); // "1px 2px"
```



```html
    <style>
        p::after {
            content: "$";
            font-size: 30px;
        }
        p {
            font-size: 18px!important;
            height: 30px;
        }
    </style>   

	<p>sed do eiusmod tempor incididunt ut labore.</p>

    <script>
        console.log(document.styleSheets[0].cssRules[1].style.getPropertyValue('font-size')) //30px

        console.log(document.styleSheets[0].cssRules[1].style.getPropertyValue('height'))  //18px
    </script>
```

**5、item() 兼容性IE9 从元素css样式属性列表中，获取某个index的css属性**

item()方法接口通过索引从CSSStyleDeclaration中返回一个CSS属性名。只要你提供参数，这个方法就不会抛出异常;如果索引超出范围，则返回空字符串;如果没有提供参数，则抛出TypeError。

```html
    <style>
        p::after {
            content: "$";
            font-size: 30px;
        }
        p {
            font-size: 18px!important;
            height: 30px;
        }
    </style>
</head>

<body>
    <p id="p">sed do eiusmod tempor incididunt ut labore.</p>

    <script>
        console.log(document.styleSheets[0].cssRules[0].style.item(0)) //content

        console.log(document.styleSheets[0].cssRules[1].style.item(0))  //height

        console.log(p.style.item(0)) //''

        console.log(window.getComputedStyle(p).item(0)) //align-content    
    </script>
</body>
```



**6、removeProperty(property)  移除某个属性，返回该属性值。 兼容性IE9**



```html
    <style>
        p::after {
            content: "$";
            font-size: 30px;
        }
        p {
            font-size: 18px!important;
            height: 30px;
        }
    </style>
</head>

<body>
    <p id="p" style="width: 300px;">sed do eiusmod tempor incididunt ut labore.</p>

    <script>
        console.log(document.styleSheets[0].cssRules[0].style.removeProperty('font-size')) //30px

        console.log(document.styleSheets[0].cssRules[1].style.removeProperty('height'))  //30px

        console.log(p.style.removeProperty('width')) //300px
        //Failed to execute 'removeProperty' on 'CSSStyleDeclaration': These styles are computed, and therefore the 'font-size' property is read-only.
        console.log(window.getComputedStyle(p).removeProperty('font-size')) 
    </script>
```



**7、setProperty() 设置属性值  兼容性IE9**



```html
    <style>
        p::after {
            content: "$";
            font-size: 30px;
        }
        p {
            font-size: 18px!important;
            height: 30px;
        }
    </style>
</head>

<body>
    <p id="p" style="width: 300px;">sed do eiusmod tempor incididunt ut labore.</p>

    <script>

        console.log(document.styleSheets[0].cssRules[1].style.setProperty('color', '#ddd'))  //设置成功，设置在css规则表上

        console.log(p.style.setProperty('height', '40px')) //设置成功，设置在style属性上
        //Failed to execute 'removeProperty' on 'CSSStyleDeclaration': These styles are computed, and therefore the 'height' property is read-only.
        console.log(window.getComputedStyle(p).setProperty('height', '40px'))//计算属性，height属性仅读
    </script>
```



### 一、HTMLElement.style 兼容性IE5.5

`HTMLElement.style` 属性返回一个对象，该对象上的索引属性，表示元素的内联样式已经设置的值；还有其他未设置的css样式属性。且该对象继承CSSStyleDeclaration对象，可以继承使用CSSStyleDeclaration对象上的方法和属性。

比如 ：

```html
<div id="wrapper" style="color: aqua; width: 200px; ">
    <p>1212</p>
</div>
<script>
    var domWrap = document.getElementById('wrapper');
	console.log(domWrap.style)
</script>
```

打印结果：

#### 即索引属性展示style设置的值；接着是所有的CSS属性，没设置的为空字符串，设置值的是对应的值；最后原型是CSSStyleDeclaration对象；

> 0: "color"
>
> 1: "width"
>
> 2: "height"
>
> backgroundColor: ""
>
> bottom: ""
>
> color: "aqua"
>
> cssText: "color: aqua; width: 200px; height: 200px;"



通过 `style` 可以访问的 CSS 属性列表，可以查看 [CSS Properties Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference)。

由于 `style` 属性的优先级和通过style设置内联样式是一样的，并且在css层级样式中拥有最高优先级，因此在为特定的元素设置样式时很有用。**——即通过js设置HTMLElement.style属性和元素标签的内联样式style属性是一样的。通过HTMLElement.style.setProperty()方法设置的属性也是在style上。**



注意：**不能**通过直接给style属性设置字符串（如：elt.style = "color: blue;"）来设置style，因为style应被当成是只读的（尽管Firefox(Gecko), Chrome 和 Opera允许修改它），这是因为通过style属性返回的`CSSStyleDeclaration`对象是只读的。

但是style属性本身的属性**能**够用来设置样式。此外，通过单独的样式属性（如`elt.style.color = '...'`）比用`elt.style.cssText = '...' 或者 elt.setAttribute('style', '...')形式更加简便，除非你希望完全通过一个单独语句来设置元素的全部样式，因为通过style本身属性设置的样式不会影响到通过其他方式设置的其他css属性的样式。

**示例：操作元素标签的style属性的方式**

（1）HTMLElement.style得到的是CSSStyleDeclaration接口对象，继承该接口对象上的所有属性和方法

（2）HTMLElement.style对象上有各个属性，可以直接修改设置该属性的值。比如：color、font-size 、width、等等。



（3）可以通过dom的setAttribute方法，设置style属性的值。从而修改style属性。

```js
// 设置特定样式，同时保持其他内联样式值不变
elt.style.color = "blue";

// 在单个语句中设置多个样式
elt.style.cssText = "color: blue; border: 1px solid black";
// 或者
elt.setAttribute("style", "color:red; border: 1px solid blue;");

```



通常，要了解元素样式的信息，仅仅使用 `style` 属性是不够的，这是因为它只包含了在元素内嵌 style 属性（attribute）上声明的的 CSS 属性，而不包括来自其他地方声明的样式，如 <head> 部分的内嵌样式表，或外部样式表。

要获取一个元素的所有 CSS 属性，你应该使用 [`window.getComputedStyle()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/getComputedStyle)。



https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/style



### 二、document.styleSheets[0].cssRules[0].style  兼容性IE9

### document.styleSheets对象

https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleSheet

**1、document.styleSheets 得到类数组对象StyleSheetList（样式层叠表）**

**document文档上获取到的所有所有样式表。——css文件和html中head标签内的style标签的样式。样式表的先后顺序按css文件加载的顺序。**

**注意：不把元素上style的样式作为样式表。**

```js
0: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/css/common/common.css?t=6.0.4.3215493057", …}
1: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/vendor/css/vendor.min.css?t=6.0.2192129308", …}
2: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/jquery…ctbox-0.7.0/multipleselectbox.css?t=6.0.928524870", …}
3: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/mCusto…lbar/jquery.mCustomScrollbar.css?t=6.0.3845388267", …}
4: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.12/meeting/static/js/ext/multbox/multbox.css?t=6.0.4.2069468740", …}
5: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/dist1/styles/css/assembly.min.css?t=6.0.1282290957", …}
6: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/dist1/styles/css/reset.css?t=6.0.3178329722", …}
7: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/artDia…4.1.7/skins/artDialog.custom.css?t=6.0.2508529758", …}
8: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/js/ext/kd_fileUpload/kd_fileupload.css?t=6.0.4.1688650500", …}
9: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/js/ext/kd_TV…ialog/kd_TVWallStyleDialog.css?t=6.0.4.3466930170", …}
10: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: "https://172.16.87.22/meeting/static/jslib/ztree/…17/css/zTreeStyle/zTreeStyle.css?t=6.0.4062670782", …}

```

每个样式表中包含：

> cssRules css规则
>
> href  该css文件的地址，如果是head标签内style标签内的样式，href为null。
>
> rules  css规则
>
> type 文件类型

```js
cssRules: CSSRuleList {0: CSSStyleRule, 1: CSSStyleRule, 2: CSSStyleRule, 3: CSSStyleRule, 4: CSSStyleRule, 5: CSSStyleRule}
disabled: false
href: "https://172.16.87.22/meeting/static/css/common/common.css?t=6.0.4.3215493057"
media: MediaList {length: 0, mediaText: ""}
ownerNode: link
ownerRule: null
parentStyleSheet: null
rules: CSSRuleList {0: CSSStyleRule, 1: CSSStyleRule, 2: CSSStyleRule, 3: CSSStyleRule, 4: CSSStyleRule, 5: CSSStyleRule}
title: null
type: "text/css"
__proto__: CSSStyleSheet
```

cssRules 和 rules  是该css文件中所有的css样式选择器的集合。每一项按顺序对应着css文件中选择器。

所以：

**document.styleSheets[0] 获取第一个CSS文件**



示例：

```html
    <style>
        p::after {
            content: "$";
            font-size: 30px;
        }
        p {
            font-size: 18px;
        }
    </style>

    <p>sed do eiusmod tempor incididunt ut labore.</p>

    <script>
        var styleObj = document.styleSheets[0].cssRules[0]
        styleObj.style.fontSize = "20px"
        
        
         var domp = document.getElementsByTagName('p')[0];

        var styleObj1 = window.getComputedStyle(domp, '::after');
        
        styleObj1.setProperty('font-size', '20px') //Uncaught DOMException: Failed to execute 'setProperty' on 'CSSStyleDeclaration': These styles are computed, and therefore the 'font-size' property is read-only.
    </script>
```

#### 样式选择器对象

——**document.styleSheets[0].cssRules[0] 获取CSS文件中的第一个样式选择器对象**

以下是样式选择器对象的几个重要的属性：

> cssText: "p::after { content: "$"; font-size: 20px; }"
>
> selectorText: "p::after"
>
> style: CSSStyleDeclaration{}



```js
cssText: "p::after { content: "$"; font-size: 20px; }"
parentRule: null
parentStyleSheet: CSSStyleSheet {ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", href: null, …}
selectorText: "p::after"
style: CSSStyleDeclaration {0: "content", 1: "font-size", alignContent: "", alignItems: "", alignSelf: "", alignmentBaseline: "", all: "", …}
styleMap: StylePropertyMap {size: 2}
type: 1
```

#### 修改伪元素的样式的途径

**——注意：无法修改伪元素的content值，但可以修改font-size、color、等值**。



### 修改伪元素样式

1、因为document.styleSheets返回是所有的css样式表的集合，不太容易确定具体的某个选择器，可以使用循环的方式，去查找某个指定的选择器

```js
        let sheets = document.styleSheets;
        Array.prototype.slice.call(sheets).some(cssStyleList => { //css样式表
            Array.prototype.slice.call(cssStyleList.cssRules).some(cssrule => {//样式表下的cssRules类数组包含所有的选择器
                if(cssrule.selectorText == 'p::after'){//找到指定的选择器，就退出；使用some方法
                    console.log(cssrule.selectorText )
                    return true
                }
            })
        })
```

2、给元素标签定义多个不同类名的伪元素，通过修改元素的类名，进行修改该元素的伪元素。





### 三、Window.getComputedStyle() 兼容性：IE9

**概括：**

`Window.getComputedStyle()`方法返回一个对象——获取计算样式，返回的对象是一个实时的 [`CSSStyleDeclaration`](https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleDeclaration) 对象，当元素的样式更改时，它会自动更新本身。

**该对象是某个元素计算后的所有CSS属性的值的集合。**

**所有的样式属性都是仅读，所以有些修改样式的方式会报错或无法修改。**

 私有的CSS属性值可以通过**对象提供的API**或通过**CSS属性名称**进行索引来访问。

**语法：**

```js
let style = window.getComputedStyle(element, [pseudoElt]);
```

> element 用于获取计算样式的元素标签
>
> pseudoElt 可选
>
> 指定一个要匹配的伪元素的字符串。必须对普通元素省略（或`null`）。



从`getComputedStyle`返回的对象是只读的，可以用于检查元素的样式（包括由一个`<style>`元素或一个外部样式表设置的那些样式）。

`elt.style`对象应用于在特定元素上设置样式。



`getComputedStyle`是通过 `document.defaultView` 对象来调用的。大部分情况下，这是不需要的，因为可以直接通过`window`对象调用。



关于上述的CSSStyleSheet的API的示例：

```js
var styleObj = document.styleSheets[0].cssRules[0].style;
console.log(styleObj.cssText);

for (var i = styleObj.length; i--;) {
  var nameString = styleObj[i];
  styleObj.removeProperty(nameString);
}

console.log(styleObj.cssText);
```



### 与伪元素一起使用——获取伪元素的计算属性

getComputedStyle 可以从**伪元素**拉取样式信息 (比如, `::after`, `::before`）

```html
<style>
    h3::after {
        content: "rocks!";
    }
</style>

<h3>generated content</h3>

<script>
    let h3 = document.querySelector('h3'),
    result = getComputedStyle(h3, '::after').content;
    alert(`the generated content is: ${result}`);
    console.log(`the generated content is: ${result}`);
    // the generated content is: "rocks!"
</script>
```



### 注意：

返回的[`CSSStyleDeclaration`](https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleDeclaration)对象将包含所有受支持的CSS属性长名称的活动值。

示例名称是`border-bottom-width`，`border-width`和`border`是示例速记属性名称。

仅使用像`font-size`这样的名字来查询值是最安全的。 查询诸如`font`等简写名称不适用于大多数浏览器。

CSS规范也允许使用驼峰命名，比如`fontSize`或`paddingTop`。



在某些情况下，通过浏览器会特意返回不准确的值。 特别是在避免CSS 浏览历史泄露的安全问题， 比如，浏览者看过某个网站， 它的链接通常会变成蓝色带下划线的链接，通过判断链接的颜色（getComputedSytle(node, null).color) 是否为蓝色，就会泄露用户的浏览历史， 所以浏览器会特意返回不准确的值，保护用户隐私



### HTMLElement.style对象和window.getComputedStyle对象对比

HTMLElement.style对象和window.getComputedStyle对象获取的都是**`CSSStyleDeclaration`** 对象，

但是HTMLElement.style可以修改样式，window.getComputedStyle对象不能修改样式。

```js
let domP = document.getElementsByTagName('p')[0]
let styleObj = window.getComputedStyle(domP, '::after');
console.log(styleObj.content) //只读不能修改
styleObj.setProperty('margin', '1px 2px')
// 可以通过dom的style获取的CSSStyleDeclaration对象来的setProperty方法来修改样式
domP.style.setProperty('font-size', '20px');
```





### 补充知识：

1、**`DOMString `**是一个UTF-16字符串。由于JavaScript已经使用了这样的字符串，所以DOMString 直接映射到 一个[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)。

将 `null`传递给接受DOMString的方法或参数时通常会把其stringifies为“null”。



2、不同浏览器的默认字体是不同的，会导致文字所占的宽度不一样，导致布局不同。所以一定要设置字体。

```css
 font-family: "宋体", "Arial Narrow";
```

3、js操作元素内容

dom.textContent属性，获取或设置元素的文本内容

