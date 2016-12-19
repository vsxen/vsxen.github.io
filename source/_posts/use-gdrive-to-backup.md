---
title: 网站备份脚本
date: 2016-10-11 20:33:54
categories: 
tags:  小技巧 
---
网站要记得备份，不然哪一天被攻击了就会心碎的。
下面是我用的备份脚本。本文以gdrive为例子，当然也可以使用别的云盘。
## 配置gdrive
作者地址https://github.com/prasmussen/gdrive
### 下载
用可以用秋水大神的服务器，一键下载二进制文件。
wget -O /usr/bin/gdrive http://dl.teddysun.com/files/gdrive-linux-x64
chmod +x /usr/bin/gdrive

### 授权
输入`gdrive about`，会输出一个网址，复制到浏览器打开，用Google账号授权，然后复制授权码，粘贴到终端就可以了。
常用的命令
```
gdrive [global] list [options]                                 List files
gdrive [global] download [options] fileId                    Download file or directory
gdrive [global] download query [options] query               Download all files and directories matching query
gdrive [global] upload [options] path                        Upload file or directory
gdrive [global] upload - [options] name                      Upload file from stdin
gdrive [global] update [options] fileId path               Update file, this creates a new revision of the file
gdrive [global] info [options] fileId                        Show file info
gdrive [global] mkdir [options] name                         Create directory
gdrive [global] share [options] fileId                       Share file or directory
gdrive [global] share list fileId                            List files permissions
gdrive [global] share revoke fileId permissionId           Revoke permission
gdrive [global] delete [options] fileId                      Delete file or directory
gdrive [global] sync list [options]                            List all syncable directories on drive
gdrive [global] sync content [options] fileId                List content of syncable directory
gdrive [global] sync download [options] fileId path        Sync drive directory to local directory
gdrive [global] sync upload [options] path fileId          Sync local directory to drive
gdrive [global] changes [options]                              List file changes
gdrive [global] revision list [options] fileId               List file revisions
gdrive [global] revision download [options] fileId revId   Download revision
gdrive [global] revision delete fileId revId               Delete file revision
gdrive [global] import [options] path                        Upload and convert file to a google document, see 'about import' for available conversions
gdrive [global] export [options] fileId                      Export a google document
gdrive [global] about [options]                                Google drive metadata, quota usage
gdrive [global] about import                                   Show supported import formats
gdrive [global] about export                                   Show supported export formats
gdrive version                                                 Print application version
gdrive help                                                    Print help
gdrive help command                                          Print command help
gdrive help command subcommand                             Print subcommand help
```
## 使用
新建一个文件，比如back.sh
然后`chmod  a+x bash.sh`，让它有执行的权限，把下面的命令复制过去。
```
#!/bin/sh
mkdir ~/back  
mysqldump -u root -ppassword blog~/back/wp.sql
#自己配置相应的信息 
cp -r /home/wwwroot/www.goog.ml back

tar zcf "backup-$(date '+%Y-%m-%d').tar.gz" back
gdrive upload --file backup-$(date '+%Y-%m-%d').tar.gz
rm backup-$(date '+%Y-%m-%d').tar.gz
rm -rf back
```
##  cron定时执行
在/etc/crontab最后面加一行，想下面那样，
也可以`echo  '30  1  *  *  * root bash /root/backup.sh'  /etc/crontab`
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



