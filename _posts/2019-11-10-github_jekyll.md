---
layout: post
title: "github+jekyll搭建个人网站"
date: 2019-11-10 
description: "github+jekyll搭建个人网站"
tag: 框架使用和安装
---   


### Github+jekyll 搭建个人网站
GitHub搭建个人网站，大家在网上一搜能搜到一大把的教程，但是大部分都讲的差不多，并不能满足自己想搭建的网站详细需求。我之前在搭建本站的时候也是查了较多资料，学习了下jekyll语法，参考了几个主题模板，才把符合我需求网站搭建出来。那么今天我将详细介绍下本站从github代码托管，jekyll安装，jekyll主题选择，jekyll目录结构，jekyll基本语法，jekyll主题修改，网站留言，访问量统计等子功能整入的详细过程。顺便当作自己记录下吧，防止以后忘记了。

### 第一步网站托管
1.首先你要到GitHub上注册一个账号,例如我注册的用户名为：leach-chen（用户名可以在设置里改）

2.点击New repository–>输入仓库名称格式为：用户名.github.io(如：leach-chen.github.io)->点击Create repository

![img](https://upload-images.jianshu.io/upload_images/3700891-ec225bdee10284f2..png?imageMogr2/auto-orient/strip|imageView2/2/w/568/format/webp)
![img](https://upload-images.jianshu.io/upload_images/3700891-a49cc279d54154fe..png?imageMogr2/auto-orient/strip|imageView2/2/w/990/format/webp)
3.浏览器里访问https://leach-chen.github.io/,可以发现这个url可以被访问了，你可以把改仓库拉取到本地，然后在里面新建一个index.html的文件,在里面输入任意内容，然后再把代码推送到git上，然后再访问改链接，可以发现index.html里面的内容被访问到了。

到这里，一个免费且无限流量的github代码托管仓库就创建完成了。

## 第二步  模板放到git服务器

- 第一种  直接把[jekyll](http://jekyllthemes.org/)模板clone下来   直接传到git 服务器里
- 第二种   把你本地jekyll弄的模板  传到git服务器里

