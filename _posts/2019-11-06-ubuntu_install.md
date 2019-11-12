---
layout: post
title: "安装ubuntu 系统"
date: 2019-11-06 
description: "ubuntu 系统"
tag: 操作系统信息
---   

<center><h1>ubuntu系统安装</h1></center>
1. ### 下载ubuntu[镜像](https://ubuntu.com/download/desktop)

2. ### 准备一个空u盘准备安装ubuntu启动镜像

   1. 下载软通牒 会提示注册,选择继续试用就好
   2. 使用软通牒 把镜像写入U盘中

3. ### 修改启动项

   1. ​	百度搜索自己电脑牌子的U盘启动
   2. 联想为例 :重启电脑，一直狂戳`F2`(有的电脑是F1，有的电脑是`Esc`,请自行查询)，直到进入BIOS，点击方向箭头→ 移动到Security，再按↓移动到Secure Boot上，点击`回车键`，选择`Disable`；

   ![Alt text](/home/yeshangjun/图片/11037888-3018f929a665a835.webp)

   3. 当然，最好去Boot里面看看USB Boot是否为`Enabled`；![Alt text](/home/yeshangjun/图片/11037888-3884606d11a079b1.webp)

      

      4. 最后，按`F10`保存退出。
         （更新）这里有个问题，改完SATA Controller Mode装完Ubuntu后无法进入Windows的解决方案是改完进入Windows的安全模式，然后重启就正常了

   4. ### 开始安装

      1. 重启进去你的电脑品牌界面时，一直狂戳`F12`,在出现的界面选择你的U盘，如我的这里有个明显的"USB 3.0"，请自行甄别。

         ![Alt text](/home/yeshangjun/图片/2.webp)

      2. 等待一会便进入启动选项，不用动，就选择`Try ubuntu whthout install`，可以先看看Ubuntu在你的电脑上的运行状况再安装。 也可以直接   ` insert` 安装

      3. 进入Ubuntu后，如果你觉得正常，便可以点击左上角的`Install Ubuntu 18.04LTS` ；

         ![Atl text](/home/yeshangjun/图片/11037888-fb59726dd32d7913.webp)

      4. .首先选择语言为中文(简体)，点继续；

      5. 之后按照指示挨个选择

   5. ### 安装完成之后 重新启动拔下u盘