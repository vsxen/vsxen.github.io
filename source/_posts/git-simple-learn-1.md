---
title: git简易教程-上
date: 2015-08-26 18:32:30
categories: 
tags: git
---

git是一个分散式版本控制软件,本地有完整的一份，服务器也有一份，自认为比SVN好一些。
##  安装 
>mac自带git
Windows可以自己去下载安装包
debian系 `sudo apt-get install git`
redhat系 `sudo yum install git`

## git连接仓库
我们要区分清楚git与github，git是一个版本控制的工具，而github有点类似于远程仓库，用于存放用git管理的各种项目。
连接之前需要配置一下
```
git config --global user.name "xxx"#配置用户名
git config --global user.email "test@example.com" #配置邮箱
```
github有两种连接仓库的方式
>ssh (无密码)
比如 git@github.com:vnexus/vnexus.github.io.git

ssh连接之前需要先生成公钥和密钥，并添加到github
打开命令行 运行
```
ssh-keygen -t rsa -b 4096 -C "youremail"#生成公钥 不带参数也可以
cat ~/.ssh/id_rsa#复制结果
#打开github，点击头像->setting ->侧边栏选择”SSH Keys" 接着粘贴key，点击”Add key”按钮，如果没有出错就添加成功了。
ssh -T git@github.com#测试连接
The authenticity of host 'github.com...(yes/no)?#输入yes
Hi 你的用户名...access#这就是添加成功了
```

>https (有密码)
比如https://github.com/vsxen/vsxen.github.io.git
（注意与ssh的区别）

如果你是用hexo搭建博客。那么上面的看懂就已经够了，也可以继续看下去，掌握git使用，对于程序员来说，非常有必要。


>先插一个`git status`命令，用于显示当前目测的git状态

##  初始化
```
git init 
#Initialized empty Git repository in path/test/.git/
git status
#On branch master#在主分支，分之在后面讲
#Initial commit
#nothing to commit (create/copy files and use "git add" to track)#
```
如果我想要开发一个test的项目，就需要先在文件夹内运行`git init `，这时候文件夹就会产生一个.git的隐藏文件夹，表示本文件夹是一个git本地仓库，当然，你也可以删除.git文件夹，那么test就不是gi本地仓库了。
## 添加文件
```
git add 
```
`git add .`表示把目录下的所有文件,都添加到主分支上面，以后，如果有新文件，都要先执行 `git add 新文件`命令。
比如
```
➜   git add test 
➜   git status
#On branch master
#Initial commit
#Changes to be committed:
#  (use "git rm --cached <file>..." to unstage)
#	new file:   test#这里显示有一个新文件
```

##  本地提交
```
git commit -m "提交说明"#这个说明可以在以后查看的时候看到
#[master (root-commit) 7a63306] test #7a63306提交id 以后会提到
# 1 file changed, 0 insertions(+), 0 deletions(-)
# create mode 100644 test
```
## 远程提交
自己在github建立一个空项目
```
git remote add origin 你的远程地址 #ssh 不要密码 https需要 ，origin 可以自己取名
git remote -v#查看添加的远程信息
git push -u origin master#提交到远程仓库
git feach origin #取回远程分支的文件
git pull origin master#取回远程分支的文件
```

更详细的请看[gitosc](http://git.oschina.net/progit/index.html)
