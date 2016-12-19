---
title: 一些简短而又强大的命令
date: 2016-12-02 13:25:03
categories: 
tags: 小技巧
---

听说大多数的人都是键盘流，所以掌握一些命令是有必要的
## windows查看WiFi密码
cmd 运行
for /f "skip=9 tokens=1,2 delims=:" %i in ('netsh wlan show profiles') do  @echo %j | findstr -i -v echo | netsh wlan show profiles %j key=clear
## 查看Linux版本
cat /etc/redhat-release#或者
cat /etc/issue
## linux查看端口占用
netstat -anl | grep "80" ；#1080  8080也是会被筛选出来
lsof -i:80
## linux查看程序占用的端口
ps  -ef | grep nginx 
## linux安装docker
curl -s https://get.docker.com/ | sudo sh
## linux查看目录中有多少文件
ls -lR|grep "^-"|wc -l 
## Python启动http服务器（传文件）
python -m SimpleHTTPServer
## linux显示命令执行的具体时间精确到秒
export HISTTIMEFORMAT='%F %T '
history | more 
## linux  DD 显示进度
先放入后台，然后每5秒显示一下进度
sudo dd if= xxx.img of=/dev/mmcblk1 bs=10MB &
while (ps auxww |grep " dd " |grep -v grep |awk '{print $2}' |while read pid; do kill -USR1 $pid; done) ; do sleep 5; done

## 命令行测速 （python+speedtest）

sudo apt-get install python-pip
sudo pip install speedtest-cli
另一种 
wget https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py



##　mplayer  后台播放
mplayer * < /dev/null > /dev/null 2>1&


## block一些恶意ip
wget https://teddysun.com/wp-content/uploads/2013/05/block.sh
chmod +x block.sh
./block.sh