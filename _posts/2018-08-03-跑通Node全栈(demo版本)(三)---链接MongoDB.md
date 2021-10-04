---
layout: post
title: "跑通Node全栈(demo版本)(三)---链接MongoDB"
date: 2018-8-03
description: "跑通Node全栈(demo版本)(三)---链接MongoDB"
tag: Vue2
---

上一章我们已经利用 express 写一个基础的路由,本章我们教大家如何用 express 链接 mongodb 数据库。

### 1.安装 mongoDB 并编写数据库操作逻辑

- 做后台怎能离得开数据库呢,首先我们需要使用 npm install mongodb --save 这条指令安装 mongodb

```
    npm install  mongodb  --save
```

- 在项目根目录下创建操作数据库的操作文件,并编写数据库增删改查的业务逻辑,在此贴出代码

  ![](/images/posts/vue/14.png)

```
    var mongodb=require("mongodb");
    var MongoClient=mongodb.MongoClient;
    var url="mongodb://127.0.0.1:27017";
    var DBNAME="studentManger";

    //添加数据
    var  insert=function(collection,data,callback,client){
      collection.insert(data,function(err,result){
                if(err){
                console.log("插入操作失败")
              }else{
                callback(result);
              }
              client.close();
      })
    }
    //删除数据
    var  deletes=function(collection,data,callback,client){
      collection.remove(data,function(err,result){
                  if(err){
                console.log("删除操作失败")
              }else{
                callback(result);
              }
              client.close();
      })
    }
    //修改数据
    var  update=function(collection,data,callback,client){
      collection.updateOne(data[0],data[1],function(err,result){
                  if(err){
                console.log("修改操作失败")
              }else{
                callback(result)
              }
              client.close();
      })
    }
    //查询数据
    var  find=function(collection,data,callback,client){
      collection.find(data).toArray(function(err,result){
              if(err){
                console.log("查询操作失败")
              }else{
                callback(result)
              }
              client.close();
      })
    }

    var  methodType={
      insert:insert,
      update:update,
      delete:deletes,
      find:find
    }


    module.exports=function(type,collections,data,callback){
      MongoClient.connect(url,function(err,client){
        if(err){
          console.log("失败"+err);
        }else{
          var db=client.db(DBNAME);
          var collection=db.collection(collections);
          console.log("数据库链接成功!数据库名: "+db.s.databaseName+" 集合名: "+collection.s.name);
            methodType[type](collection,data,callback,client);

        }
      })
    }
```

- 注:我这里的 mongo 端口号是 27017,数据库名称为 studentManger,查询的集合名为 student,可自行修改

### 2.测试连接是否成功

- 接着我们在 index.js 中编写一个测试接口,用来显示 studentManger 中的数据,以测试访问是否成功。注：这里 studentManger 中的数据需要自行添加,本文不介绍 mongoDB 的基本语法。另外测试的时候大家只需要录入任意数据结构的信息。具体学生管理系统的数据结构会在后续贴出。

(1)首先,我们需要在 index.js 中引入 db-min-pro.js 中暴露出来数据库的操作句柄

```
   var DBHandler=require("../db-min-pro.js")
```

(2)接着编写路由,使用 DBHandler 查询数据

```
    router.get('/testDB', function(req, res, next) {
      DBHandler("find","student",{},function(result){
        res.send(result);
      })
    });
```

(3)重启服务器,在浏览器里输入对应接口,若成功则会弹出如下结果,我们可以看到服务器已经将数据库中的数据成功返回了出来。

![](/images/posts/vue/15.png)

### 3.编写前端静态页面

- 当然啦,萌萌哒的用户不可能聪明到每个请求都到浏览器中手动输入接口,所以我们还需要给一个静态页面让用户可以点击后进行相关访问和操作。在这里我们以表单为例,编写一个静态页面。

- 首先,我们在 express 的静态资源托管文件夹 pubilc 中创建一个 testDB.html 文件,并指定数据访问的地址。然后在服务器中访问该页面,点击提交,OK!和在浏览器直接访问的效果是一样的。

![](/images/posts/vue/16.png)

- 至此,我们连接上数据库后的后台访问接口的逻辑就算打通啦！下一章我们将介绍如何使用 Vue 作为前端向后台请求和发送数据。
