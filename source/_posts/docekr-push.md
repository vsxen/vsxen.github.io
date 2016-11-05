---
title: 自己亲手制作docker ssh镜像之手动push
date: 2016-09-26 13:04:43
categories: 
tags:  docker
---
docker作为一个新兴的技术已经越来越流行了，下面我们就来从零开始自己制作docker镜像，并且发布到dcoker hub。（类似于github）
## 注册账号
首先需要在https://hub.docker.com注册一个账号，过程就不多说了。
本文说的是手动push，这种方法不适用网速比较差的，因为push的速度太差，我都是选择自动构建的。

##  pull镜像
比如centos
```
docker pull centos(默认是latest)`
docker images
REPOSITORY   TAG     IMAGE ID            CREATED（省略）           
ubuntu              latest               c2c361df7160         
centos               latest              980e0e4c79ec               
```

##  本地运行 
```
docker -it  --name=centos-ssh（起一个名字） centos(pull的镜像名称) /bin/bash
#（启动之后运行 的命令）`之后，命令行就会变成root@****，这就是成功的进入了centos，
yum -y update
yum -y install openssh-server#（安装sshd服务）
ssh-keygen -t rsa#生成密钥（密码登录的话 可省略 ）
echo "root:123456"|chpasswd#设置登录密码
/usr/sbin/sshd -D#启动sshd服务
#输入exit退出，
docker ps 
#没有输出，因为没有正在运行的容器
dcoker ps - a
CONTAINER ID   IMAGE    COMMAND     CREATED      STATUS            
33dc80ac3fd3  centos-ssh   "/bin/sh -c 'yum -y u"   3 days ago       

```
##  建立仓库
在hub上面建立仓库，如果选择第一个就是自己本地构建并push上去，第二就是细看Dockerfile自动构建，这里我们先选择第一个。
## 测试镜像
```
docker ps -a，
CONTAINER ID   IMAGE    COMMAND     CREATED      STATUS        
33dc80ac3fd3  centos   "/bin/sh -c 'yum -y u"   3 days ago      
#用CONTAINER ID了给容器打上标签，
docker run -p 10022:22 -d sshd-centos /usr/sbin/sshd -D#端口不指定也可以需要用docker ps来查看
在本机运行 ssh root@docker ip -p 10022 #然后输入yes，再输入密码，不出错的话就可以连上了
docker tag 33dc80ac3fd3 test/test
docker push test/test#开始push
```
参考http://chinawu.blog.51cto.com/10692884/1826004
http://www.myfreax.com/build-image-with-dockerfile-hub/