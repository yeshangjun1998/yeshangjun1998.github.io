---
layout: post
title: "Node.js 函数"
date: 2019-11-28 
description: "Node.js"

tag: 编程语言
---   


## Node.js 函数

在JavaScript中,一个函数可以作为另一个函数的参数。我们可以先定义一个函数，然后传递，也可以在传递参数的地方直接定义函数。

```
创建一个.html文件
<script>
	function say(word){
		console.log(word);
	}
	
	function execute(someFuncition,value){
		someFunction(value);
	}
	
	execute(say,"Hello");
</script>
```

- 以上代码，我们把say函数作为execte函数的第一个变量进行了传递。这里传递的不是say的返回值，而是say 本身!
- 这样以来，say 就变成了 execute 中的本地变量 someFunction，execute 可以通过someFunctio() (带括号的形式) 来使用say函数。
- 当前，因为say 有一个变量，execute 在调用 someFunction时可以传递这样一个变量

### 匿名函数

- 我们可以把一个函数作为变量传递。但我们不一定要绕这个"先定义，在传递"的圈子，我们可以直接在另一个函数的括号中定义和传递这个函数：

```
function execute(someFunction,value){
	someFunction(value);
}

execute(function(word){console.log(word)},"hello");
```

- 我们在execute 接收第一个参数的地方直接定义了我们准备传递给execute的函数。
- 用这种方式，我们甚至不用给这个函数起名字，这也是为什么他被叫做匿名函数。

### 函数传递是如何让HTTP服务器工作的

- 带着这些知识，我们再来看看我们简约而不简单的HTTP服务器：

```
var http = require("http");

http.createServer(function(request,response){
	response.writeHead(200,{"Content-Type":"text/plain"});
	response.write("Hello World");
	response.end();
}).listen(8888);
```

- 现在他看上去应该清晰了很多：我们向createServer 函数传递了一个匿名函数。
- 用这样的代码也可以达到同样的目的：

```
var http = require("http");

function onRequest(request,response){
 	response.writeHead(200, {"Content-Type": "text/plain"});
  	response.write("Hello World");
  	response.end();
}
http.createServer(onRequest).listen(8888);
```



