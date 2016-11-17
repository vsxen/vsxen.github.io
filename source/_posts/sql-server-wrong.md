---
title: sql server的一些错误以及解决方法
date: 2016-11-16 14:02:04
categories: 
tags: sqlserver
---

安装一路继续就行，默认的是只能通过windows登陆认证的，可以安装之后修改
如果SQL Server 2008 的 SQL Server Management Studio连接不上，并且出现
“在与 SQL Server 建立连接时出现与网络相关的或特定于实例的错误。未找到或无法访问服务器。请验证实例名称是否正确并且 SQL Server 已配置为允许远程连接。 (provider: 命名管道提供程序, error: 40 - 无法打开到 SQL Server 的连接)“
可以按照下面的步骤来做，就好了
打开Sql server 管理配置器或者在命令行输入：SQLServerManager10.msc

![](/img/sql-1.jpg)
![](/img/sql-2.jpg)
![](/img/sql-3.jpg)
然后重启一个sql server的服务，重新打开SQL Server Management Studio，在服务器名称输入：(local)或者127.0.0.1，即可登录数据库了。


### 错误信息：已更新或删除的行值要么不能使该行成为唯一行，要么改变了多个行（２行）

请更正错误，并重试删除该行

出现这个是因为没有设置主键，导出表中的数据，新建表，并设置主键就可以了


###  修改数据库表结构时提示【不允许保存更改。您所做的更改要求删除并重新创建以下表。您对无法重新创建的标进行了更改或者启用了“阻止保存要求重新创建表的更改"选项。】
错误源：Microsoft VisualStudio.DataTools.

就是不允许更改表

工具-〉选项-〉左侧有个 设计器-〉表设计器和数据库设计器 -> 阻止保存要求重新创建表的更改(右侧) 把钩去掉即可。

参考
http://www.bkjia.com/MsSql/937081.html