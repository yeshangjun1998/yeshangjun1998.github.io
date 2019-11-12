---
layout: post
title: "使用jekyll搭建本地博客"
date: 2019-11-10 
description: "使用jekyll搭建本地博客"
tag: 框架使用和安装
---   


## jekyll
### 下载模板
- [jekyll模板](http://jekyllthemes.org/) 下载自己合适的博客模板  点击`` demo``演示 如果可以点击 `` homepage`` 进入github 代码库 

- 进入代码库之后  打开终端在你的文件目录下面输入 `` git clone 库网址`` 命令  把项目克隆下来 

### 使用 jekyll

- 在终端目录输入命令  `` jekyll new 目录名`` 创建jekyll框架
- cd 目录名  进入框架   输入 `` jekyll serve `` 开启jekyll 服务
- 网页ip地址输入  localhost:4000  查看项目是否正常
- 除了 Gemfile  Gemfile.lock  两个文件 剩下的全部删除
- 把下载的模板所有文件复制到你的jekyll框架目录下(不包括Gemfile  Gemfile.lock)
- 模板传好之后输入 ``jekyll serve`` 再次开启服务查看模板是否能正常使用
- 如果能使用就开始慢慢调成自己想修改的内容

