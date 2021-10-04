---
layout: post
title: "跑通Node全栈(demo版本)(一)---Express安装"
date: 2018-8-02
description: "跑通Node全栈(demo版本)(一)---Express安装"
tag: Vue2
---

### 1.项目介绍

- 该项目工分为使用前端技术完成的简易版学生管理系统。项目分为前端和后端两个部分，前端采用 Vue-cli 脚手架工具搭建。后端采用 express 框架搭建，数据库则选择了 MongoDB 这门轻量级的数据库,完成了最基本的增删改查的功能。先将项目中的业务逻辑打通，后续会补充更复杂的业务需求。

### 2.项目准备

- 关于环境搭建，本文只提供必要的提示。具体安装流程不在本文介绍范围之内,在此不做赘述。

- 必要环境：NodeJs、Vue-cli、mongoDB

### 3.开始项目

- (1)首先我们需要准备自己的后台，具体流程如下

- 使用 NodeJs 全局安装 express 框架

  ```
      npm install express-generator -g
  ```

  安装成功后则可以使用 express 项目名 这条指令创建 express 项目了

  (2)现在 我们就使用 express studentM 这条指令在桌面创建一个 express 项目

  ![](/images/posts/vue/01.png)

  (3)当然，上图展示的文件结构只是基础架构，我们还需要使用 npm(或者 cnpm) install 补全项目依赖，成功后我们会发现文件夹里多了一个 node_modules 文件夹

  ![](/images/posts/vue/02.png)

  (4)运行 npm start,如果成功，在浏览器里输入 localhost:3000 则会出现下图的 express 欢迎页面

  ![](/images/posts/vue/03.png)

- 到此为止,express 后台环境搭建完毕
