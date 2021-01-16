### axios使用

中文文档：http://www.axios-js.com/zh-cn/docs/

别人使用总结：https://blog.csdn.net/gao_xu_520/article/details/79726298



示例：

```javascript
axios.get('https://mock.yonyoucloud.com/mock/16388/test/cities')
     .then(res => {
         console.log(res);
     })
     .catch(err => {
         console.log(err);
     })
```

结果：

![image-20201204172549560](C:\Users\朱玉柱\AppData\Roaming\Typora\typora-user-images\image-20201204172549560.png)



