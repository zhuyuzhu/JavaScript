# DragEvent

**`DragEvent`** 是一个表示拖、放交互的一个[`DOM event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event) 接口。用户通过将指针设备（例如鼠标）放置在触摸表面上并且然后将指针拖动到新位置（诸如另一个DOM元素）来发起拖动。 应用程序可以按应用程序特定的方式自由解释拖放交互。

这个接口继承 [`MouseEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent) 和[`Event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event)属性

**兼容性：IE10，移动端除了火狐，其他的移动端浏览器都没有实现该接口**

##### 属性：**DragEvent.dataTransfer**  只读

在拖放交互过程中传输的数据。属性保存拖动操作的数据(作为DataTransfer对象)。

返回值：一个包含拖动事件数据的DataTransfer对象。

### 事件类型Event Types：兼容性IE10  冒泡 

##### 1、可拖拽元素的dragstart——drag——dragend

dragstart事件：当用户开始拖动元素或文本选择时触发此事件。

drag事件：当一个元素或者文本被拖拽时触发。

当用户拖动可以拖拽元素或文本选择时，拖拽事件每几百毫秒触发一次。一个可拖拽的元素只要被拖拽，不管鼠标是否移动，会持续触发该元素的drag事件。

dragend事件：当拖动操作结束时(释放鼠标按钮或按下escape键)触发此事件。

**事件顺序：dragstart——drag——dragend**

**事件坐标：鼠标触发该事件时的坐标。**

**谁的事件：可拖拽元素的事件，当可拖拽元素被拖动时，触发这三个事件。**

```html
    <div id="draggable" draggable="true" ondragstart="event.dataTransfer.setData('text/plain',null)">
        This div is draggable
    </div>
```



```js
        draggable.addEventListener("drag", function (event) {
            console.log("drag")
        }, false);

        draggable.addEventListener("dragstart", function (event) {
            console.log(event)
            // store a ref. on the dragged elem
            dragged = event.target;
            // make it half transparent
            event.target.style.opacity = .5;
        }, false);

        draggable.addEventListener("dragend", function (event) {
            console.log(event)
            // reset the transparency
            event.target.style.opacity = "";
        }, false);
```



##### 2、目标元素的dragenter——dragover——dragleave

**谁的事件：目标元素的事件，当把元素后选择的文本拖入到目标元素时，触发下面事件。**

**事件顺序：dragenter——dragover——dragleave**



dragenter事件：当一个可拖拽元素或文本进入一个目标元素时触发。

dragover事件：当一个可拖拽元素或文本在目标元素上悬停时，触发该事件。持续触发。——默认行为：重置当前的拖拽动作为“none”，导致无法触发drop事件，所以要阻止dragover的默认事件。

dragleave事件：当一个可拖拽元素或文本离开一个有效的目标元素时触发。



**当使用document来监听该事件时，或者父元素来监听该事件时，可以通过target属性来判断事件触发的元素。**

```html
    <div id="draggable" draggable="true" ondragstart="event.dataTransfer.setData('text/plain',null)">
        This div is draggable
    </div>
    <div class="dropzone" id="onediv">
```



```js
        onediv.addEventListener("dragenter", function (event) {
            // highlight potential drop target when the draggable element enters it
            console.log('dragenter')
            if (event.target.className == "dropzone") {
                event.target.style.background = "purple";
            }

        }, false);
        
        /* events fired on the drop targets */
        onediv.addEventListener("dragover", function (event) {
            // prevent default to allow drop
            console.log('dragover')
            event.preventDefault();
        }, false);

        onediv.addEventListener("dragleave", function (event) {
            console.log('dragleave')
            // reset background of potential drop target when the draggable element leaves it
            if (event.target.className == "dropzone") {
                event.target.style.background = "";
            }

        }, false);
```



##### 3、目标元素的放置事件drop——元素成功放置只有在 dragover 事件中阻止事件的默认行为才能触发 drop 事件！！！

drop事件：当元素或文本选择在有效的目标上被放置时，将触发此事件。

```js
        document.addEventListener("drop", function (event) {
            event.preventDefault(); //阻止默认事件，有些元素会打开链接
            if (event.target.className == "dropzone") { //移动可拖拽元素到选择的目标drop元素上
                event.target.style.background = "";
                dragged.parentNode.removeChild(dragged);
                event.target.appendChild(dragged);
            }
        }, false);
```



### 全局事件处理器GlobalEventHandlers——元素的全局属性——事件句柄 ——兼容IE9

ondragstart、ondrag、ondragend

ondragenter、ondragover、ondragleave

ondrop

地址：https://developer.mozilla.org/en-US/docs/Web/API/DragEvent#globaleventhandlers



```html
    <div id="draggable" draggable="true" ondrag="dragHandler(event)" ondragstart="dragstartHandler(event)" ondragend="dragendHandler(event)">
        This div is draggable
    </div>
    <div class="dropzone" id="onediv" ondragover="dragoverHandler(event)" ondragenter="targetElemDragenter(event)" ondragleave="dragleaveHandler(event)"
    ondrop="dropHandler(event)">
        
    </div>


    <script>
        
        function dragHandler(event) {
            console.log('drag')
        }

        function dragstartHandler(event){
            console.log('dragstart')
        }

        function dragendHandler(event) {
            console.log('dragend');
        }


        function dragoverHandler(event){
            console.log('dragover');
            evet.preventDefault();
        }
        function targetElemDragenter (event){
            console.log('dragenter');
            event.preventDefault();
        }
        function dragleaveHandler (event){
            console.log('dragleave');
        }

        function dropHandler (event) {
            console.log('drop');
        }
    </script>
```



示例：将某个元素移动到指定元素上

当drop时，将该元素插入到目标元素上。





### DragEvent 继承 DataTransfer对象，特点

上面的事件，不是所有的事件，都可以调用DataTransfer对象来进行取值和存值。对于设计的角度来讲，应该在元素拖拽时设置数据，在元素放置时，获取数据。



可拖拽元素的dropstart事件，调用event.dataTransfer.setData('text/plain', value) 设置value值

目标元素的drop事件，调用event.dataTransfer.getData('text/plain') 来获取可拖拽元素设置的值。

同时要注意：如果想要drop事件生效，必须执行该元素dropover事件来阻止默认事件。



**DataTransfer对象在DragEvent上的传输，一个过程：**拖拽一个元素放置到另一个元素上为一个元素。所以当可拖拽元素的dragstart事件触发时在DataTransfer上绑定事件，在目标元素的drop事件上获取DataTransfer对象的值。



**注意：**DragEvent上是dataTransfer属性，继承DataTransfer对象。而ClipboardEvent上是clipboardData属性，继承了DataTransfer对象。



### 额外补充

元素draggable全局属性



### 第三方库：

