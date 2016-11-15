---
title: ArchLinux硬盘安装全记录
date: 2016-11-08 13:17:39
categories: Linux
tags: 
---
ArchLinux是Linux的另一个发行版，它的安装过程可能会排除掉一大部分Linux新手，不过这正是熟练使用Linux的开始，
如果没有安装ArchLinux的话，你比较难知道Linux系统的运行情况。
ArchLinux的官方wiki 特别详细，有的也是中文，遇到问题可以及时查阅。

本文适宜于BIOS启动，UEFI未测试！！！
安装过程必须联网，手动检查`ping t.cn`
## 下载镜像
官方网站都有，像163,ustc都有，应该在800m左右
## 刻盘
windows用官方的推荐工具https://rufus.akeo.ie/
Linux用dd命令就行
## 优盘启动
从优盘启动系统，选择第一个X64启动项，之后就会显示root@arch了
## 分区
如果是双系统，在Windows分区最简便，直接格式化为EXT4和swap就行
或者你可以使用伪图形化界面cfdisk以及fdisk,我是用的cfdisk
如果你用的是cfdisk,请记住82和83这两个数字
整个硬盘就是sda，wWindows用的就是sda1，D盘就是sda2，我的sda3就是Archlinux的根目录
下面是我的分区表
/dev/sda3  60G /      物理分区   8300
/dev/sda4  8G  swap   物理分区   8200
## 文件系统
分区系统转化为ext4和swap，最后一条命令是开启交换分区。
```
mkfs.ext4 /dev/sda3
mkswap /dev/sda4
swapon /dev/sda4
```
## 挂载
`mount /dev/sda3 /mnt`
## 选择源
选择国内的比较快
```
nano /etc/pacman.d/mirrorlist
pacman -Syy
```
## 安装
`pacstrap -i /mnt base base-devel net-tools`
net-tools基本的网络命令像ifconfig
##  生成fstab
fstab中记录了挂载的相关信息，Archlinux中提供了工具来一键生成
`genfstab -U -p /mnt >> /mnt/etc/fstab`
这里使用的是UUID，如果不加-U，那么在fstab中记录的就是/dev/sdX之类的地址了，UUID的方式更加好，为什么呢？请自行wiki。

---------------分割线----------
## 系统设置
```
arch-chroot /mnt /bin/bash
alias ls='ls --color'#后一条命令是为了让ls显示颜色，方便查看。
```
##  设置Locale
`nano /etc/locale.gen`
这里你至少开启en_US.UTF-8和zh_CN.UTF-8。
```
locale-gen
echo LANG=zh_CN.UTF-8 >> locale.conf
```
这里由于console字体的原因，中文会变成方框，如果你不安装桌面环境，请使用en_US.UTF-8。
## 设置console
``
nano /etc/vconsole.conf
#输入如下内容
KEYMAP=us
FONT=
```

## 时区
`ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
这里大家可能会发现BIOS的时间和系统不一样了，我提供一个解决方案。
nano /etc/adjtime
输入如下内容：
0.000000 0 0.000000
0
LOCAL
参见https://wiki.archlinux.org/index.php/Time

## 主机名
虽说这里的主机名可以有大写，不过我建议大家使用常规的英文小写。
`echo 主机名 > /etc/hostname`
你还得修改/etc/hosts文件的内容。
nano /etc/hosts
你会看到如下内容：
127.0.0.1   localhost.localdomain localhost   主机名   
::1     localhost.localdomain localhost   主机名
这里面的主机名也需要修改
## 创建初始 ramdisk 环境

在您用 pacstrap 安装 linux 时就会自动运行 mkinitcpio，大部分用户都可以使用 mkinitcpio.conf 默认设置，如果有定制需求，请阅读re-generate the initramfs image。然后运行：

`mkinitcpio -p linux`
## 安装启动器
```
pacman -S grub os-prober
grub-install --target=i386-pc --recheck /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

##卸载分区并重启系统
现在新系统已经准备好第一次引导了，先退出 chroot 环境：
exit
然后，卸载分区并重启系统：
```
umount -R /mnt
reboot
```



## 安装桌面环境
这里以 GNOME 为例：
$ pacman -S gnome
要启用图形界面登录和锁屏等功能，可启用 gdm：
$ systemctl enable gdm.service
安装 GNOME 的一些常用工具（更多工具和扩展请参见这里）：
$ pacman -S gnome-tweak-tool gnome-packagekit gnome-settings-daemon-updates
安装中文输入法，GNOME 集成了 iBus，所以只需安装合适的输入法引擎，然后在 GNOME 系统设置中启用即可，参见这里：
$ pacman -S ibus-libpinyin
参考
https://hyjk2000.github.io/2014/01/23/arch-linux-install-guide/
https://coolrc.top/2015/12/04/04231804/
http://blog.lucode.net/linux/archlinux-install-tutorial.html