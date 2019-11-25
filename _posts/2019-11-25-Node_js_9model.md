---
layout: post
title: "Node.js 模块系统"
date: 2019-11-25 
description: "Node.js"

tag: 编程语言
---   


## Node.js 模块系统

- 为了让Node.js 的文件可以相互调用，node.js 提供了一个简单的模块系统。
- 模块时Node.js 应用程序的基本组成部分，文件和模块时一一对应的。换言之，一个Node.js 文件就是一个模块，这个文件可能是JavaScript代码、json 或者编译过的C/C++扩展。

### 创建模块

- 在 Node.js 中，创建一个模块一个模块非常简单，如下我们创建一个 main.js 文件，代码如下：

``` 
var hello = require('./hello');
hello.world();
```

- 以上实例中，代码require('hello') 引入了当前目录下的hello.js文件（./为当前目录，Node.js 默认后缀为js）。
- Node.js 提供了 export 和 require 两个对象，其中 exports 时模块公开的接口，require 用于从外部获取一个模块的接口，及所获取模块的 exports 对象。
- 接下来我们就来创建hello.js 文件，代码如下：

``` 
exports.world = function(){
	console.log('hello World');
}
```



- 在以上示例中，hello.js 通过 exports 对象把 world 作为模块的访问接口，在main.js 中通过 require('./hello') 加载这个模块，然后就可以直接访问hello.js 中 exports 对象的成员函数了。
- 有时候我们只是想把一个对象封装到模块中，格式如下：

```
module.exports = function(){
     //....
}
```

- 例如

```
//hello.js 
function Hello() { 
    var name; 
    this.setName = function(thyName) { 
        name = thyName; 
    }; 
    this.sayHello = function() { 
        console.log('Hello ' + name); 
    }; 
}; 
module.exports = Hello;
```

- 这样就可以直接获的这个对象了：

```
//main.js 
var Hello = require('./hello'); 
hello = new Hello(); 
hello.setName('BYVoid'); 
hello.sayHello(); 
```

- 模块接口的唯一变化是使用module.exports = Hello 代替了 exports.world = function(){}。 在外部引用该模块时，其接口对象就是要输出的Hello对象本身，而不是原先的exports。

### 服务端的模块放哪里

- 也许你已经注意到，我们已经在代码中使用了模块了。像这样：

```
var http = require("http");

...

http.createServer(...);
```

- Node.js 中自带了一个叫HTTP 得到模块，我们在我们的代码中请求它并把返回值赋给一个本地变量。
- 这把我们的本地变量变成了一个拥有所有http模块所提供的公共方法的对象。
- Node.js 的 require 方法中的文件查找策略如下：
- 由于Node.js 中存在4类模块（原声模块和3中文件模块），尽管require 方法及其简单，但是内部的加载却是十分复杂的，其加载优先级也是各自不同。如下图所示：

![](https://www.runoob.com/wp-content/uploads/2014/03/nodejs-require.jpg)

- **从文件模块缓存中加载**

- 尽管原声模块与文件模块的优先级不同，但是都会优先从文件模块的缓存中加载已存在的模块。

- **从原声模块加载**

- 原声模块的优先级仅次于文件模块缓存的优先级。require 方法在解析文件名之后，优先检查模块是否在原声模块列表中。以http模块为例，尽管在目录下存在一个http/http.js/http.node/http.json 文件，require("http") 都不会从这些中加载，而是从原声模块中加载。

- **从文件加载**

- 在文件模块中不存在，而且不是原声模块时候，Node.js 会解析 require 方法传入的参数，并从文件系统中加载实际的文件，加载过程中的包装和编译细节在前一节中已经介绍过，这里我们将详细查找文件模块的过程，其中，也有一些细节值得知晓、

- require 方法接受以下几种参数的传递：

  - http、fs、path 等，原声模块
  - ./mod 或 ../mod , 相对路径的文件模块。
  - /pathtomodule/mod，绝对路径的文件模块。
  - mod，非原生模块的文件模块。

  





