---
title: hexo教程之三 --- 查错
date: 2015-06-19 17:45:45
categories:
tags: hexo
---
use-hexo

##  问题
>yml配置文件的每个冒号后面必须要**`空格`**

##  部署错误

在Hexo 3.0版本后deploy git 被分开的，所以需要安装，安装命令如下:
npm install hexo-deployer-git --save 
安装好后在尝试一下就ok。

部署的时候执行：hexo deploy 命令行没有任何输出，也没有错误。 
查看配置文件有没有错误，有没有空格


##  文章没有更新
我的建议是直接删除public文件夹，这个就是生成的文章列表，有人说删除.DS*开头的文件也是可以的，删除之后重新部署


##  hexo s无法预览
mac直接在浏览器直访问http://0.0.0.0:4000/,
windows直接在浏览器直访问http://localhost:4000/ 


##  jacman使用多说
wiki上说的是用户名，其实就三级域名的最开始的部分
vsxen.duoshuo.com,所以用户名就是vsxen

如果出现
INFO  Start processing
ERROR Process failed: _posts/test.md
YAMLException: end of the stream or a document separator is expected at line 2, column 5:
    date: 2016-11-04 10:42:42

就是说  text.md的yaml格式错了。日期后面需要加上空格






参考
http://ibruce.info/2013/11/22/hexo-your-blog/
http://fanweiya.thisistap.com/instagram/