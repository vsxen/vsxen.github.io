---
title: linux-mount-webdav-yandex
date: 2016-11-04 07:38:41
categories: Linux
tags:
---
什么是webdav，是一组基于超文本传输协议的技术集合，有利于用户间协同编辑和管理存储在万维网服务器文档。国外的很多网盘，包括owncloud都支持webdav,本文以yandex为例子介绍，挂载在Linux上。
##  介绍
Linux
- davfs2或者fusedav将WebDAV共享挂载成Coda或者FUSE文件系统。
- KDE将WebDAV作为kio_http的一部分提供原生支持。Dolphin，Konqueror等其他KDE应用程序可以直接与WebDAV服务器交互。
- Nautilus也提供内置支持。
- cadaver命令行工具提供类FTP命令集，也包含在很多Linux发行版中。
- Apache HTTP 服务 提供基于davfs和Apache Subversion的WebDAV 模块。

Windows
- NetDrive：挂载为网络硬盘机

Mac
- Finder：系统内置程式
本文就是利用davfs2挂载wendav。

## 安装
Linux主要的源中都有davfs2,也可以自己编译，需要准备好环境。
```
apt-get install davfs2
mkdir /mnt/webdav
mount -t davfs https://webdav.yandex.ru /mnt/webdav
Please enter the username to authenticate with server
https://webdav.yandex.ru or hit enter for none.
  Username: test
Please enter the password to authenticate user test with server
https://webdav.yandex.ru or hit enter for none.
  Password: 
```
## 配置
可以把账号密码写入配置文件，以普通用户来挂载。
`usermod -a -G network username`
编辑 `/etc/fstab`文件，在后面添加（username自己替换）:
`https://webdav.example.com /home/username/webdav davfs user,noauto,uid=username,file_mode=600,dir_mode=700 0 1`

创建账号密码配置:
```
mkdir ~/.davfs2/
echo "https://webdav.example.com webdavuser webdavpassword" >> ~/.davfs2/secrets 
chmod 0600 ~/.davfs2/secrets
```
yandex  url是
`https://webdav.yandex.ru`

如果是owncloud, url是:
`https://webdav.example.com/remote.php/webdav`


多用户配置
```
/home/username/disk1 webdavuser1 "webdavpassword1"
/home/username/disk2 webdavuser1 "webdavpassword2"
.........
/home/username/diskN webdavuserN "webdavpasswordN" 
```
Now you should be able to mount and unmount ~/webdav:
`mount ~/webdav`

取消挂载
`fusermount -u ~/webdav`

## 错误
如果在复制剪切文件遇到错误，编辑`/etc/davfs2/davfs2.conf`，修改配置如下，
```
[...]
use_locks 0
[...]
```


参考
https://wiki.archlinux.org/index.php/Davfs
https://yandex.com/support/disk/webdav.html
https://zh.wikipedia.org/wiki/WebDAV