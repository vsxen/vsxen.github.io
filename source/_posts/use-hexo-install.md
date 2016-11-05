---
title: hexo教程之一 ---安装
date: 2015-06-18 17:57:00
categories:  
tags: hexo
---

 本文最后更新于2016-09-13 

hexo是一个基于node生成静态页面的blog程序，基于命令行进行生成，部署。使用hexo需要使用到npm和git，不知道的可以看我以前写的。

##  安装
```
npm install hexo-cli -g#3.20后的版本
npm install -g hexo #这是以前的命令
```
##  初始化
```
mkdir blog
hexo init
npm instll#如果网速慢，可以使用cnpm
```
##  写作
```
hexo new 参数  文章题目#可以简写为hexo n 参数 文章标题
```
参数包括post（文章）、page（页面） 和 draft（草稿）
###  举例
 `hexo n test`（如果是post可以省略）生成标题为test的文章（/sourse/_post下）
`hexo new page about`生成about页面(在/sourse/about/index.md)，修改即可。
`hexo new draft "title" `在source/_drafts中会创建一份md文件.作为草稿.
`hexo generate --draft`在生成时同时生成草稿 
`hexo server --draft` 在本地预览时显示草稿
`hexo publish draft "title"` 把草稿从_draft中移动到_post
##  生成
```
hexo generator#简写为hexo g
```
这条命令会在/public下面生成 静态页面
##  部署
```
hexo deploy #简写为hexo d
```
>部署前要配置_config.yml文件，找到deploy:标签，我的配置如下：

```
deploy:
type: git
repository: https://github.com/vsxen/vsxen.github.io.git
branch: master
```
`hexo 3.0之后 把hexo-deployer-git分离出来了，需要先npm install hexo-deployer-git --save `

如果没有错误的话，就是成功了
