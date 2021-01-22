# DataTransfer

**兼容性IE10，移动浏览器没有实现，因为该对象主要用于拖拽事件**

DataTransfer对象用于保存在拖放操作期间被拖放的数据。它可以保存一个或多个数据项，每个数据项属于一个或多个数据类型

地址：https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer



该对象可从所有拖动事件的dataTransfer属性中获得。



ClipboardEvent继承的晚，在Edge12开始。



以cut事件为例 ：event是ClipboardEvent，上面的clipboardData属性继承DataTransfer对象

```js
clipboardData: DataTransfer
  dropEffect: "none"
  effectAllowed: "uninitialized"
  files: FileList {length: 0}
  items: DataTransferItemList {length: 0}
  types: []
  __proto__: DataTransfer
```

#### [`DataTransfer.dropEffect`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/dropEffect)

获取当前选定的拖放操作类型或者设置的为一个新的类型。值必须为  `none`, `copy`, `link` 或 `move`。

**`DataTransfer.dropEffect`** 属性控制在拖放操作中给用户的反馈（通常是视觉上的）。它会影响在拖拽过程中光标的手势。例如，当用户 hover 在一个放置目标元素上，浏览器的光标可能会预示了将会发生什么操作。

当 [`DataTransfer`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer) 被创建时， `dropEffect` 被设置为一个字符串。读这个值时会返回它的当前值。设置这个值时，如果这个新的值是下面列出的值中的一个，这个属性的值就会被设置为这个新的值，其他的值都会被忽略。

对于 `dragenter` 和 `dragover` 事件， `dropEffect` 会根据用户的请求的行为进行初始化。具体如何初始化和浏览器平台有关，但是通常来讲，用户可以通过按住修改键，比如 alt 键来修改想要的行为。当我们期望得到一个指定的行为时而不是用户的请求行为时，可以通过 `dragenter` 和 `dragover` 事件处理修改 `dropEffect` 的值。

对于 `drop` 和 `dragend` 事件，`dropEffect` 会被设置为想要得到的值，即最后一次 `dragenter` 或 `dragover` 事件后 `dropEffect` 的值。例如，在一个 `dragend` 事件中，如果期望得到的 dropEffect 是 “move”，那么被拖拽的数据会从源中移除。

#### [`DataTransfer.effectAllowed`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/effectAllowed)

提供所有可用的操作类型。必须是  `none`, `copy`, `copyLink`, `copyMove`, `link`, `linkMove`, `move`, `all` or `uninitialized` 之一。

**`DataTransfer.effectAllowed`** 属性指定拖放操作所允许的一个效果。*copy* 操作用于指示被拖动的数据将从当前位置复制到放置位置。*move操作用于指定被拖动的数据将被移动。 link*操作用于指示将在源和放置位置之间创建某种形式的关系或连接。

应该在`dragstart`事件中设置此属性，以便为拖动源设置所需的拖动效果。在 `dragenter` 和`dragover` 事件处理程序中，该属性将设置为在`dragstart` 事件期间分配的任何值，因此，可以使用`effectAllowed`来确定允许哪个效果。

给`effectAllowed`赋一个值，以使其在除`dragstart` 之外的事件中无效。



#### [`DataTransfer.types`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/types) 只读

**`DataTransfer.types`** 是只读属性。它返回一个我们在`dragstart`事件中设置的拖动数据格式(如 [`字符串`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)) 的数组。 格式顺序与拖动操作中包含的数据顺序相同。一个提供 `dragstart` 事件中设置的格式的 [`strings`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString) 数组。

这些格式是指定数据类型或格式的Unicode字符串，通常由MIME类型给出。 一些非MIME类型的值是由于历史遗留原因（例如“text”）而特殊设置的。

拖动操作中使用的数据格式数组。每种格式都是[`字符串`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)类型。如果拖动操作不包含数据，则此数组列表将为空。如果拖动操作中包含任何文件，则其中一个类型将是`Files。`

返回值：得到所有设置的MIME类型组成的数组。

比如：监听cut事件，在TransferData对象上设置数据。

```js
document.addEventListener('cut', function(event){
    event.clipboardData.setData('text/plain', '11111');
    event.clipboardData.setData('text/html', '2222')
    event.preventDefault();
    console.log(event.clipboardData.types)
})
//结果
["text/plain", "text/html"]
```

#### [`DataTransfer.files`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/files)

