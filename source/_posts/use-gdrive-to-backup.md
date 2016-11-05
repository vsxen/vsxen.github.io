---
title: 网站备份脚本
date: 2016-10-11 20:33:54
categories:
tags:
---
网站要记得备份，不然哪一天被攻击了就会心碎的。
下面是我用的备份脚本。本文以gdrive为例子，当然也可以使用别的云盘。
## 配置gdrive
作者地址https://github.com/prasmussen/gdrive
### 下载
用可以用秋水大神的服务器，一键下载二进制文件。
```
wget -O /usr/bin/gdrive http://dl.teddysun.com/files/gdrive-linux-x64
chmod +x /usr/bin/gdrive
```
### 授权
输入`gdrive about`，会输出一个网址，复制到浏览器打开，用Google账号授权，然后复制授权码，粘贴到终端就可以了。
常用的命令可以去作者的主页去看
## 使用
新建一个文件，比如back.sh
然后`chmod  a+x bash.sh`，让它有执行的权限，把下面的命令复制过去。
```
#!/bin/sh
mkdir ~/back  
mysqldump -u root -ppassword blog>~/back/wp.sql
#自己配置相应的信息 
cp -r /home/wwwroot/www.goog.ml back

tar zcf "backup-$(date '+%Y-%m-%d').tar.gz" back
gdrive upload --file backup-$(date '+%Y-%m-%d').tar.gz
rm backup-$(date '+%Y-%m-%d').tar.gz
rm -rf back
```
##  cron定时执行
在/etc/crontab最后面加一行，想下面那样，
也可以`echo  '30  1  *  *  * root bash /root/backup.sh' >> /etc/crontab`
```
# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
 30  1  *  *  * root bash /root/backup.sh
```
表示，每天凌晨 1 点 30 分，root 用户执行一次 backup.sh 脚本。



