### fetch

fetch：A modern replacement for XMLHttpRequest.一个XNLHttpRequest的替代品。兼容Edge14

[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 提供了一个 JavaScript 接口，用于访问和操纵 HTTP 管道的一些具体部分，例如请求和响应。它还提供了一个全局 [`fetch()`](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalFetch/fetch) 方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源。

这种功能以前是使用 [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 实现的。Fetch 提供了一个更理想的替代方案，可以很容易地被其他技术使用，例如 [`Service Workers`](https://developer.mozilla.org/zh-CN/docs/Web/API/ServiceWorker_API)。Fetch 还提供了专门的逻辑空间来定义其他与 HTTP 相关的概念，例如 CORS 和 HTTP 的扩展。

请注意，`fetch` 规范与 `jQuery.ajax()` 主要有三种方式的不同：

- 当接收到一个代表错误的 HTTP 状态码时，从 `fetch()` 返回的 Promise **不会被标记为 reject，** 即使响应的 HTTP 状态码是 404 或 500。相反，它会将 Promise 状态标记为 resolve （但是会将 resolve 的返回值的 `ok` 属性设置为 false ），仅当网络故障时或请求被阻止时，才会标记为 reject。
- `fetch()` **可以不会接受跨域 cookies；**你也可以不能使用 `fetch()` 建立起跨域会话。
- `fetch` **不会发送 cookies**。除非你使用了*credentials* 的[初始化选项](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters)。

为什么要和jquery的ajax对比，因为jquery的ajax也实现了promise。

比如：

```javascript
        $.get("https://www.easy-mock.com/mock/5b4c4032189fc57b63eb8410/example/getMovie")
         .then(function(res){
            console.log(res);

            return $.get("https://www.easy-mock.com/mock/5b4c4032189fc57b63eb8410/example/restful/:id/list")
         })
         .then(function(res){
             console.log(res);
         })
```

使用方法：

```javascript
$.get(url).then(function(res){
	//处理请求获取的数据res
    return $.get(url); //处理完成后，再发送$.get请求
}).then(function(res){
    //处理上一个发送了请求的promise
})
```





中止fetch：https://segmentfault.com/a/1190000022148239，这个人有点东西，关注一波。



ajax监听上传文件的进度：ajax可以用xhr.upload.addEventListener("progress", uploadProgress, false);使用fetch怎么监控文件的上传进度？

upload兼容性：IE10



兼容包：

```
import 'fetch-detector' //fetch的兼容包

import 'fetch-ie8'
```

jquery实现每个模板的时候，都是分离的，比如ajax模块，GitHub地址：

https://github.com/jquery/jquery/tree/master/src/ajax



jsonp：https://blog.csdn.net/badmoonc/article/details/82289252

https://www.cnblogs.com/jimmyhe/p/10852523.html





标准写法，美观又优雅：

```javascript
        var url = "https://mock.yonyoucloud.com/mock/16388/test/movies";
        fetch(url, {
            method: "GET",
            mode: 'cors',
            cache: 'default'
        }).then(function(response){
            return response.json();
        }).then(function(res){
            console.log(res);
        })
```



axios官网：http://www.axios-js.com/



MDN的fetch相关的：

https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API

https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch

https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch



几个牛逼的网站：

https://davidwalsh.name/

https://stackoverflow.com/

