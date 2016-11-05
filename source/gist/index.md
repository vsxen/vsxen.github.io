---
title: 整理一些短小强大的代码
date: 2016-09-27 19:23:11
---
```
#cmd运行，输入WiFi密码
for /f "skip=9 tokens=1,2 delims=:" %i in ('netsh wlan show profiles') do  @echo %j | findstr -i -v echo | netsh wlan show profiles %j key=clear
#查看Linux版本
cat /etc/redhat-release#或者
cat /etc/issue
#查看端口占用
netstat -anl | grep "80" ；#1080  8080也是会被筛选出来
lsof -i:80
#查看程序占用的端口
ps  -ef | grep nginx 
#安装docker
curl -s https://get.docker.com/ | sudo sh
```
