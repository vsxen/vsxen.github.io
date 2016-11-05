---
title: git简易教程-下
date: 2015-08-27 17:58:47
categories:
tags: git
---

上一篇讲了git安装、配置、初始化以及提交。
##  分支
git init之后默认是都是master分支，就是主分支。相当于稳定版。
git分支是用来开发新功能，或者修复bug，尝试新技术，最后可以合并到master分支
```
git branch iss50  #建立iss50分支
git branch -d iss50 #删除iss50分支
git chackout iss50 #更换分支
#Switched to branch 'gh-pages'
git checkout -b iss50  #-b 建立iss50分支后转入iss50分支 
git merge iss50 #讲iss50合并到master分支
```

## 回退
版本回退，如果发现master分支有地方太激进了，或者有严重bug，那么就需要回退到上一个版本。
```
git log #按q退出
#commit 7a6330640895848b00d99998d69b7410bf696275  #这是commit id
#Author: vnexus <vnexusk@gmail.com>
#Date:   Tue Sep 13 16:11:16 2016 +0800

#    test #这是commit的信息
git reset --hard 7a63306 #commitid 的前几位
```