---
title: htc s720e升级hboot到1.33
date: 2016-12-03 11:55:57
categories: Android
tags: 一些问题 
---
本文适宜于CID是htc_621的型号
HTC 提供的firmware 里面，用于Android 4.0 (ICS) 和Android 4.2 or 4.3 (JellyBean) 的HBOOT 是不相容的，因此若你想要使用ICS 的版本，你就必须使用旧一点的HBOOT，反之，若你要使用JellyBean，你就需要比较新的HBOOT，两者只能取其一。

下图是hboot模式
![](/img/htc2.png)
插上数据线，连接电脑，装驱动就不需要说了。

以下命令需要在cmd窗口中输入
## 重启到fastboot
`#按住音量下键和电源键，等10s左右就可以进入fastboot`
![fastboot](/img/htc1.jpg)
##　查看CID
`fastboot getvar cid`
如果不是htc_621的话，需要自己找对应的固件，就是firmware.zip
## 给设备上锁
`fastboot oem lock`
## 重启到RUU
`fastboot oem rebootRUU`
## 刷入固件
`fastboot flash zip firmware.zip`
## 回到fastboot
`fastboot reboot-bootloader`
## 官方解锁
这一步可以用一键解锁工具代替
http://www.shuame.com/bootloader-unlock.html
`fastboot flash unlocktoken Unlock_code.bin`
这时候 看hboot已经是1.33了
## 安装CWM Recovery 
`fastboot flash recovery recovery-clockwork-touch-5.8.4.0-endeavoru.img`
以上我自己亲测成功
参考
http://coldnew.github.io/blog/2013/12-29_76c4a/

一些工具
hboot 1.33 adb等
https://pan.baidu.com/share/link?shareid=112114&uk=3707991204
