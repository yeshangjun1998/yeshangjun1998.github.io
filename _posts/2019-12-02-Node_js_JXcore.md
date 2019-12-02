---
layout: post
title: "Node.js JXcore打包"
date: 2019-12-02 
description: "Node.js"

tag: 编程语言
---   



## JXcore 打包

Node.js 是一个开放源码、跨平台的、用于服务器端和网络应用的运行环境。

JXcore 是一个支持多线程的 Node.js 发行版本，基本不需要你对现有的代码做任何改动就可以直接线程安全的以多线程运行。

### JXcore 安装

下载JXcore 安装包，并解压，在解压的目录下提供了jx 二进制文件命令，接下来我们主要使用这个命令。

### 步骤1 下载

下载 JXcore 安装包 https://github.com/jxcore/jxcore-release，你需要根据你自己的系统环境来下载安装包。

1、Window 平台下载：[Download(Windows x64 (V8))](https://raw.githubusercontent.com/jxcore/jxcore-release/master/0311/jx_win64v8.zip)。

2、Linux/OSX 安装命令：

```
$ curl https://raw.githubusercontent.com/jxcore/jxcore/master/tools/jx_install.sh | bash
```

如果权限不足，可以使用以下命令：

```
$ curl https://raw.githubusercontent.com/jxcore/jxcore/master/tools/jx_install.sh | sudo bash
```

以上步骤如果操作正确，使用以下命令，会输入版本号信息：

```
 jx --version
v0.10.32
```

### 包代码

例如，我们的Node.js 项目包含以下几个文件，其中index.js 时主文件：

```
drwxr-xr-x  2 root root  4096 Nov 13 12:42 images
-rwxr-xr-x  1 root root 30457 Mar  6 12:19 index.htm
-rwxr-xr-x  1 root root 30452 Mar  1 12:54 index.js
drwxr-xr-x 23 root root  4096 Jan 15 03:48 node_modules
drwxr-xr-x  2 root root  4096 Mar 21 06:10 scripts
drwxr-xr-x  2 root root  4096 Feb 15 11:56 style
```

接下来我们使用jx 命令打包以上项目，并指定index.js 为node.js 项目的主文件：

```
js package index.js index
```

以上命令执行成功，会生成以下两个文件：

- index.jxp 这是一个中间文件，包含了需要编译的完整项目信息。
- index.jx  这时完整包信息的二进制文件，可运行在客户端上。

### 载入jx文件

node.js 的项目运行：

> `` node index.js command_line_arguments``

使用JX编译后，我们可以使用以下命令来执行生成的jx二进制文件：

> `` jx indedx.jx command_line_arguments``

更多 JXcore 安装参考：https://github.com/jxcore/jxcore/blob/master/doc/INSTALLATION.md。

更多 JXcore 功能特性你可以参考官网：https://github.com/jxcore/jxcore。