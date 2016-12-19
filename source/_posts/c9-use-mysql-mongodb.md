---
title: c9使用mysql，mongodb数据库、修改默认密码
date: 2016-11-15 13:01:46
categories:   数据库
tags: 
---

c9.io在之前都说过了，是一个支持多种语言的在线IDE,有时候可能会用到mysql，这么介绍一下如何使用。
## 安装
打开之后，输入`mysql-ctl cli`就可以安装mysql了
可以看到
- Installing MySQL
 * Stopping MySQL database server mysqld
   ...done.
 * Starting MySQL database server mysqld
   ...done.
 * Checking for tables which need an upgrade, are corrupt or were 
not closed cleanly.
MySQL 5.5 database added.  Please make note of these credentials:

默认是没有密码的，这样对于一些应用可能就不能用了，所以需要修改密码。
## 修改mysql密码

1. 停止mysqld； 
/etc/init.d/mysql stop
(您可能有其它的方法,总之停止mysqld的运行就可以了)
2. 用以下命令启动MySQL，以不检查权限的方式启动； 
mysqld --skip-grant-tables &
3. 然后用空密码方式使用root用户登录 MySQL； 
mysql -u root
4. 修改root用户的密码； 
mysql> update mysql.user set password=PASSWORD('newpassword') where User='root'; 
mysql> flush privileges; 
mysql> quit 
重新启动MySQL
/etc/init.d/mysql restart
就可以使用新密码 newpassword 登录了
## mongdb
跟着命令打就可以了
```
$ sudo apt-get install -y mongodb-org
#开始安装  等等就好了

$ mongod --bind_ip=$IP --nojournal
The output will include:

...
waiting for connections on port 27017
# 成功运行了
```
这时候新开一个终端，输入`mongo`就可以连上了