---
title: mysql从零开始学习
date: 2016-05-14 17:43:57
categories: mysql
tags:
---
## 安装
sudo apt-get install mysql

## 启动服务
`sudo service mysql  start`
启动成功
 Starting MySQL database server mysqld                                                  [ OK ] 
 
 Checking for tables which need an upgrade, are corrupt or were not closed cleanly.

### 显示所有表
show databases;
### 选择表
use  表名
database changed
### 创建表 
```
CREATE TABLE 表的名字
(
列名a 数据类型(数据长度),
列名b 数据类型(数据长度)，
列名c 数据类型(数据长度)
);
```
### 插入数据
注意看区别
```
INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110);

INSERT INTO employee VALUES(02,'Jack',119119119);

INSERT INTO employee(id,name) VALUES(03,'Rose');
```
### 查询数据
`SELECT name,age FROM employee;`



SET character_set_database=gbk;
SET character_set_server=gbk;
how variables like 'colla%';show variables like 'char%';
LOAD DATA LOCAL INFILE '/home/ubuntu/workspace/a.txt' INTO TABLE test_01   ;
update  test_01 set age=13 where name='asd';


非root用户从client机器load data local infile至remote mysql server时，报错：
ERROR 1148 (42000): The used command is not allowed with this MySQL version
可能原因（from mysql reference manual）：
If LOAD DATA LOCAL is disabled, either in the server or the client, a client that attempts to issue such a statement receives the following error message:
ERROR 1148: The used command is not allowed with this MySQL version
可见，出于安全考虑，默认是不允许从client host远程通过load data命令导数据的
解决办法：
For the mysql command-line client, enable LOAD DATA LOCAL by specifying the --local-infile[=1]option, or disable it with the --local-infile=0 option
也即，在需要从client host导数据的情况下，登陆mysql时，需用--local-infile[=1]显式指定参数，典型命令形式为：
 mysql --local-infile -u user -ppasswd
登陆成功后，执行load data infile 'filename' into table xxx.xxx即可

INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110);
INSERT INTO employee VALUES(02,'Jack',119119119);
INSERT INTO employee(id,name) VALUES(03,'Rose');
查看列：desc 表名;
修改表名：alter table t_book rename to bbb;
添加列：alter table 表名 add column 列名 varchar(30);
删除列：alter table 表名 drop column 列名;
修改列名MySQL： alter table bbb change nnnnn hh int;
修改列名SQLServer：exec sp_rename't_student.name','nn','column';
修改列名Oracle：lter table bbb rename column nnnnn to hh int;
修改列属性：alter table t_book modify name varchar(22);
truncate table 表名删除
 delete from表名
 　　如果DELETE不加WHERE子句，那么它和TRUNCATE TABLE是一样的，但它们有一点不同，那就是DELETE可以返回被删除的记录数，而TRUNCATE TABLE返回的是0。

 sql语句
 CREATE DATABASE mysql_shiyan;

use mysql_shiyan;

CREATE TABLE department
(
  dpt_name   CHAR(20) NOT NULL,
  people_num INT(10) DEFAULT '10',
  CONSTRAINT dpt_pk PRIMARY KEY (dpt_name)
 );

CREATE TABLE employee
(
  id      INT(10) PRIMARY KEY,
  name    CHAR(20),
  age     INT(10),
  salary  INT(10) NOT NULL,
  phone   INT(12) NOT NULL,
  in_dpt  CHAR(20) NOT NULL,
  UNIQUE  (phone),
  CONSTRAINT emp_fk FOREIGN KEY (in_dpt) REFERENCES department(dpt_name)
 );
 
CREATE TABLE project
(
  proj_num   INT(10) NOT NULL,
  proj_name  CHAR(20) NOT NULL,
  start_date DATE NOT NULL,
  end_date   DATE DEFAULT '2015-04-01',
  of_dpt     CHAR(20) REFERENCES department(dpt_name),
  CONSTRAINT proj_pk PRIMARY KEY (proj_num,proj_name)
 );