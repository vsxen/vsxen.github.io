---
title: windows的包管理工具choco--安装使用指南 
date: 2016-11-15 13:53:33
categories:
tags: 软件推荐
---
在Linux世界中，安装一个软件不需要在浏览器中寻找软件的官网，然后将其下载下来，然后双击进行安装。只需要一条简单的命令，就可以完成搜索、安装、更新、卸载等所有操作。
其实Windows下,也有这么一个包管理器，功能虽然不及Linux中那些包管理器强大，但是也让Windows下的软件安装方便了不少。这就是Chocolatey。
## 安装
打开一个具有管理员权限的命令行窗口，执行如下命令：
`PowerShell @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin`

PowerShell
打开一个具有管理员权限的PowerShell窗口，执行如下命令： `PowerShell iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))`
或者` iwr https://cin.st | iex`
## 安装
以下是安装winrar的事例，需要使用代理
```
C:\>choco install winrar
Chocolatey v0.10.2
Installing the following packages:
winrar
By installing you accept licenses for the packages.

winrar v5.40 [Approved] - Likely broken for FOSS users (due to download location
 changes)
winrar package files install is complete. Performing other installation steps.
The package winrar wants to run 'chocolateyInstall.ps1'.
Note: If you don't run this script, the installation will fail.
Note: To confirm automatically next time, use '-y' or consider setting
 'allowGlobalConfirmation'. Run 'choco feature -h' for more details.
Do you want to run the script?([Y]es/[N]o/[P]rint): y

Using system proxy server '127.0.0.1:1080'.
Using system proxy server '127.0.0.1:1080'.
Downloading winrar 64 bit
  from 'http://www.rarlab.com/rar/winrar-x64-540.exe'
Using system proxy server '127.0.0.1:1080'.
Progress: 100% - Completed download of C:\Users\Administrator\AppData\Local\Temp
\chocolatey\winrar\5.40\winrar-x64-540.exe (2.08 MB).
Download of winrar-x64-540.exe (2.08 MB) completed.
WARNING: Missing package checksums are not allowed (by default for HTTP/FTP,
 HTTPS when feature 'allowEmptyChecksumsSecure' is disabled) for
 safety and security reasons. Although we strongly advise against it,
 if you need this functionality, please set the feature
 'allowEmptyChecksums' ('choco feature enable -n
 allowEmptyChecksums')
 or pass in the option '--allow-empty-checksums'. You can also pass
 checksums at runtime (recommended). See choco install -? for details.
The integrity of the file 'winrar-x64-540.exe' from 'http://www.rarlab.com/rar/w
inrar-x64-540.exe' has not been verified by a checksum in the package scripts.
Do you wish to allow the install to continue (not recommended)?
[Y] Yes [N] No (default is "N")
y
Installing winrar...
winrar has been installed.
 The install of winrar was successful.
  Software installed as 'exe', install location is likely default.

Chocolatey installed 1/1 packages. 0 packages failed.
 See the log for details (C:\ProgramData\chocolatey\logs\chocolatey.log).
```

除了在命令行中搜索软件包，还可以直接在Chocolatey网站上搜索软件包，网址是https://chocolatey.org/packages/ 。细心的同学会发现在网站上有一些同名的软件包，不同之处在于一个后面有Install，另一个则没有。这两者的区别是：有Install的软件包在安装之后，会在控制面板的添加和删除程序中找到。
 ## 错误
无法加载文件 ******.ps1，因为在此系统中禁止执行脚本。有关详细信息，请参阅 "get-help about_signing"。 
默认情况下是严格模式，允许执行命令但是禁止执行脚本。输入以下命令将执行策略设置为允许签名的远程脚本就行了。
管理员cmd运行
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`