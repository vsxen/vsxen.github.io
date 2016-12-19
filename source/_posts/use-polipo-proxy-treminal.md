---
title: 用polipo为终端设置代理
date: 2016-09-28 19:55:47
categories: Linux
tags: 小技巧
---
简介：polipo是什么？它是一个由C语言编写的开源的超轻量的http代理工具，本文就是用它来做终端的代理
git clone 的速度超慢，本片文章就是叫你如何加速git clone等一系列需要在终端FQ的操作。
首先你需要会使Shadowsocks，Shadowsocks是我们常用的代理工具，它使用socks5协议，而终端很多工具目前只支持http和https等协议，对socks5协议支持不够好，所以我们为终端设置shadowsocks的思路就是将socks协议转换成http协议，然后为终端设置即可。
##  安装
```
Fedora安装
yum install polipo
Mac下使用Homebrew安装
brew install polipo
#如果brew被墙，可以自己下载后jichong'm重命名到`/Library/Caches/Homebrew/`，就是homebrew 的缓存目录
Ubuntu安装
sudo apt-get install polipo
```
## 配置
一般来说配置文件在 `/etc/polipo/config`，你也可以新建一个（在`~/.polipo`也可以）
内容如下
```
#必填
socksParentProxy = "localhost:1080"
socksProxyType = socks5
#可选
logFile=/var/log/polipo
logLevel=4
```

##  运行
`pilipo &`就可以放入后台了，默认的http代理端口是8123,如果被占用，可以自己修改端口，或者关闭8123端口的程序。
##  测试
```
$ curl ip.gs
当前 IP：125.*.*.14 来自：中国* 联通
$ http_proxy=http://localhost:8123 curl ip.gs
当前 IP：210.*.193.* 来自：*本 
#这就是可以了
```
##  别名
bash中有一个很好的东西，就是别名alias. Linux用户修改~/.bashrc，Mac用户修改~/.bash_profile文件，增加如下设置,zsh就不需要我说了吧
`alias hp="http_proxy=http://localhost:8123"`
然后Linux用户执行source ~/.bashrc，Mac用户执行source ~/.bash_profile生效
之后就可以在命令前加上hp使用polipo
```
$ curl ip.gs
当前 IP：125.*.*.14 来自：中国* 联通
$ hp curl ip.gs
当前 IP：210.*.193.* 来自：*本 
#这就是可以了
```
这样只是对这个终端有效，如果想打开终端就启用polipo可以将export http_proxy=http://localhost:8123加入.bashrc或者.bash_profile文件

参考
http://droidyue.com/blog/2016/04/04/set-shadowsocks-proxy-for-terminal/