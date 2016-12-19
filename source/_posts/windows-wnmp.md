---
cdtitle: windows的配置lnmp
date: 2016-03-27 20:55:18
categories: 
tags:  小技巧 
---

## php配置
（nginx下php是以FastCGI的方式运行，所以我们下载非线程安全也就是nts的php包）
修改目录下面的php.ini-recommended文件为php.ini，并用Editplus或者Notepad++打开来。找到
extension_dir ="./ext"
更改为
extension_dir ="D:/wnmp/php5/ext"
往下看，再找到
;extension=php_mysql.dll ;extension=php_mysqli.dll
前面指定了php的ext路径后，只要把需要的扩展包前面所对应的“;”去掉，就可以了。这里打开php_mysql.dll和php_mysqli.dll，让php支持mysql。当然不要忘掉很重要的一步就是，把php5目录下的libmysql.dll文件复制到C:\Windows目录下，也可以在系统变量里面指定路径，当然这里我选择了更为方便的方法^_^。
到这里，php已经可以支持mysql了。
接下来我们来配置php，让php能够与nginx结合。找到
;cgi.fix_pathinfo=1
我们去掉这里的封号。
cgi.fix_pathinfo=1
这一步非常重要，这里是php的CGI的设置。
## nginx配置
把下载好的nginx-1.0.4的包同样解压到D盘的wnmp目录下，并重命名为nginx。接下来，我们来配置nginx，让它能够和php协同工作。进入nginx的conf目录，打开nginx的配置文件nginx.conf，找到
location / { root html;　　　　　　#这里是站点的根目录 index index.html index.htm; }
将root  html;改为root   D:/wnmp/www;
再往下，找到pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000 
先将前面的“#”去掉，同样将root  html;改为root   D:/wnmp/www;。再把标记为红色的/scripts改为“$document_root”，这里的“$document_root”就是指前面“root”所指的站点路径，

开启命令
```
D:/wnmp/php5/php-cgi.exe -b 127.0.0.1:9000 -c D:/wnmp/php5/php.ini echo Starting nginx... RunHiddenConsole D:/wnmp/nginx/nginx.exe -p D:/wnmp/nginx
```
结束命令
@echooffecho Stopping nginx...   taskkill /F /IM nginx.exe > nulecho Stopping PHP FastCGI... taskkill /F /IM php-cgi.exe > nul exit
