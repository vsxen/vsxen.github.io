---
title: 成功在centos7上挂载google-drive
date: 2016-10-10 19:57:06
categories:  Linux 
tags:
---
简介：google-drive-ocamlfuse是一个可以在Linux系统上挂载Google-drive的工具，是搭建私有云，备份网站的神器。开源地址https://github.com/astrada/google-drive-ocamlfuse
## 安装依赖
```
yum install sqlite-devel fuse fuse-devel libcurl-devel zlib-devel m4
 yum install ocaml ocamldoc ocaml-camlp4-devel
 wget https://raw.github.com/ocaml/opam/master/shell/opam_installer.sh -O - | sh -s /usr/local/bin/
 yum install 
 opam install google-drive-ocamlfuse
 ```

## 初始化
此过程比较漫长，大约10分钟
```
opam init
opam install google-drive-ocamlfuse
opam list
export DISPLAY=:0.0
source ~/.bash_profile#加入环境变量
```
## 常用命令
```
google-drive-ocamlfuse --help
Usage: google-drive-ocamlfuse [options] [mountpoint]
  -version    show version and exit.
  -verbose    enable verbose logging on stdout. Default is false.
  -debug      enable debug mode (implies -verbose, -f). Default is false.
  -label      use a specific label to identify the filesystem. Default is "default".
  -id         provide OAuth2 client ID.
  -secret     provide OAuth2 client secret.
  -f          keep the process in foreground.
  -d          enable FUSE debug output (implies -f).
  -m          enable multi-threaded operation.
  -o          specify FUSE mount options.
  -cc         clear cache
  -headless   enable headless mode. Default is false.
  -skiptrash  enable permanent deletion mode. Default is false. Activate at your own risk. Files deleted with this option *cannot* be restored.
  -help       Display this list of options
  --help      Display this list of options
```

## 挂载
- mkdir -p /drive
- google-drive-ocamlfuse /drive

##  卸载
fusermount -u ~/google-driveLinux

参考 
https://github.com/kimduho/linux/wiki/CentOS-7-Google-Drive-mount
https://github.com/astrada/google-drive-ocamlfuse/wiki/Headless-Usage-%26-Authorization