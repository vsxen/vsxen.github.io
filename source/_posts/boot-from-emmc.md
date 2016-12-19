---
title: banan-pi把系统烧录到emmc
date: 2016-12-18 09:23:18
categories: 
tags: bananapi 
---
香蕉派从emmc启动的方法，理论适合所有的香蕉派
## 启动
首先用sd卡正常启动系统
说一下香蕉派的启动顺序，
如果有SD卡，从SD卡启动
SD卡于emmc都有系统，优先从emmc启动
## SD卡放入系统
## 烧录
运行`fdisk -l`一般来说  emmc是/dev/mmcblk1
可能就想下图
![](/img/burn-linux1.jpg)
然后

`sudo dd if=ubuntu.img of=/dev/mmcblk1 bs=10MB`

![](/img/burn-linux2.jpg)

等到烧录成功之后
拔出SD卡就可以从emmc启动了


参考
https://bananapi.gitbooks.io/bpi-m3/content/zh/howtoburnlinuximagetoemmc.html