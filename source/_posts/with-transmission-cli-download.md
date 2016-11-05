---
title: 使用transmission-cli下载文件
date: 2016-10-18 14:11:09
tags:
---
## 安装
sudo apt-get install transmission-cli 

如果你经常使用 transmission-cli ，那么值得花时间来熟悉一下它的命令行选项。

"-w /path/to/download-directory" 选项指定下载文件保存的文件夹。
"-f /path/to/finish-script" 选项设置当前下载完成后要运行的脚本。注意 transmission-cli 默认在文件下载完成后继续运行。如果你想在成功下载完成后自动关闭 transmission-cli，你可以使用这个选项。下面这个简单的脚本可以完成这个功能。
#!/bin/sh
sleep 10
killall transmission-cli
如果你想为 transmission-cli 分配上传/下载带宽限制，你可以使用 “-d <download-speed-in-KB/s>” 和 “-u <upload-speed-in-KB/s>” 选项。如果你不想限制带宽使用，仅仅指定 “D” 或 “-U” 选项即可。
这有一个更高级的 transmission-cli 使用范例。在这个例子中，命令行客户端在成功下载后自动退出。下载速度不限而上传速度限制为 50KB/s。

$ transmission-cli -w ~/iso -D -u 50 -f ~/finish.sh ubuntu-14.10-desktop-amd64.iso.torrent
