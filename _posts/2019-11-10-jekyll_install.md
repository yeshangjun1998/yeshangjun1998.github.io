---
layout:post
title:"jekyll安装"
date:2019-11-10
description:"Jekyll安装"
tag:Jekyll
---

## Jekyll

### 事先准备

安装 Jekyll 相当简单，但是你得先做好一些准备工作。开始前你需要确保你在系统里已经有如下配置。
- [Ruby](http://www.ruby-lang.org/en/downloads/) (（including development headers, Jekyll 2 需yemian要 v1.9.3 及以上版本，Jekyll 3 需要 v2 及以sudo apt-get install nodejs上版本）)
`` sudo apt-get install ruby-full `` 安装命令
- [RubyGems](https://rubygems.org/pages/download) 
- [NodeJS](https://nodejs.org/en/)或其他 JavaScript 运行环境（Jekyll 2 或更早版本需要 CoffeeScript 支持）。`` sudo apt-get install nodejs`` 安装nodejs
- [[Python 2.7](https://www.python.org/downloads/)]（Jekyll 2 或更早版本） `` sudo apt-get install python ``

###  用RubyGems 安装 Jekyll

安装 Jekyll 的最好方式就是使用 RubyGems 只要打开终端输入一下命令就可以安装了: `` gem install jekyll``

所有的 Jekyll 的 gem 依赖包都会被自动安装，所以你完全不用去担心。如果你在安装中碰到了问题，请查看 [troubleshooting](http://jekyllcn.com/docs/troubleshooting/) 或者 [report an issue](https://github.com/jekyll/jekyll/issues/new) 那么 Jekyll 社区就会帮助你解决问题了。

~ $ gem install jekyll   		//安装jekyll

~ $ jekyll new myblog 		// 创建jekyll 框架

~ $ cd myblog 						//  进入目录

~/myblog $ jekyll serve		// 使用本地服务

  => Now browse to http://localhost:4000 	// localhost:4000 显示项目页面

