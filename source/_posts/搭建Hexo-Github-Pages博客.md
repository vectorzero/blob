---
title: 搭建Hexo+Github Pages博客
date: 2016-12-09 00:06:01
tags: 黑科技
---

### 注册 Github 账号
[Github官网](https://github.com/)

### 生成 Github Pages
假设，你注册github时的username为`hello`，

邮箱为`xxx@123.com`。

点击 New repository 即新建仓库，

Repository name 那里就得填写 `hello.github.io`，

然后点击Create repository。

再点击右边的Settings，把页面拉到下面，

你会看到一个Lauch automatic page generator 按钮，点击它。

进入另一个页面后，直接拉到下面，点击右下角的Continue to layouts按钮。

页面跳转后，随便选择一个主题，然后点击Publish Page按钮。

Github Pages完成了!

现在你可以在浏览器输入`https://hello.github.io`预览到Github Pages了。

<!-- more -->

### 安装 git
[下载git客户端](https://git-scm.com/downloads)

打开gitbash.exe。

现在我们来为本地 git 配置全局的 `user` 与 `email` 参数

(这里的`hello`和`xxx@123.com`要换成你自己的)

在Git Bash 里输入

`git config --global user.name "hello"`

然后按回车键，再输入

`git config --global user.email "xxx@123.com"`

再按回车，现在要在本地生成 `SSH` 秘钥，这时你要输入

`ssh-keygen -t rsa -C "xxx@123.com"`

然后一路回车即可。

安装完之后，打开`C:\Users\Administrator\.ssh` 

会发现其目录底下生成了两个文件，

其中 `id_rsa` 是私钥，`id_rsa.pub` 是公钥。

用记事本打开公钥`id_rsa.pub`，复制里面的全部内容，提交给github。

如何提交给github呢？

进入你的github，点击你的头像，选setting，

再选SSH and GPG keys，点击New SSH key。

Title那里你可以随便填，比如`Hexo blog`。

而Key里面要填的就是你刚才复制的东西，直接黏贴进去即可。

最后按下Add SSH key，搞定！

好了，前期工作准备完成后，现在可以正式来搭建博客了。

### 安装 node.js 
[下载nodejs](https://nodejs.org/en/)

### 安装 hexo
按`win+r`，输入`cmd`，回车。输入命令行：

`npm install hexo-cli -g`

### 搭建博客

（假设，你想把这个博客的代码放在F盘的根目录下）

在Git Bash 里输入（每输完一条指令都要按一下回车键）

`cd f:/`

`mkdir Hexo && cd Hexo`

`hexo init blog`

`cd blog`

`npm install`

`hexo g`

`hexo s`

好了，本地博客搭建完成！

在浏览器地址栏中输入`localhost:4000`即可看到你的本地博客了。

打开`F:/Hexo/blog`可以看到这样的目录中有这些重要文件：

* `_config.yml` ：配置文件，可以修改网站的主题、标题、作者等信息。
* `public` ：由 hexo 根据 source 文件夹中的资源进行渲染生成的文件夹，里边存储着最终的静态网页文件。
* `scaffolds/ `:模板文件，当要给博客添加新文章的时候，将根据对应的模板进行创建。
* `source/ `：用于存储用户资源，比如文章与新页面等。其中以 _ 开头的文件夹中除了 `_posts`文件夹中的 markdown 或 HTML 文件会在执行 generate 操作的时候被渲染添加到 public 文件夹中之外，其他均被忽略。而且在初始化博客的过程中 `_posts` 目录底会自带一个 hello-world.md 的文件。
* `themes/` ：主题文件，自带默认主题 landscape 。

### 部署到 Github Page

进入github，点击你刚才创建的`hello`仓库。

点击Clone or download按钮，

点击网址右边的按钮并按`ctrl+c`（即复制该网址）

打开gitbash.exe。

在Git Bash输入

`cd f:/Hexo/blog`

`git clone https://github.com/hello/hello.github.io`

(这里只是示范。上面的地址你得更换成你刚才复制的那个。
下文出现的`hello`以及`hello.github.io`，
你都要根据你自己的实际username以及仓库名修正)

然后你会发现`F:/Hexo/blog/`目录下多了你的仓库文件夹了。

接着，在Git Bash继续输入(此时目录为`F:/Hexo/blog/`)

`hexo c`

`hexo g`

`cp -R public/* hello.github.io`

`cd hello.github.io`

`git add .`

`git commit -m 'update blog'`

`git push`

至此，完成了部署！

`update blog`只是你提交代码的时候给的注释，你可以随便换成别的。

`git push`过程中需要你输入你的username以及github的密码。

现在，你就可以打开`https://hello.github.io`浏览你的博客了！

（未完待续...）



