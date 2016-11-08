---
title: hexo教程之二 --- 插件
date: 2015-06-18 22:54:00
categories:
tags: hexo
---
本文介绍一下hexo的一些插件，包括部署,站点地图和SEO等等，
官方的收录的插件https://hexo.io/plugins/
其实还有很多官方没有收录的插件，可以再github搜搜试试。
其实在hexo安装成功之后，就已经自带了一些插件，打开package.json文件可以看到，下面的插件都是我安装的，
```
    "hexo": "^3.2.0",
    "hexo-deployer-git": "0.0.4",
    "hexo-generator-archive": "^0.1.2",
    "hexo-generator-category": "^0.1.2",
    "hexo-generator-feed": "^1.2.0",
    "hexo-generator-index": "^0.1.2",
    "hexo-generator-sitemap": "^1.1.2",
    "hexo-generator-tag": "^0.1.1",
    "hexo-git-backup": "^0.1.2",
    "hexo-neat": "^1.0.4",
    "hexo-renderer-ejs": "^0.1.0",
    "hexo-renderer-marked": "^0.2.4",
    "hexo-renderer-stylus": "^0.2.0",
    "hexo-server": "^0.1.2"
```


## Google站点地图
SEO怎么少得了站点地图，这个就是自动生成站点地图的插件，然后在根目录的配置文件加上
```
plugin:
   hexo-generator-sitemap  #站点地图
```
运行`npm install hexo-generator-sitemap  --save`，
然后hexo g就会发现public文件夹多出来一个sitemap.xml了。
百度的 （hexo-generator-baidu-sitemap）。
## 备份插件
主页https://github.com/coneycode/hexo-git-backup
如果是hexo 2.X.X版本
运行 npm install hexo-git-backup@0.0.91 --save
如果是hexo 3.X.X版本
运行 npm install hexo-git-backup --save
配置，目前是自动备份主题，并删除主题目录的.git文件夹
```
backup:
    type: git
    repository:
       github: git@github.com:vsxen/vsxen.github.io.git,back
```
然后运行`hexo back`(hexo b)就可以备份到back分支了。
## 页面压缩
压缩页面可以更快的载入，使用的是https://github.com/rozbo/hexo-neat
安装`npm install hexo-neat --save`
配置(文章内不能有左右标签<>)
```
neat_enable: true
neat_html:
  enable: true
  exclude:
neat_css:
  enable: true
  exclude:
    - '*.min.css'
neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '*.min.js'
```
## 添加keyword
如果你使用jacman的话,可以在`_config.yml`后面添加
```
keywords: 忆流年,yiliunian,Linux
```
## feed插件
运行hexo-generator-feed 安装插件，
然后再配置文件加上
```
plugin:
   hexo-generator-feed #rss输出
```
运行hexo g就可以在public看到atom.xml了。 