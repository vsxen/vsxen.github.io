---
title: Ubuntu安装后要做的事
date: 2016-08-21 17:52:19
categories: Linux
tags:
---

##  换源
通常情况下，Ubuntu的软件源都是国外的，下载和更新的时候都特别慢,所以需要换成国内的。以163为例子，`vim /etc/apt/sources.list`
>deb http://mirrors.163.com/ubuntu/ wily main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-backports main restricted universe multiverse

##  系统优化工具
```
sudo apt-get install ubuntu-tweak
sudo apt-get install unity-tweak-tool
```
更改主题的话。可以把图标文件可以安装在/usr/share/themes中，也可以安装在~/.themes中

##  安装chrome
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_i386.deb#36位
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb#64位
dpkg -i  goog tab
```
## 安装geany，sublime编辑器
`sudo apt-get install geany`
sublime需要自己下载，然后tar就行了

##  更改语言
(中文的终端看起来十分别扭)
```
sudo vi /etc/default/locale
 #中文LANG="zh_CN.UTF-8"
 LANGUAGE="zh_CN:zh"
#英文 LANG="en_US.UTF-8"
LANGUAGE="en_US:en"
```

## 安装搜狗
```
sudo add-apt-repository ppa:fcitx-team/nightly
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install fcitx
```
然后直接双击安装下载的deb包就行了

美化方面可以参考https://github.com/lijianying10/FixLinux/blob/master/prob/MacTheme.md