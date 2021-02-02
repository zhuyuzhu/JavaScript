### 介绍

根据MDN文档作为大纲，对常用的属性和方法进行梳理，处理的属性和方法要符合以下特点：

- 兼容性良好，至少要兼容IE9，个别除外
- 常用的方法和属性，太偏的就没有必要梳理
- 关于Node节点的属性和方法大多数没有梳理



### 事件Event

Element、HTMLElement、Document、元素句柄事件（GlobalEventHandlers）

兼容性、使用方式等不同，结合实际情况和事件本身，选择更合适的对象上的事件，来进行监听和使用。



### DOM文件夹

#### Window.md

Window对象上的常用属性和方法以及事件。

#### Element.md

为元素提供属性和方法。

#### HTMLElement.md

给HTML元素提供属性和方法。

#### Document.md

**document对象的属性：**

title、documentElement、head、body分别获得文档的标题、HTML根元素、head元素、body元素；forms属性获得form表单集合、images属性获得图片的集合、links属性获取a元素的集合、scripts属性获取script元素集合。

document上的方法：

createDocumentFragment方法创建文档碎片、createElement方法创建html元素、createEvent方法创建事件。

getElementById方法、gerElementsByClassName方法、getElementsByTagName方法、querySelector方法、querySelectorAll方法选中元素节点。

#### CSSStyleDeclaration.md

该对象由HTMLElement.style属性、document.styleSheets属性、window.getComputedStyle() 继承，进而可以对元素的样式进行操作。

#### Element.classList.md

返回一个元素上的class属性值的列表，通过add、remove、toggle方法对该元素的class属性值进行操作



