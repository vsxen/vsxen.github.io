---
title: 关于
date: 2015-06-20 19:52:57
---
喜欢Linux，热爱open sourse 。



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
ls -lR|grep "^-"|wc -l 
```



图片素材库 https://www.pexels.com/
同上 https://pixabay.com/  
测试网站性能 https://gtmetrix.com/  
前段开源库 https://www.awesomes.cn  
搜索引擎集合 http://so.chongbuluo.com/ 
awesome集合 https://www.libhunt.com/  
找同类软件 http://alternativeto.net/  
各平台的命令详解 http://ss64.com/  
枪版电影 http://s4yy.com/  
单页网站 https://onepagelove.com/  
同上 https://shapebootstrap.net/  
jekyll主题 http://jekyllthemes.org/  
从零开始做产品 http://www.devstore.cn/  
电视直播 http://www.66re.cn/tv/  
演示动画 http://thecodeplayer.com/  
YouTube电影院 https://andchill.tv/  
十分钟邮箱 http://mail.bccto.me/  