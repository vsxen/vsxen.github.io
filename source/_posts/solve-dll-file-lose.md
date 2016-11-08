---
title: 无法启动此程序,因为计算机中丢失MSVCR110.dll的解决方法
date: 2016-11-08 13:33:47
categories:
tags:
---
千万不要相信百度上面让注册dll文件的方法
千万不要相信百度上面让注册dll文件的方法
千万不要相信百度上面让注册dll文件的方法
  今天在给win10装wamp时出现了几个错误。错误提示都是提示丢失MSVCR110.dll。共出现两次。一是httpd.exe提示，二是php-win.exe提示。我去找dll网站找该dll未能找到，之后自习百度后获得了一下解决方法，安装一个vcredist_x（系统位数）.exe，此方法可行。

原文如下：

​“对于32位系统，安装Wampserver 后启动的时候提示系统错误：MSVCR110.dll丢失。

于是卸载原来的WAMPSERVER 。安装vcredist_x86.exe，重新安装WAMPSERVER 2之后，问题解决了

对于64位系统，则需要下载wampserver 64位版，并且安装vcredist_x64.exe 

64位下载地址：

vcredist_x64.exe 和vcredist_x86.exe下载地址：http://www.microsoft.com/zh-cn/download/details.aspx?id=30679  ”

提示一下：

如果是64位系统安装了32位的wamp，需将该文件的64.32位都安装上，才不会报错。