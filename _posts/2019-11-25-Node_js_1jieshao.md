---
layout: post
title: "Node.js介绍"
date: 2019-11-25 
description: "Node.js"

tag: 编程语言
---   

## Node.js简介
[RUBOOB.COM](https://www.runoob.com/nodejs/nodejs-npm.html)

- 如果我们使用PHP来编写后段代码时,需要 Apache 或者 Nginx 的 HTTP 服务器,并配上 mod_PHP5 模块 和 PHP-cgi.
- 从这个角度看,整个"接收HTTP 请求并提供Web 页面"的需求就不需要PHP来处理
- 不过对 Node.js 来说,概念完全不一样.使用Node.js 时,我们不仅仅在实现一个应用,同时还实现了整个HTTP 服务器.事实上,我们的web 应用以及对应的服务器基本上是一样的.
- 在我们创建Node.js 第一个 "Hello,World!" 应用前,让我们了解下Node.js应用是由几部分组成:
  - **引入 required 模块**: 我们可以使用 **require** 指令来载入 Node.js 模块
  - **创建服务器:** 服务器可以监听客户端请求,类似于Apache , Nginx 等 HTTP服务器.
  - **接收请求与响应请求** 服务器很容易创建,客户端可以使用浏览器或终端发送HTTP 请求,服务器接收请求后返回响应数据.

## 创建Node.js 应用

 ### 步骤一  引入 require 模块

-  我们使用  **require** 指令来载入http 模块,并将实例化的 HTTP 赋值给变量 http ,示例如下
- `` var http = require("http");`` 

### 步骤二  创建服务器

- 接下来我们使用 http.createServer() 方法创建服务器 ,并使用 listen 方法绑定8080 端口 , 函数通过request,response 参数来接收和响应数据.

- 实例如下,在你项目的根目录下创建一个叫server.js 的文件,并写入以下代码 ：

- ```node.js
  var http = require("http");
  
  http.createServer(function(request,response){
      // 发送HTTP头部
      // HTTP 状态值：200 ：OK
      // 内容类型：text/plain
      response.writeHead(200,{'Content-Type':'text/plain'});    
      
      response.end("Hello World!");    
  }).listen(8080);
  
  console.log('Server running at http://127.0.0.1:8080');
  ```

-  以上代码我们完成了一个可以工作的服务器。

- 使用Node命令执行以上代码：

- `` node server.js``

- ![](https://www.runoob.com/wp-content/uploads/2014/03/cmdrun.jpg )

- 接下来，打开浏览器访问 http://127.0.0.1:8080/ ，你会看到写着一个 ‘Hello World’的网页。

- ![](https://www.runoob.com/wp-content/uploads/2014/03/nodejs-helloworld.jpg)

- 分析Node.js 的服务器：

  - 第一行请求 （require） Node.js 自带的 http 模块，并且把他赋值给 http 变量。
  - 接下来我们调用 http 模块提供的函数：createServer。 这个函数会返回一个对象，这个对象有一个叫 listen 的方法，这个方法有一个数值参数，指定这个HTTP 服务器监听的端口号。