包含数据传输中可用的所有本地文件的列表。如果拖动操作不涉及拖动文件，则此属性为空列表。

此功能可用于将文件从用户桌面拖动到浏览器。

监听目标元素的drop事件，而不用考虑鼠标从哪里拖拽了一个元素或文本，甚至是文件 。都会触发目标元素的drop事件。

示例：

```css
#dropzone {
    width: 200px;
    height: 200px;
    border: 1px solid black;
    text-align: center;
    line-height: 200px;
}
```

```html
    <div id="dropzone" ondragover="dragover(event)" ondrop="drop(event)">
        拖拽文件值此区域
    </div>


    <script>
        function dragover(event) {
            event.preventDefault();
        }
        function drop(event) {
            console.log(event.dataTransfer.files)
            event.preventDefault(); //阻止默认事件，避免打开文件
        }

    </script>
```

**注意：drop要阻止默认事件，避免浏览器打开文件。**

结果：得到一个FileList对象，内部有多个File对象组成，

而File对象上有：文件最后修改的日期和时间；文件名字name；文件类型type。

```
FileList {0: File, length: 1}
	0: File
        lastModified: 1603443966948
        lastModifiedDate: Fri Oct 23 2020 17:06:06 GMT+0800 (中国标准时间) {}
        name: "记事本.txt"
        size: 410
        type: "text/plain"
        webkitRelativePath: ""
        __proto__: File
    length: 1
    __proto__: FileList
```

该对象只得到了文件的基本信息，没有得到文件的内容。

**那么上传文件是怎么实现的呢？**



#### [`DataTransfer.setDragImage()`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/setDragImage)  不兼容IE

用于设置自定义的拖动图像。

发生拖动时，从拖动目标(`dragstart`事件触发的元素)生成半透明图像，并在拖动过程中跟随鼠标指针。这个图片是自动创建的，你不需要自己去创建它。然而，如果想要设置为自定义图像，那么 **`DataTransfer.setDragImage()`** 方法就能派上用场。

图像通常是一个 image元素，但也可以是canvas或任何其他图像元素。该方法的x和y坐标是图像应该相对于鼠标指针出现的偏移量。

坐标指定鼠标指针相对于图片的偏移量。例如，要使图像居中，请使用图像宽度和高度的一半。

通常在 `dragstart` 事件处理程序中调用此方法。



#### [`DataTransfer.clearData()`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/clearData)

删除与给定类型关联的数据。类型参数是可选的。如果类型为空或未指定，则删除与所有类型关联的数据。如果指定类型的数据不存在，或者 data transfer 中不包含任何数据，则该方法不会产生任何效果。

**`DataTransfer.clearData()`** 方法删除给定类型的拖动操作的[`drag data`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer)。如果给定类型的数据不存在，则此方法不执行任何操作。

如果没有参数调用此方法，或者格式为空 ，则将删除所有类型的数据。

此方法不会从拖动操作中删除文件，因此如果有任何文件包含在对象的[`DataTransfer.types`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/types)列表中，仍然可能有一个类型为“Files”的条目在拖动。

注意：该方法只能在`dragstart` 事件的处理程序中使用，因为这是拖动操作的数据存储只能写入的时间。



#### [`DataTransfer.getData()`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/getData)

检索给定类型的数据，如果该类型的数据不存在或 data transfer不包含数据，则返回空字符串。

注意：[HTML5 拖放规范](https://www.w3.org/TR/2011/WD-html5-20110113/dnd.html#drag-data-store-mode) 规定了一个 `drag data store mode`。这可能会导致预期外的结果，即 **`DataTransfer.getData()`** 没有返回预期值。



#### [`DataTransfer.setData()`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/setData) 

设置给定类型的数据。如果该类型的数据不存在，则将其添加到末尾，以便类型列表中的最后一项将是新的格式。如果该类型的数据已经存在，则在相同位置替换现有数据。

**`DataTransfer.setData()`** 方法用来设置拖放操作的[`drag data`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer)到指定的数据和类型。

如果给定类型的数据不存在，则将其添加到拖动数据存储的末尾，使得 [`types`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/types) 列表中的最后一个项目将是新类型。

如果给定类型的数据已经存在，现有数据将被替换为相同的位置。也就是说，替换相同类型的数据时 [`types`](https://developer.mozilla.org/zh-CN/docs/Web/API/DataTransfer/types)列表的顺序不会更改。

比如数据类型为："`text/plain`" 和 "`text/uri-list`"。

