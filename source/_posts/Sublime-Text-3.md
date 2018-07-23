---
title: Sublime Text 3
date: 2016-12-10 09:54:55
tags: 工具
---

## 下载Sublime Text 3
[SublimeText3官网下载](http://www.sublimetext.com/3)

## 安装 Package Control
(1) 按 *Ctrl+`* 调出 console

(2) 粘贴以下代码到底部命令行并回车
```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

(3) 重启Sublime Text 3

(4) 如果在 *perferences* -> *package settings* 中看到 *package control* 这一项，则表示安装成功

## 使用 Package Control 安装插件
(1) 按下 *Ctrl+Shift+P* 调出命令面板

(2) 输入 `install` 调出 Install Package 选项并回车，然后在列表中选中要安装的插件

<!-- more -->

## 常用插件
(1) **Emmet**: 一种快速编写HTML/CSS代码的方法 
**快捷键（以下按键均需加上Tab键）**

 *!* 生成 HTML5 结构

 *#aaa* 生成id为aaa的div

 *.bbb* 生成class为bbb的div

 *span.bbb* 生成class为bbb的span

 *ul#ccc.ddd* 生成id为ccc的class为ddd的ul

 *div>ul>li* 后代 >

 *div+p+bq* 兄弟 +

 *div>ul>li^span* 上级 ^

 *ul>li*3* 重复多个 *

 *div>(header>ul>li*2>a)+footer>p* 分组 ( )

 *a[href="http://www.aaa.com/" title="aaa 博客"]* 生成href 为 “http://www.aaa.com/ ，title 为“aaa 博客”的 a 标签

 *[attr]* 自定义属性

(2) **SideBarEnhancements**: 侧边栏增强

(3) **jQuery**: jQuery代码补全

(4) **MarkDownEditing**: markdown语法高亮 

(5) **OmniMarkupPreviewer**: 在浏览器预览markdown文档 
**快捷键：Ctrl+Alt+O **

## 设置浏览器预览快捷键
打开 " *Preference* -> *Package Settings* -> *Side Bar* -> *key Bindings-User*"，

在打开的文件中添加如下内容：

```
[ { 
    "keys": ["f12"], "command": "side_bar_files_open_with", 
    "args": { 
        "paths": [], 
        "application": "C:/Users/Administrator/AppData/Local/Google/Chrome/Application/chrome.exe", 
        "extensions":".*"
        } 
} ]
```

(其中，快捷键和路径需根据实际情况更改)

## 配置浏览器预览路径localhost
(1) 安装 SideBarEnhancements 侧边栏增强插件

(2) 打开 " *Preference* -> *Package Settings* -> *Side Bar* -> *Settings User-User*"

(3) 在打开的文件中添加：

`{ "default_browser": "chrome" //one of this list: firefox, aurora, chrome, canary, chromium, opera, safari }`

(4) 为 SideBarEnhancements 指定默认localhsot目录在侧边栏任意文档上点击鼠标右键，

选择 " *Project* -> *Edit Preview URLs*"

(5) 在打开的文件中添加如下内容：

```{ 
    "E:/WEBSITE/HelloWorld/":{ 
        "url_testing": "http://localhost:8008/", 
        "url_production": "http://equipmentmgr.sinaapp.com/"
         }
    }
```

> " *E:/WEBSITE/HelloWorld/* " 是项目在磁盘中的路径，请修改为你的项目地址 

> " *url_testing* " 是你本地的 localhost 地址 

> " *url_production* " 是项目线上地址

(6) 为浏览器绑定热键

打开 " *Preference* -> *Package Settings* -> *Side Bar* -> *key Bindings-User* "，

在打开的文件中添加如下内容：

```
[ { 
    "keys": ["f12"], 
    "command": "side_bar_open_in_browser", 
    "args": { 
        "paths": [], 
        "type": "testing", 
        "browser": "" 
        } 
} ]
```

## 快捷键

### 选择类

*Ctrl+D* 选中光标所占的文本，继续操作则会选中下一个相同的文本

*Alt+F3* 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑举个栗子：快速选中并更改所有相同的变量名、函数名等

*Ctrl+L* 选中整行，继续操作则继续选择下一行，效果和 Shift+↓ 效果一样

*Ctrl+Shift+L* 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行

*Ctrl+Shift+M* 选择括号内的内容（继续选择父括号）举个栗子：快速选中删除函数中的代码，重写函数体代码或重写括号内里的内容

*Ctrl+M* 光标移动至括号内结束或开始的位置

*Ctrl+Enter* 在下一行插入新行举个栗子：即使光标不在行尾，也能快速向下插入一行

*Ctrl+Shift+Enter* 在上一行插入新行举个栗子：即使光标不在行首，也能快速向上插入一行

*Ctrl+Shift+[* 选中代码，按下快捷键，折叠代码

*Ctrl+Shift+]* 选中代码，按下快捷键，展开代码

*Ctrl+K+0* 展开所有折叠代码

*Ctrl+←* 向左单位性地移动光标，快速移动光标

*Ctrl+→* 向右单位性地移动光标，快速移动光标

*Shift+↑* 向上选中多行

*Shift+↓* 向下选中多行

*Shift+←* 向左选中文本

*Shift+→* 向右选中文本

*Ctrl+Shift+←* 向左单位性地选中文本

*Ctrl+Shift+→* 向右单位性地选中文本

*Ctrl+Shift+↑* 将光标所在行和上一行代码互换（将光标所在行插入到上一行之前）

*Ctrl+Shift+↓* 将光标所在行和下一行代码互换（将光标所在行插入到下一行之后）

*Ctrl+Alt+↑* 向上添加多行光标，可同时编辑多行

*Ctrl+Alt+↓* 向下添加多行光标，可同时编辑多行

### 编辑类

*Ctrl+J* 合并选中的多行代码为一行举个栗子：将多行格式的CSS属性合并为一行

*Ctrl+Shift+D* 复制光标所在整行，插入到下一行

*Tab* 向右缩进

*Shift+Tab* 向左缩进

*Ctrl+K+K* 从光标处开始删除代码至行尾

*Ctrl+Shift+K* 删除整行

*Ctrl+/* 注释单行

*Ctrl+Shift+/* 注释多行

*Ctrl+K+U* 转换大写

*Ctrl+K+L* 转换小写

*Ctrl+Z* 撤销

*Ctrl+Y* 恢复撤销

*Ctrl+U* 软撤销，感觉和 Gtrl+Z 一样

*Ctrl+F2* 设置书签

*Ctrl+T* 左右字母互换

*F6* 单词检测拼写

### 搜索类

*Ctrl+F* 打开底部搜索框，查找关键字

*Ctrl+shift+F* 在文件夹内查找，与普通编辑器不同的地方是sublime允许添加多个文件夹进行查找，略高端，未研究

*Ctrl+P* 打开搜索框举个例子：1、输入当前项目中的文件名，快速搜索文件，2、输入@和关键字，查找文件中函数名，3、输入：和数字，跳转到文件中该行代码，4、输入#和关键字，查找变量名

*Ctrl+G* 打开搜索框，自动带：，输入数字跳转到该行代码举个栗子：在页面代码比较长的文件中快速定位

*Ctrl+R* 打开搜索框，自动带@，输入关键字，查找文件中的函数名举个栗子：在函数较多的页面快速查找某个函数

*Ctrl+:* 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等

*Ctrl+Shift+P* 打开命令框场景例子：打开命名框，输入关键字，调用sublime text或插件的功能，例如使用package安装插件

*Esc* 退出光标多行选择，退出搜索框，命令框等

### 显示类

*Ctrl+Tab* 按文件浏览过的顺序，切换当前窗口的标签页

*Ctrl+PageDown* 向左切换当前窗口的标签页

*Ctrl+PageUp* 向右切换当前窗口的标签页

*Alt+Shift+1* 窗口分屏，恢复默认1屏（非小键盘的数字）

*Alt+Shift+2* 左右分屏-2列

*Alt+Shift+3* 左右分屏-3列

*Alt+Shift+4* 左右分屏-4列

*Alt+Shift+5* 等分4屏

*Alt+Shift+8* 垂直分屏-2屏

*Alt+Shift+9* 垂直分屏-3屏

*Ctrl+K+B* 开启/关闭侧边栏

*F11* 全屏模式

*Shift+F11* 免打扰模式

### 补充

*Ctrl+O* 可以实现头文件和源文件之间的快速切换

通过 *View -> Side bar* 可在左侧显示当前打开的文件列表

Sublime text 删除插件步骤：*Ctrl+Shift+P* -> *Remove Package* ->找到需要删除的插件，并点击即可删除; 

## 定制主题

[SublimeText定制主题](http://tmtheme-editor.herokuapp.com/#!/editor/theme/Monokai)

可以轻松按照自己的意愿制作喜欢的主题完毕之后将生成的xx.sublime.theme文件，

点开 *Preferences* -> *Browsr Packages*，

放在这个直属目录之下，即可在Theme处选择这个主题了!
