---
title: 运行Alsamixer或amixer提示no such file
date: 2016-12-18 09:15:24
categories:
tags: bananapi
---
香蕉派在使用音频接口播放音乐的时候提示no such file
解决方法
使用编辑器打开etc/asound.conf 


修改配置，和下面一样就可以了
```
pcm.!default {
type hw
card 0 
}

ctl.!default {
type hw
card 0 
}
```