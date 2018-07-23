---
title: WebStorm配置Git
date: 2017-04-03 16:26:26
tags:
---

点击WebStorm的设置按钮

进入设置面板后，直接在左上角搜索github（这个也算是WebStorm方便功能之一，很快速定位设置项），然后填入你github的账户名和密码，然后按一下Test看看是否连接成功

成功连接后，你就已经登录到Github账户了，但这还不够，你还得让WebStorm能够支持到Git操作，那么我们首先先去[https://code.google.com/p/msysgit/downloads/list](https://code.google.com/p/msysgit/downloads/list)下载Git，安装后，在WebStorm中查找Git，选好git.exe的路径，配置，然后按一下Test看看是否连接成功

<!-- more -->

打开gitbash.exe。

现在我们来为本地 git 配置全局的 user 与 email 参数

Ps:这里的hello和xxx@123.com要换成你自己的

在Git Bash 里输入

`git config --global user.name "hello"`

然后按回车键，再输入

`git config --global user.email "xxx@123.com"`

再按回车，现在要在本地生成 SSH 秘钥，这时你要输入

`ssh-keygen -t rsa -C "xxx@123.com"`

然后一路回车即可。

安装完之后，打开`C:\Users\Administrator\.ssh`

会发现其目录底下生成了两个文件，

其中 `id_rsa` 是私钥，`id_rsa.pub` 是公钥。

用记事本打开公钥 `id_rsa.pub`，复制里面的全部内容，提交给github。

如何提交给github呢？

进入你的github，点击你的头像，选 setting，

再选 SSH and GPG keys，点击 New SSH key。

Title那里你可以随便填，比如myProject。

而Key里面要填的就是你刚才复制的东西，直接黏贴进去即可。

最后按下Add SSH key，搞定！

将项目导入Webstorm中 
VCS -> import into version control -> create git repository

创建一个名为 .gitignore 的文件，里面的内容为
```
built/
node_modules/
.idea/
npm-debug.log
```

在项目根目录处 右键 点击git bash here

`git init`

`git add .`

`git commit -m "commitname"`

`git remote add origin https://github.com/xxxx/xxx.git`

`git push -u origin master`
