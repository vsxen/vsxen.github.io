---
title: Windows office2016只安装自己需要的组件
date: 2016-01-11 20:36:59
categories: 
tags: 小技巧
---
office2016  因为采用全新的安装方式，在安装的时候会吧word，excel，onenote等等全部的产品都安装上，反正我是只需要三件套就足够了所以就找到了以下方法
原文http://www.ithome.com/html/office/178814.htm
##  解压

先讲iso文件解压，得到一大堆的文件，找到configuration.xml
修改配置，看下面， `<ExcludeApp ID="Groove" />`意思就是说不要安装这和组件，大家可以根据自己的需要自行修改
##  安装

按住shift键，在空白处右击，或者自己打开cmd命令，然后在移动到，安装目录，也可以，之后运行下面的命令就可以了
```
setup.exe /configure configuration.xml
```
附上configuration.xml
```
<Configuration>
  <Add SourcePath="G:\office2016\" OfficeClientEdition="64" >
    <Product ID="ProPlusRetail">
      <Language ID="zh-CN" />
 <ExcludeApp ID="Groove" />
 <ExcludeApp ID="InfoPath" />
 <ExcludeApp ID="Lync" />
 <ExcludeApp ID="OneNote" />
 <ExcludeApp ID="Outlook" />
 <ExcludeApp ID="Publisher" />
 <ExcludeApp ID="SharePointDesigner" />
    </Product>
  </Add>  
</Configuration>
```
##  其他
其他相关的配置说明
SourcePath代表的是data的目录
OfficeClientEdition表示架构，如果你想安装32位则改为32；
 SourcePath表示Office2016 ISO镜像加载位置；
 Language表示语言，zh-CN表示中文，如果你安装的是英文，则为en-us；
##  修改路径
把office安装到其他盘，默认的安装位置是C盘，可以通过修改注册表来实现安装到其他盘
本人未测试，请先备份注册表

 方法：开始菜单----运行----Regedit-----打开注册表。找到：`HKEY_LOCAL_MACHINE\ SOFTWARE\Microsoft\Windows\CurrentVersion`，然后双击右侧的“ProgramFilesDir”字符串，出现C:\Program Files就是默认安装路径。
