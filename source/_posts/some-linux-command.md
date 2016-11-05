---
title: Linux命令讲解之一---dig，screen，
date: 2016-05-14 17:38:02
categories: Linux
tags:
---
本文介绍一下Linux有用的命令，可以给日常使用以及服务器维护带来一点的方便。
## dig
dig即Domain Information Groper。是常用的域名查询工具，可以用来测试域名系统工作是否正常。
### 安装
>yum install bind-utils

###  查询
```
 dig @8.8.8.8 vsxen.github.io#指定dnssome

; <<>> DiG 9.8.3-P1 <<>> @8.8.8.8 vsxen.github.io
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36253
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;vsxen.github.io.		IN	A

;; ANSWER SECTION:
vsxen.github.io.	3599	IN	CNAME	github.map.fastly.net.
github.map.fastly.net.	2651	IN	CNAME	prod.github.map.fastlylb.net.
prod.github.map.fastlylb.net. 19 IN	A	151.101.100.133

;; Query time: 158 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Thu Oct  6 13:18:47 2016
;; MSG SIZE  rcvd: 123




## screen
如果你远程登录了服务器，突然网络断了，那么命令就会停止，而screen就是用来解决这个问题的。
### 安装
>yum install screen #centos系
apt-get install screen#debian系

###  常用命令
```
screen -S docker   # 新建一个名叫docker的session，并马上进入
screen -ls            #列出当前所有session
screen -r docker   恢复到zhouxiao这个session，#前提是已经是断开状态（-d可以远程断开会话）
screen -wipe          #检查目前所有的screen作业，并删除已经无法使用的screen作业
```
 
### 快捷键

- Ctrl+a w    #显示所有窗口列表
- Ctrl+a k    #这个快捷键杀死当前的窗口，同时也将杀死这个窗口中正在运行的进程
- Ctrla  d    #detach，暂时离开当前session

参考(http://www.cnblogs.com/mchina/archive/2013/01/30/2880680.html)
 