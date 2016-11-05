---
title: sublime安装以及使用
date: 2015-10-27 18:33:30
categories: 
tags: 软件推荐
---

简介：sublime是一个跨平台的简洁的文本编辑器，功能强大，有控制面板，代码自动补齐，可以安装很扩展包，确实是一个利器。
## 安装
官网上面都有对应的版本，自己下载下来安装可以了
##  快捷键
>通用

↑↓←→：上下左右移动光标，注意不是不是 KJHL ！
Alt：调出菜单
Ctrl + Shift + P：调出命令板（Command Palette）
Ctrl + ` ：调出控制台
>编辑

Ctrl + Enter：在当前行下面新增一行然后跳至该行
Ctrl + Shift + Enter：在当前行上面增加一行并跳至该行
Ctrl + ←/→：进行逐词移动
Ctrl + Shift + ←/→进行逐词选择
Ctrl + ↑/↓移动当前显示区域
Ctrl + Shift + ↑/↓移动当前行
>选择

Ctrl + D：选择当前光标所在的词并高亮该词所有出现的位置，再次 Ctrl + D 选择该词出现的下一个位置，在多重选词的过程中，使用 Ctrl + K 进行跳过，使用 Ctrl + U 进行回退，使用 Esc 退出多重编辑
Ctrl + Shift + L：将当前选中区域打散
Ctrl + J：把当前选中区域合并为一行
Ctrl + M：在起始括号和结尾括号间切换
Ctrl + Shift + M：快速选择括号间的内容
Ctrl + Shift + J：快速选择同缩进的内容
Ctrl + Shift + Space：快速选择当前作用域（Scope）的内容
>查找&替换

F3：跳至当前关键字下一个位置
Shift + F3：跳到当前关键字上一个位置
Alt + F3：选中当前关键字出现的所有位置
Ctrl + F/H：进行标准查找/替换，之后：
Alt + C：切换大小写敏感（Case-sensitive）模式
Alt + W：切换整字匹配（Whole matching）模式
Alt + R：切换正则匹配（Regex matching）模式
Ctrl + Shift + H：替换当前关键字
Ctrl + Alt + Enter：替换所有关键字匹配
Ctrl + Shift + F：多文件搜索&替换
>跳转

Ctrl + P：跳转到指定文件，输入文件名后可以：
@ 符号跳转：输入 @symbol 跳转到 symbol 符号所在的位置
#关键字跳转：输入 #keyword 跳转到 keyword 所在的位置
: 行号跳转：输入 :12 跳转到文件的第12行。
Ctrl + R：跳转到指定符号
Ctrl + G：跳转到指定行号
>窗口

Ctrl + Shift + N：创建一个新窗口
Ctrl + N：在当前窗口创建一个新标签
Ctrl + W：关闭当前标签，当窗口内没有标签时会关闭该窗口
Ctrl + Shift + T：恢复刚刚关闭的标签
>屏幕

F11：切换普通全屏
Shift + F11：切换无干扰全屏
Alt + Shift + 2：进行左右分屏
Alt + Shift + 8：进行上下分屏
Alt + Shift + 5：进行上下左右分屏
分屏之后，使用 Ctrl + 数字键 跳转到指定屏，使用 Ctrl + Shift + 数字键 将当前屏移动到指定屏
##  安装插件
首先要安装packagecontrol，按下Ctrl+`，然后打开
https://packagecontrol.io/installation#st2 (2.x)
或者https://packagecontrol.io/installation#st3 (3.x)

### emmet
打开preferences -> package control  输入 ip(install package) ,接着输入emmet,如果弹出弹出一个package Control information就可以了.
所有语法http://docs.emmet.io/abbreviations/syntax/
### IMESupport
输入法跟随（好像win下才需要装）
### js format
### html beauti
格式化 html、css、js，需要安装node，Windows需要配置node的安装目录。
### SublimeTmpl 
快速生成文件模板,SublimeTmpl 能新建 html、css、javascript、php、python、ruby 六种类型的文件模板，所有的文件模板都在插件目录的templates文件夹里，可以自定义编辑文件模板。
SublimeTmpl默认的快捷键
ctrl+alt+h → html
ctrl+alt+j → javascript
ctrl+alt+c → css
ctrl+alt+p → php
ctrl+alt+r → ruby
ctrl+alt+shift+p → python
## 主题
### Spacegray Dark
![Spacegray Dark](https://packagecontrol.io/readmes/img/ca28f488fbf053507cecba3aa8f8636d8195ba58.png)
### material theme
如下图
![material theme](https://packagecontrol.io/readmes/img/4db1efeb44fd6fb00332a28f3228db7eefc0769e.gif)
## 快速打开

### mac
`sudo ln -s "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl" /usr/bin/subl`
### Windows
使用 Win + R 运行 sysdm.cpl 打开 “系统属性”，然后配置环境变量，增加一个到sublime的安装目录就行了。
### Linux
安装之后就可以直接用，subl  文件或者subl 文件夹

## 用户设置
可以设置自己的缩进规则，快捷键，换行等，打开Preferences -> Settings - User,而且出现问题可以直接删除配置文件，比较方便。
```
// 设置tab的大小为2
"tab_size": 2,
// 添加行宽标尺
"rulers": [80, 100],
// 显示空白字符
"draw_white_space": "all",
// 保存时自动去除行末空白
"trim_trailing_white_space_on_save": true,
// 保存时自动增加文件末尾换行
"ensure_newline_at_eof_on_save": true,
按f2打开chrome（需要sider bar）
{ "keys": ["f2"], "command": "side_bar_files_open_with",
        "args": {
            "paths": [],
            "application": "C:/Program Files (x86)/Google/Chrome/Application/chrome.exe",
            "extensions":".*"
                 }
},
"word_wrap": true 80字换行：
 "draw_minimap_border" : true, 右侧缩略图边框
    "font_face"           : "YaHei Consolas Hybrid",字体设置
    "font_size"           : 13,   字体大小
    "highlight_line"      : true, 当前行标亮
    "ignored_packages"    : ["Toggle Css Format"],开启vim模式
    "save_on_focus_lost"  : true,  失去焦点后保存
    "auto_complete"       : false, 失去焦点后保存
    "word_separators"     : "./\\()\"':,.;<>~!@#$%^&*|+=[]P{}`~?", 双击选中中划线
    "update_check"        : false  关闭自动更新
    "http_proxy": "http://127.0.0.1:8123",  代理，需要开启polipo
```

参考
http://zh.lucida.me/blog/sublime-text-complete-guide/
https://github.com/jikeytang/sublime-text
http://www.jeffjade.com/2015/12/15/2015-04-17-toss-sublime-text/