---
title: windows的包管理工具choco安装使用指南 
date: 2016-11-15 13:53:33
categories:
tags:
---


```
打开一个具有管理员权限的命令行窗口，执行如下命令： PowerShell @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin

PowerShell
打开一个具有管理员权限的PowerShell窗口，执行如下命令： PowerShell iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))

无法加载文件 ******.ps1，因为在此系统中禁止执行脚本。有关详细信息，请参阅 "get-help about_signing"。 
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