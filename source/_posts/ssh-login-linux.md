---
title: ssh免密码登录服务器
date: 2016-09-20 11:06:27
categories: Linux
tags:
---
简介：SSH是一个专为远程登录会话和其他网络服务提供安全性的协议。默认状态下SSH链接是需要密码认证的，可以通过添加系统认证（即公钥-私钥）的修改，修改后系统间切换可以避免密码输入和SSH认证，之前介绍的github免密码推送代码用的就是ssh协议。
对信息的加密和解密采用不同的key，这对key分别称作private key和public key，其中，public key存放在欲登录的服务器上，而private key为特定的客户机所持有。
当客户机向服务器发出建立安全连接的请求时，首先发送自己的public key，如果这个public key是被服务器所允许的，服务器就发送一个经过public key加密的随机数据给客户机，这个数据只能通过private key解密，客户机将解密后的信息发还给服务器，服务器验证正确后即确认客户机是可信任的，从而建立起一条安全的信息通道。
通过这种方式，客户机不需要向外发送自己的身份标志“private key”即可达到校验的目的，并且private key是不能通过public key反向推断出来的。这避免了网络窃听可能造成的密码泄露。客户机需要小心的保存自己的private key，以免被其他人窃取，一旦这样的事情发生，就需要各服务器更换受信的public key列表。
## 生成公钥
本机运行`ssh-keygen`一路回车就可以了
其中ssh-keyen可以有参数
```
 -t指定算法
 -f 指定生成秘钥路径
 -N 指定密码
```
查看是否成功 `ls  ~/.ssh/`
## 复制公钥
```
scp id_rsa.pubroot@ip:~/.ssh/ 
#The authenticity of host '192.168.1.3(192.168.1.3)' can't be established.  ...
#输入yes
#输入密码
cat id_dsa.pub >> ~/.ssh/authorized_keys  
chmod 600 ~/.ssh/authorized_keys  #设置权限
chmod 700 -R .ssh  
```

## 登录 
`ssh root@ip` 
如果不出错的话就登录成功了。
`文件和目录的权限千万别设置成chmod 777.这个权限太大了，不安全，数字签名也不支持。`
参考
http://blog.csdn.net/leexide/article/details/17252369
