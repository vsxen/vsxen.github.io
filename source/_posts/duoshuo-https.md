---
title: 全站https之多说使用https头像
date: 2016-12-02 13:03:11
categories: 
tags: hexo 
---
多说官方的头像已经支持https了，但是新浪之类还是http,如果你有自己自己的服务器，而且使用的是nginx,可以轻松的通过nginx的代理模块，达到全站https的要求
如果你用的是github pages可以使用本文的方法
感谢
https://github.com/rainwsy/duoshuo-https
提供缓存

以下摘自eadme

原理 :将https图片转由七牛CDN处理

使用方法

## 方法一:
如果你没有对embed.js 做定制可以直接

-<script src="https://dn-hb0716.qbox.me/embed.js"></script>
## 方法二: 
本地化embed.js
下载embed.js引用到你的网站文件
对应CDN:

http://static.duoshuo.com/ => nznlz6ohs.qnssl.com

http://himg.bdimg.com/ => nzriuc44h.qnssl.com

http://ds.cdncache.org/ => nzrisok3d.qnssl.com

http://img.kaixin001.com.cn/ => nzrktdox3.qnssl.com

http://app.qlogo.cn/ => nzvcelvwu.qnssl.com

http://wx.qlogo.cn/ => nzwsf9aei.qnssl.com

http://hdn.xnimg.cn/ => nzrj4etbg.qnssl.com

http://img.t.sinajs.cn/ => nznlz6ohs.qnssl.com

http://tp4.sinaimg.cn/ => odfhb4m72.qnssl.com

