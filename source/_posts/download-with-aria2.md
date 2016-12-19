---
title: 利用aria2打造离线下载（顺便破某网盘）
date: 2016-11-08 13:22:22
categories:
tags: 小技巧
---
需要用到的工具软件插件都在云盘的这个文件夹中，建议全部下载，传送门：http://pan.baidu.com/s/1nu4UHfV
##  懒人版 
### Mac
1. 安装Aria2GUI.dmg，位于网盘的Aria2 for Mac文件夹中
2. 下载自己的文件，复制下载地址到Aria2 GUI就可以了,如果你想百度云的，先登录，找到下载链接，
类似于`https://qdcache00.baidupcs.com/file`这样的，然后添加链接，max-connection-per-server建议设置为10左右，我的下载速度在1m/s左右
默认下载位置在Downloads

### Windows
1. 首先下载懒人包，详见网盘Aria2 for Windows
其中aria2.rar这个文件一定要解压在D:\aria2这个文件夹里，即D:\aria2\里面不能再有文件夹了
然后在D盘根目录建立一个Downloads的文件夹，这个文件夹就是你下载的文件存放的地方，不要把文件的名字搞错了
2. 进入D:\aria2\里面，双击HideRun.vbs这个文件，电脑不会有任何反应，因为运行窗口被屏蔽掉了，这是你进入任务管理器可以看到aria2c.exe这个进程正在运行。如果想开机自行启动，请看折腾版
然后找到 aria2控制界面.rar，将这个文件在任意位置解压缩，然后双击index.html这个文件，你的默认浏览器就会打开，这个网页就是控制aria2这个软件的界面，这是中文界面。然后把他加入浏览器的收藏夹即可,其他的就和Mac 一样了。



##  折腾版
下载安装最新版的Aria2（目前是1.21.0）,不同的系统自己选择下载
项目地址
https://github.com/tatsuhiro-t/aria2
https://github.com/tatsuhiro-t/aria2/releases/tag/release-1.21.0
安装目录是/usr/local/aria2（安装完就会出现在这里，隐藏的）
windows自己解压到任意目录就行
2）下载Aria2所需文件
找到网盘文件夹中的配置文件aria2.conf，运行Aria2所有的选项都可以在配置文件中设置
想具体了解配置文件可以参考以下网站：http://aria2c.com/usage.html 
或 https://aria2.github.io/manual/en/html/aria2c.html
附上我的配置文件
```
#rpc加密密钥
rpc-secret=token
#允许rpc
enable-rpc=true
#允许所有来源,web界面跨域权限需要
rpc-allow-origin-all=true
#允许外部访问，false的话只监听本地端口
rpc-listen-all=true
#RPC端口,仅当默认端口被占用时修改
#rpc-listen-port=6800
#最大同时下载数(任务数),路由建议值:3
max-concurrent-downloads=5
#断点续传
continue=true
#断开速度过慢的连接
lowest-speed-limit=0
#同服务器连接数
max-connection-per-server=5
#最小文件分片大小,下载线程数上限取决于能分出多少片,对于小文件重要
min-split-size=10M
#单文件最大线程数,路由建议值:5
split=10
#下载速度限制
max-overall-download-limit=0
#单文件下载速度限制
max-download-limit=0
#上传速度限制
max-overall-upload-limit=0
#单文件上传速度限制
max-upload-limit=0

#下载文件的保存路径,默认为当前启动位置
dir=/Users/qq/Downloads
#文件预分配,能有效降低文件碎片,提高磁盘性能.缺点是预分配时间较长
#所需时间none<falloc?trunc«prealloc,falloc和trunc需要文件系统和内核支持
file-allocation=prealloc
```
### Mac
打开终端Terminal，输入：
mkdir ~/.aria2
用户根目录（/Users/XXX， XXX是你的用户名）下会生成一个.aria2的文件夹(隐藏文件夹)，将配置文件aria2.conf 拖入这个文件夹中（这一步是为了方便每次启动aria2c的时候不用每次手动输入配置文件的位置）
接着找到压缩文件夹aria2c.zip，解压后将aria2c文件夹整个拖入 /Applications 目录下
运行Aria2
继续在Terminal输入：
mkdir ~/.aria2
如果第二步中的文件放置的位置没问题那么aria2c应该已经启动了
看aria2c 是否启动的办法是Terminal中输入：
ps aux|grep aria2c

出现图片中第三行的结果说明aria2c已经正常启动
### Windows
新建几个文件：
Aria2.log （日志，空文件就行）
aria2.session （下载历史，空文件就行）
aria2.conf （配置文件）
HideRun.vbs （隐藏cmd窗口运行用到的）
以上也可以借用懒人版的
配置文件
```
dir=D:\Downloads\
log=D:\Program Files\aria2\Aria2.log
input-file=D:\Program Files\aria2\aria2.session
save-session=D:\Program Files\aria2\aria2.session
save-session-interval=60
force-save=true
log-level=error
# see — split option
max-concurrent-downloads=5
continue=true
max-overall-download-limit=0
max-overall-upload-limit=50K
max-upload-limit=20
# Http/FTP options
connect-timeout=120
lowest-speed-limit=10K
max-connection-per-server=10
max-file-not-found=2
min-split-size=1M
split=5
check-certificate=false
http-no-cache=true
# FTP Specific Options
# BT/PT Setting
bt-enable-lpd=true
#bt-max-peers=55
follow-torrent=true
enable-dht6=false
bt-seed-unverified
rpc-save-upload-metadata=true
bt-hash-check-seed
bt-remove-unselected-file
bt-request-peer-speed-limit=100K
seed-ratio=0.0
# Metalink Specific Options
# RPC Options
enable-rpc=true
pause=false
rpc-allow-origin-all=true
rpc-listen-all=true
rpc-save-upload-metadata=true
rpc-secure=false
# Advanced Options
daemon=true
disable-ipv6=true
enable-mmap=true
file-allocation=falloc
max-download-result=120
#no-file-allocation-limit=32M
force-sequential=true
parameterized-uri=true
```
启动
用文本编辑工具打开刚才建立的HideRun.vbs
复制以下内容，注意修改D:\Progra~1\aria2\ 为你的aria2安装路径
CreateObject(“WScript.Shell”).Run “D:\Progra~1\aria2\aria2c.exe — conf-path=aria2.conf”,0
要启动aria2，一定要点击这个文件，不要点击aria2c.exe
如果要开机启动，创建一个HideRun.vbs的快捷方式，把快捷方式丢到 C:\Users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup中
这个目录的所有东西 都会开机启动
### GUI 控制
aria2是基于命令行的下载工具，不过还好大神们早已开发了各种易用的UI方便我们小白们使用
最常用的webui-aria2: http://ziahamza.github.io/webui-aria2/
也可以用binux大神的YAAW：http://binux.github.io/yaaw/demo/
其他就不需要多说了吧

速度参考
![](img/arai2.PNG)
参考
https://medium.com/@Justin___Smith/aria2%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B-mac%E5%92%8Cwindows-b31d0f64bd4e#.p7u9xoyrp