---
title: pip简单教程
date: 2016-03-27 20:00:01
categories:
tags: 小技巧
---

##  换源
编辑 ~/.pip/pip.conf 文件（如果没有则创建之），将 index-url 开头的一行修改为下面一行：

index-url = https://pypi.mirrors.ustc.edu.cn/simple
如果运行 pip 时, 提示如下错误

configparser.MissingSectionHeaderError: File contains no section headers.
请在 ~/.pip/pip.conf 最上方加上  这一 section header
也就是 
```
[global]
index-url = https://pypi.mirrors.ustc.edu.cn/simple
```
##  常用命令

```
pip freeze or pip list
导出requirements.txt
pip freeze > <目录>/requirements.txt
安装包
在线安装
pip install <包名> 或 pip install -r requirements.txt
通过使用== >= <= > <来指定版本，不写则安装最新版
requirements.txt内容格式为：
Django==1.5.4
MySQL-Connector-Python==2.0.1
MySQL-python==1.2.3
PIL==1.1.7
## 安装本地安装包
pip install <目录>/<文件名> 或 pip install --use-wheel --no-index --find-links=wheelhouse/ <包名>
<包名>前有空格
可简写为
pip install --no-index -f=<目录>/ <包名>
卸载包
pip uninstall <包名> 或 pip uninstall -r requirements.txt
升级包
pip install -U <包名>
升级pip
pip install -U pip
显示包所在的目录
pip show -f <包名>
搜索包
pip search <搜索关键字>
查询可升级的包
pip list -o
下载包而不安装
pip install <包名> -d <目录> 或 pip install -d <目录> -r requirements.txt
打包
pip wheel <包名>
```