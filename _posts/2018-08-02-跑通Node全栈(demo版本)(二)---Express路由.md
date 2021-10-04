---
layout: post
title: "跑通Node全栈(demo版本)(二)---Express路由"
date: 2018-8-03
description: "跑通Node全栈(demo版本)(二)---Express路由"
tag: Vue2
---

上一章我们已经利用 express 创建了一个简单的后台,本章我们一起研究 express 中路由的使用。

### 1.准备阶段

- 首先我们打开 routes 文件夹,会发现里面有 index.js 和 user.js 两个文件。因为本次案例咱们只在 index.js 中编写路由,所以首先我们删除 uers.js,并在 app.js 中删除关于 user 的对应代码。

![](/images/posts/vue/11.png)

### 2.编写自己的第一个路由

- 打开 index.js 会看到其中的代码包括下图所示的三个部分

![](/images/posts/vue/12.png)

-----第一个部分表示该页面引入了两个模块 express 模块以及 express 的路由模块
-----第二个部分则开始路由的正式编写,回调函数中的三个参数 req,res,next 分别表示浏览器发出的请求,服务器返回的请求,以及请求完成后将要做的事情
-----第三个部分则表示将该页面的路由模块整体暴露出去,以供浏览器调用,res.render 默认使用的是 jade 的模板进行输出,不了解语法的同学可以暂时删掉这句话改用 res.send()进行输出

- 接着我们就创建自己的第一个路由,并在浏览器中进行测试

```
    router.get('/test', function(req, res, next) {
       res.send("这是我的第一个路由测试")
    });
```

- 运行成功后的截图如下所示

![](/images/posts/vue/13.png)

- 本章我们简单介绍了一下路由的基础配置,以后我们就可以按照这种格式编写其他业务逻辑的路由啦。
