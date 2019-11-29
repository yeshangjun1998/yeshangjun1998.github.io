---
layout: post
title: "Node.js 终端聊天室"
date: 2019-11-28 
description: "Node.js"

tag: 编程语言
---   



## 终端聊天室

- 使用socket 和net 写的终端聊天室

1. 创建文件 server.js    服务器端

Net 模块提供了一些用于底层的网络通信的小工具，包含了创建服务器/客户端的方法，我们可以通过以下方式引入该模块：

```
//使用net 模块
var net = require('net');
var clientList = [];	//创建变量

// 创建一个tcp服务器 使用socket
var server = net.createServer(function (socket) {
	// 如果有人连接  则把连接用户追加到clientList 变量里
	clientList.push(socket);
	// socket 打印success
	socket.write("success!\r\n");
	// socket 监听 data   如果客户传值 则执行函数体	
	socket.on('data',function(data) {
		// 打印用户传过来的数据
		console.log(data.toString());
		// 使用函数 实参为用户传过来的数据
		broadcast(data);
	});
	//  监听end  
	socket.on('end',function(){
		socket.write('end');
	});
});

// tcp 服务器监听 8080端口  127.0.0.1 ip
server.listen(8080,'127.0.0.1');

// 函数 	data 形参
function broadcast(data){
	//for 循环
	for(var i = 0;i<clientList.length;i++){
		clientList[i].write(data);
	}
}
```

### 创建client.js  客户端

#### process 对象

process 对象是一个全局变量，它提供当前 Node.js 进程的有关信息，以及控制当前 Node.js 进程。 因为是全局变量，所以无需使用 require()。

process.argv 属性返回一个数组，这个数组包含了启动Node.js进程时的命令行参数，

其中：

数组的第一个元素process.argv[0]——返回启动Node.js进程的可执行文件所在的绝对路径

第二个元素process.argv[1]——为当前执行的JavaScript文件路径

剩余的元素为其他命令行参数

```
// 引入net模块
var net = require("net");
var hostname = process.argv[2]; // 参数1
var port = process.argv[3];				// 参数2
var name = process.argv[4];  		// 参数3

// 连接tcp 服务器  host为参数1  port 为参数2   name 为参数3
var client = net.connect({host:hostname,port:port,name:name},
	function(){
		console.log('连接服务器');
		// 设置编码为utf8
		process.stdin.setEncoding('utf8');
		// 监听 readable
		process.stdin.on('readable',function(){
        	// 读取终端写入的内容赋值给变量chunk
			var chunk = process.stdin.read();
			// 判断是否写入
			if(chunk !== null){
				//  客户端 写入 姓名：输入内容 
				client.write(name + ":  "+chunk);
			}
		});
	});
	
	// 监听 data  
	client.on('data',function(data){
		// 打印服务器发送过来的数据
		console.log(data.toString());
	});
	
	// 监听end
	client.on('end',function(){
		// 打印关闭连接
		console.log('关闭连接');
	});

```

