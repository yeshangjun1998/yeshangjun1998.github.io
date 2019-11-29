---
layout: post
title: "Node.js 简易聊天室"
date: 2019-11-28 
description: "Node.js"

tag: 编程语言
---   



## 使用Node.js 写 聊天室

- 此聊天室是使用node.js + Express 框架 + socket.io 的简单及时通讯。

套接字（socket）是一个抽象层，应用程序可以通过它发送或接收数据，可对其进行像对文件一样的打开、读写和关闭等操作。套接字允许应用程序将I/O插入到网络中，并与网络中的其他应用程序进行通信。网络套接字是IP地址与端口的组合。

![](https://img-blog.csdn.net/20171101151103629?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvend3MTk4NDc3NDM0Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



### 1. 初始化一个Node 项目：

> ```
> mpm init     //一路回车
> ```

### 安装socket.io 在文件夹里打开终端输入命令 `` npm  install  socket.io``

### 2. 安装依赖

> ```
> npm install express
> // 安装 express 框架
> npm install socket.io
> //安装socket.io 
> ```

### 3.server.js 创建服务，监听socket

> ```Node
> var express = require('express');  			//引入express框架
> var app = express(); 									//使用express
> 
> // 把框架放进  http服务器 
> var server =require("http").createServer(app);  
> // 使用socket.io 监听http 服务器
> var io = require("socket.io").listen(server);
> 
> var users = [];
> 
> //将当前所有的文件文件夹 写入服务器 （静态文件）
> app.use('/',express.static(__dirname+'/'));
> // 监听端口
> server.listen(8088);
> 
> // socket 监听 connection 
> io.sockets.on('connection',(socket)=>{
> 	//处理操作
> })
> ```

### 4. 客户端连接socket

> ```
> //var socket = io.connect();
> // 连接socket 监听的服务器
> var socket = io.connect('http://127.0.0.1:8088');
> ```

### 5. socket 事件触发

> ```
> //发事件给单用户
> socket.emit('receive_message',newData);
>// 发事件给所有用户
> socket.broadcast.emit('receive_message',newData);
>```
> 

### 上面只是介绍socket使用 下面是聊天室的完整代码

## 完整代码

### index.html   客户端

> ```
> <!DOCTYPE HTML>
> 	<html>
> 		<head>
> 			<meta charset = "utf-8">
> 			<title>Socket.IO Example</title>
> 		</head>
> 		<body>
> 			<h1>Socket.IO 及时通讯</h1>
> 			<p id="count"></p>
> 			<form id="message-form" action="#" style="display: flex; flex-direction: row; align-items: center;">
> 				 <textarea id="message" rows="2" cols="30"></textarea>
>       				<input type="submit" value="发送" style="background-color: blue; width: 50px; height: 30px; margin-left: 10px; color: white" />
>     		</form>
>     		<div id="msg"></div>
>     		<!-- 引入jQuery 文件 -->
>     		<script type="text/javascript" src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
>     		<script src="socket.io/socket.io.js"></script>
> 		</body>
> 		<script>
> 			//连接socket
> 			var socket = io.connect('http://127.0.0.1:8088');
> 			// 给监听login的 函数传值
> 			socket.emit('login',{username:'user'+new Date().getTime()});
> 			
> 			//监听 users  如果服务器给users发送内容则执行函数体
> 			scoket.on('users',function(data){
> 				$("#count").text('当前在线人数：' +data.number);
> 			});
> 			
> 			//获取 id为message对象
> 			var message = document.getElementById("message");
> 			//message的form 如果提交则执行函数体 
> 			$(nessage.form).submit(function(){
> 				// 给 监听message 传值     (message.value则是你要发送的内容)
> 				socket.emit('message',{text:message.value});
> 				return false; 			//阻止默认事件  	(阻止表单提交)
> 			})
> 			
> 			//接收消息 
> 			socket.on('receive_message',function(data){
> 				$('#msg').append('<p>'+data.user+'说'+data.txt+'</p>');
> 			})
> 			
> 		</script>
> 	</html>
> ```

### server.js 服务器端

> ```
> //引入express 框架
> var express = require("express");
> var app = express();   //使用框架
> 
> // 把框架放到http服务器里
> var server = require('http').creaetServer(app);
> //使用socket 监听 HTTP服务器
> var io = require('socket.io').listen(server);
> 
> //创建users 变量(存放客户端用户)
> var  users=[];
> 
> // 将所有文件文件夹写入到 服务器中  (静态文件)
> app.use("/",express.static(__dirname+'/'));
> server.listen(8088);	 	// 监听HTTP端口
> 
> // 使用 socket 监听 connection 如果客户端连接则执行函数体
> io.sockets.on('connection',(socket)=>{
> 	//失去连接
> 	socket.on('disconnect',function(){
> 		// 判断users 里面是否有客户端传过来的用户名
> 		if(users.indexOf(socket.username)>-1){
> 			//如果由则删除客户端用户
> 			//splice(方法向/从数组中添加/删除项目，然后返回被删除的项目。)
> 			users.splice(users.indexOf(socket.username),1);
> 			console.log(socket.username+'=====>disconnected');
> 		}
> 		
> 		//发送给所有客户端   
> 		socket.broadcast.emit('users',{number:users.length});
> 	});
> 	
> 	//如果客户端给message 发送信息 执行函数体
> 	socket.on('message',function(data){
> 		//定义一个唯一变量  (data.text  是客户端传过来的信息)
> 		let newData = {text:data.text,user:socket.username}
> 		
> 		// 把newData 发送给单用户
> 		socket.emit('receive_message',newData);
> 		//把newData  发送给所有用户
> 		socket.broadcast.emit('receive_message',newData);
> 	});
> 	
> 	
> 	//监听 login 
> 	socket.on('login',function(data){
> 	//如果users里 查找到 data.username则执行函数体
> 	 if(users.indexOf(data.username)>-1){
> 
>         }else{
>           socket.username = data.username;
>          //将用户信息 插入到users里
>          users.push(data.username);
>           // 统计连接数
>           socket.emit('users',{number:users.length});  // 发送给自己
>           socket.broadcast.emit('users',{number:users.length}); // 发送给其他人
>         }
> 
> 	});
> 	
> });
> ```





----------------------------------------

原文链接：https://blog.csdn.net/zww1984774346/article/details/78414384