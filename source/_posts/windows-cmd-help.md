---
title: windows的一些命令
date: 2015-08-21 17:52:40
categories:
tags:  小技巧
---

此处列举了Windows命令行中常用的一些命令，如果不熟悉该命令的用法，可以在键入命令后 跟随 /?，如下所示：

arp 显示与修改地址解析协议（ARP）使用的IP地址到网卡物理地址之间的转换表
assoc 显示与修改扩展文件关联
attrib 显示与修改文件属性
bcdedit 显示与管理引导配置数据（BCD）库文件
call 以过程的形式调用脚本或脚本标记
chkdsk 检查磁盘的错误并显示报告
chkntfs 显示卷状态，在计算机启动时设置或排除一些系统自动检测过程中涉及到的卷
choice 创建一个选择列表，通过该列表，用户可以在批处理脚本中选择相应的选项
cipher 显示当前的加密状态，或在NTFS卷上修改文件夹与文件加密
cmdkey 创建，显示和删除保存的用户名和密码
color 设置默认的控制台前景和背景颜色
comp 比较两个文件或文件集的内容
compact 显示或改变NTFS分区上文件的压缩
convert 将FAT卷转换为NTFS
## cd 
和Linux一样，进入目录
## clip
把上文得到的输出复制到剪切板比如ipconfig|clip
## cls
清屏
## copy 
复制或合并文件
## date
显示或设置日期
defrag 对硬盘驱动器进行碎片整理
## del 
删除一个或多个文件
## dir
显示目录的所有文件和目录信息
diskcomp 比较两个软盘的内容
doskey 编辑命令行，重新调用命令，创建宏
driverquery 显示所有已安装设备驱动程序及其属性列表
## echo 
显示信息，或将命令回显打开或关上
edit MS-DOS编辑器
endlocal 在批处理文件中终止环境变量的局部化，所做的环境变量的改动不再仅限于批处理文件中
erase 同del，删除一个或多个文件
esentutl 管理可扩展存储引擎(ESE)数据库，包括活动目录域(ADDS)使用的
eventcreate 在事件日志中创建自定义事件
## exit 
退出命令解释器或当前批处理脚本
expand 取消文件的压缩
##  fc 
比较两个文件并显示差别
find 在文件中搜索文本字符串
findstr 使用正则表达式在文件中搜索字符串
for 对文件集中的每一文件运行指定命令
forfiles 选择一个或多个文件并对每一文件执行命令
format 对软盘或硬盘进行格式化
ftype 显示或修改用在文件扩展名关联中的文件类型
getmac 显示网络适配器信息
goto 跳转到批处理脚本中标号行
gpupdate 强制进行组策略的后台刷新
## hostname 
打印计算机名
icacls 显示或修改文件的访问控制表(ACL)
if 在批处理脚本程序中进行条件处理
## ipconfig 
显示TCP/IP配置
## label 
创建、改变或删除磁盘的卷标
## md 
创建目录或子目录（同mkdir）
## more 
输出一次显示在一个屏幕
mountvol 创建、删除或列出卷挂载点
## move 
将文件从一个目录移动到同一驱动器上的其他目录
nbtstat 显示协议统计和当前使用NBI的TCP/IP连接
net config server 显示或修改server服务的配置
net continue 恢复暂停的服务
net localgroup 显示、创建、修改或删除本地组帐号
net pause 挂起服务
net print 显示或管理打印任务与共享队列
net session 列出或断开回话
net share 显示或管理共享的打印机与目录
net start 列出或启动网络服务
net statistics 显示工作站与服务器统计信息
net stop 终止服务
net time 显示或同步网络时间
net use 显示或管理远程链接
net user 显示、创建、修改或删除本地用户帐号
net view 显示网络资源或计算机
netsh 调用一个单独的命令提示符，用于对本地计算机或远程计算机上的网络服务配置进行管理
## netstat 
显示网络连接状态
## nslookup 
显示DNS状态,查询dns记录
path 在当前窗口中，显示或设置可执行文件的搜索路径
pathping 对路由进行追踪并提供丢包信息
pause 挂起对脚本的处理，直至有键盘输入
ping 确定是否可以建立网络连接
popd 切换到由pushd保存的目录
print 打印文本文件
prompt 改变Windows命令提示符
pushd 保存当前目录，之后切换到新目录
rd 移除目录
reg add 向注册表添加一个子健或条目
reg copy 将某注册表条目复制到本地或远程系统上的特定健路径
reg delete 从注册表中删除一个子健或条目
reg query 列出某注册表健下的条目与子健名（如果有）
reg restore 将保存的子健与条目写会到注册表
reg save 将指定子健、条目、值的副本保存到某个文件中
regsvr32 注册或取消对DLL的注册
ren 对文件进行重命名
route 管理网络路由表
runas 以特定用户许可权限运行程序
## set 
显示或修改Windows环境变量，也可以用于在命令中评估数字表达式
setlocal 在批处理文件中开始变量的局部化
shift 移动脚本中可替换的位置
## shutdown 
关闭或重启计算机
## sort 
对输入进行排序
## start 
启动一个新的命令shell窗口，用来运行指定的程序或命令 `start https://vsxen.githu.io`可以打开我的网站
## systeminfo 
显示详尽的配置信息
## taskkill
根据进程名和进程ID终止运行中的进程
## tasklist 
根据进程名或进程ID列出所有运行中的进程
## time 
显示或设置系统时间
timeout 在批处理脚本中设置超时周期或者等待按键
## title 
为命令提示窗口设置标题
tracert 显示计算机之间的联通路径
## type
显示文本文件内容
## ver 
显示Windows版本
where 显示匹配搜索模式的文件列表
whoami 显示当前用户的登录与安全信息
```
---
原文http://realwall.cn/blog/