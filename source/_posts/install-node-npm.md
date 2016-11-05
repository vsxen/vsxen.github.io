---
title: 各平台的node安装和npm的简单使用
date: 2015-10-27 18:23:49
categories:  node
tags:  
---


## 安装
>MAC可以使用`brew install node`或者直接去官网下载pkg，安装一路next就行，需要输入密码
linux有三种安装方式
`去官网下载源码，tar make `
软件源安装 `apt-get install nodejs`  `yum install nodejs`(自动安装npm)
利用nvm或者n，二者区别nvm是独立的，而n则是需要先安装npm才可以 `sudo n stable`  `sudo nvm lts`
`node version`和`npm version`可以查看版本号


## npm常用命令
```
npm install <name> --save  #save的作用是将信息写入package.json中
npm init  #会引导你创建一个package.json文件，包括名称、版本、作者这些信息等
npm update <name>#更新
npm ls #列出当前安装的了所有包
npm root #查看当前包的安装路径
npm uninstall <name>
npm rm <name> #卸载某一个包
npm root -g  #查看全局的包的安装路径
npm help  帮助，如果要单独查看install命令的帮助，可以使用的npm help 
```
## 换淘宝源
因为某些域名被墙，所以需要换源
`sudo npm install -g cnpm --registry=https://registry.npm.taobao.org`
以后就可以用cnpm install 代替 npm install。

>MAC 安装全局模块一点要sudo  否则 会出问题。