---
title: 忘记mysql密码，修改mysql密码
date: 2016-11-15 13:26:30
categories: mysql
tags:
---

## 修改mysql密码
`flush privileges`这条命令是刷新权限，
### my.cnf

工具 编辑器
1. 修改MySQL的登录设置： 
` vi /etc/my.cnf `
在[mysqld]的段中加上一句：skip-grant-tables 保存并且退出vi。
2. 重新启动mysqld 
 /etc/init.d/mysqld restart  ( service mysqld restart )
3. 登录并修改MySQL的root密码
```
mysql> USE mysql ; 
mysql> UPDATE user SET Password = password ( 'newpassword' ) WHERE User = 'root' ; 
mysql> flush privileges ; 
mysql> quit
```
4．将MySQL的登录设置修改回来 
将刚才在[mysqld]的段中加上的skip-grant-tables删除 
保存并且退出vi。
5．重新启动mysqld 
 `/etc/init.d/mysqld restart   ( service mysqld restart )`
### safe_mysqld 

1. KILL掉系统里的MySQL进程； 
killall -TERM mysqld
2. 用以下命令启动MySQL，以不检查权限的方式启动； 
safe_mysqld --skip-grant-tables &
3. 然后用空密码方式使用root用户登录 MySQL； 
mysql -u root
4. 修改root用户的密码； 
```
mysql> update mysql.user set password=PASSWORD('新密码') where User='root'; 
mysql> flush privileges; 
mysql> quit 
```
重新启动MySQL，就可以使用新密码登录了
 
有可能你的系统没有 safe_mysqld 程序(比如我现在用的 ubuntu操作系统, apt-get安装的mysql) 
就可以用下面方法可以恢复
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


转载于
http://lxsym.blog.51cto.com/1364623/477027