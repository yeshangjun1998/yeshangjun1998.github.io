---
layout: post
title: "ubuntu配置阿里源"
date: 2019-11-10 
description: "ubuntu"
tag: 操作系统信息
---   

## ubuntu配置阿里源
1. 第一步:备份原来的源文件
    - `` cd /etc/apt/ ``
    -  然后会显示下面的source.list
    - 输入命令  `` sudo cp sources.list sources.list.bak  ``
    - 就是将sources.list 备份到 sources.list.back

2. 第二步:替换源
    - 阿里云源的文件
	
    ```
     deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse  
    ##测试版源  
    deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse  
    # 源码  
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse  
    ##测试版源  
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse 

    ```
    
    - 打开sources.list 把阿里源文件里的内容复制到 sources.list 文件中
3. 更新源和软件
    - ``  sudo apt-get update `` 更新源
    -  `` sudo apt-get upgrade ``  更新软件

