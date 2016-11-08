---
title: 自己亲手制作docker ssh镜像之自动构建
date: 2016-09-26 13:29:13
categories: 
tags:  docker
---

用dockerfile自动构建，首先需要简单链接一下手动的步骤，因为dockerfile就只是把手动需要输入的命令集中起来了。
## 准备
你首先需要有一个docker hub账号和 github 账号。
## dcokerfile
以下是docker官方的实例文件，来自https://docs.docker.com/engine/examples/running_ssh_service/
```
FROM ubuntu:14.04#来自哪个镜像
MAINTAINER Sven Dowideit <SvenDowideit@docker.com>
#作者信息
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22#开放端口
CMD ["/usr/sbin/sshd", "-D"]#启动时候执行的命令
```


因为dockerfile构建可能会有错误，所以可以现在本地测试一下，然后在放到仓库上
```
docker run -d -P --name test_sshd eg_sshd
docker port test_sshd 22
0.0.0.0:49154
ssh root@192.168.1.2 -p 49154
# The password is screencast.
root@f38c87f2a42d:/#
```

## 建立仓库
先登录到docker hub ，并且用github账号为 docker hub授权，
![](/img/link-github.png)
查看授权的账号可以到https://hub.docker.com/account/authorized-services/
然后选择第二个自动构建，
![(/img/create-repo.png)
选择你的dockerfile所在的repo,修改一下名字和是否私有就可以创建了。
![](/img/create.png)
在dockerfile可以查看自己的dockerfile，
Build Settings可以指定dockerfile的位置
Bulid Detail可以查看所有的build信息
![](/img/info.png)
如果repo是共有，就可以pull下来，使用了。
参考http://chinawu.blog.51cto.com/10692884/1827787