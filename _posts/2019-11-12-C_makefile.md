---
layout: post
title: "C语言makeFile的编写"
date: 2019-11-12 
description: "C语言"

tag: 编程语言
---   



## makeFile的编写

检查装没装`make -v`

没有安装终端输入命令  ``suto apt-get install make``（ubuntu）

- ``vim Makefile`` 开始编写

- ``` c
  hello.out:max.o min.o hello.c
  //[tab]键 否则报错
  			gcc max.o min.o hello.c -o hello.out
  max.o:max.c
  			gcc - c max.c
  min.o:min.c
  			gcc -c min.c
  ```

- ```c
  上面解释
  hello.out 获取这个文件  需要操作 :max.o min.o hello.c 等文件
  //[tab]键 否则报错
  			并且需要输入这个命令获取 gcc max.o min.o hello.c -o hello.out
  如果没有max.o 之后会在下面获取max.o文件 开始递归知道完成
  max.o 获取这个文件需要操作:  max.c 文件
  			并且输入命令  gcc - c max.c
  min.o 获取这个文件需要操作:  min.c 文件
  			并且输入命令   gcc -c min.c
  ```

- 之后在外面执行输入命令  `make`

  

