---
title: webpack
date: 2017-01-20 22:51:54
tags: 工具
---
### 安装node.js

`win+R` 输入`cmd` 并回车

输入 `node -v` 查看node版本

输入 `npm -v` 查看npm版本

### 安装webpack
输入 `npm install webpack -g`

此时 Webpack 已经安装到了全局环境下，可以通过命令行 `webpack -h` 查看。

通常我们会将 Webpack 安装到项目的依赖中，

这样就可以使用项目本地版本的 Webpack。

进入项目目录，若没有package.json，

在项目目录下按 `shift+鼠标右键` 选中“在此处打开命令窗口”，

输入 `npm init` 并且一路回车即可。

接下来直接输入 `npm install webpack --save-dev`

若你看到node_module文件夹，则说明你安装成功

（PS：安装指定版本的 webpack，请输入 npm install webpack@1.12.x --save-dev）

<!-- more -->

### 使用webpack
在项目目录下创建一个index.html和一个js入口文件entry.js
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <script src="bundle.js"></script>
</body>
</html>
```

```javascript
// entry.js
document.write("it works")
```

然后编译entry.js并打包到bundle.js:

`webpack entry.js bundle.js`

用浏览器打开index.html将会看到 it works

接下来添加一个模块 module.js 并修改入口 entry.js:
```javascript
//module.js
module.exports = 'it works from module.js'
```

```javascript
//entry.js
document.write("it works")
document.write(require('./module.js'))//添加模块
```

重新打包 webpack entry.js bundle.js 后刷新页面可以看到

it works it works from module.js

Webpack 会分析入口文件，解析包含依赖关系的各个文件。

这些文件（模块）都打包到 bundle.js 。

Webpack 会给每个模块分配一个唯一的 id 并通过这个 id 索引和访问模块。

在页面启动时，会先执行 entry.js 中的代码，

其它模块会在运行 require 的时候再执行。

### Loader
Webpack 本身只能处理 JavaScript 模块，

如果要处理其他类型的文件，就需要使用 loader 进行转换。

Loader 可以理解为是模块和资源的转换器，

它本身是一个函数，接受源文件作为参数，返回转换的结果。

这样，我们就可以通过 require 来加载任何类型的模块或文件，

比如 CoffeeScript、 JSX、 LESS 或图片。

Loader 可以在 require() 引用模块的时候添加，

也可以在 webpack 全局配置中进行绑定，还可以通过命令行的方式使用。

若在页面中引入一个 CSS 文件 style.css，

index将 style.css 也看成是一个模块，然后用 css-loader 来读取它，

再用 style-loader 把它插入到页面中。

```css
/* style.css */
body { background: yellow; }
```

修改entry.js
```javascript
    require("!style!css!./style.css") // 载入 style.css
    document.write('It works.')
    document.write(require('./module.js'))
```

安装loader:

`npm install css-loader style-loader`

重新编译打包，刷新页面，就可以看到黄色的页面背景了。

你也可以将entry.js中的`require("!style!css!./style.css")` 

修改为 `require("./style.css")` ，然后执行：

`webpack entry.js bundle.js --module-bind "css=style!css"`

这样做会得到同样的效果。

### 配置文件

Webpack 在执行的时候，除了在命令行传入参数，还可以通过指定的配置文件来执行。

默认情况下，会搜索当前目录的 webpack.config.js 文件，

这个文件是一个 node.js 模块，返回一个 json 格式的配置信息对象，

或者通过 --config 选项来指定配置文件。

继续我们的案例，在根目录创建 package.json 来添加 webpack 需要的依赖。

即在原本的package.json的devDependencies中加上

```
"css-loader": "^0.21.0",
"style-loader": "^0.13.0",
```

```javascript
{
  "name": "webpack-example",
  "version": "1.0.0",
  "description": "A simple webpack example.",
  "main": "bundle.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "webpack"
  ],
  "author": "",
  "license": "MIT",
  "devDependencies": {
    "css-loader": "^0.21.0",
    "style-loader": "^0.13.0",
    "webpack": "^1.14.0"
  }
}
```

接着运行 `npm install`

然后创建一个配置文件 webpack.config.js：

```javascript
var webpack = require('webpack')

module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {test: /\.css$/, loader: 'style!css'}
    ]
  }
}
```

同时简化 entry.js 中的 style.css 加载方式：
`require('./style.css')`

最后运行 `webpack`，可以看到 webpack 通过配置文件执行的结果和前面通过命令行 

`webpack entry.js bundle.js --module-bind 'css=style!css' `

执行的结果是一样的。

### 插件
插件可以完成更多 loader 不能完成的功能。

插件的使用一般是在 webpack 的配置信息 plugins 选项中指定。

Webpack 本身内置了一些常用的插件，还可以通过 npm 安装第三方插件。

接下来，我们利用一个最简单的 BannerPlugin 内置插件来实践插件的配置和运行，

这个插件的作用是给输出的文件头部添加注释信息。

修改 webpack.config.js，添加 plugins：

```javascript
var webpack = require('webpack')

module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {test: /\.css$/, loader: 'style!css'}
    ]
  },
  plugins: [
    new webpack.BannerPlugin('This file is created by vector')
  ]
}
```

然后运行 `webpack`，打开 bundle.js，可以看到文件头部出现了我们指定的注释信息：

```
/*! This file is created by vector */
/******/ (function(modules) { // webpackBootstrap
/******/  // The module cache
/******/  var installedModules = {};
// 后面代码省略
```

### 开发环境

当项目逐渐变大，webpack 的编译时间会变长，

可以通过参数让编译的输出内容带有进度和颜色。

`webpack --progress --colors`

如果不想每次修改模块后都重新编译，那么可以启动监听模式。

开启监听模式后，没有变化的模块会在编译后缓存到内存中，

而不会每次都被重新编译，所以监听模式的整体速度是很快的。

`webpack --progress --colors --watch`

当然，使用 `webpack-dev-server` 开发服务是一个更好的选择。

它将在 localhost:8080 启动一个 express 静态资源 web 服务器，

并且会以监听模式自动运行 webpack，

在浏览器打开 http://localhost:8080/ 或 http://localhost:8080/webpack-dev-server/ 

可以浏览项目中的页面和编译后的资源输出，

并且通过一个 socket.io 服务实时监听它们的变化并自动刷新页面。

安装 `npm install webpack-dev-server -g`

运行 `webpack-dev-server --progress --colors`

### 故障处理
一般情况下，webpack 如果出问题，会打印一些简单的错误信息，比如模块没有找到。

我们还可以通过参数 `--display-error-details` 来打印错误详情:

`webpack --display-error-details`

### 参考链接 
[webpackdoc](http://webpackdoc.com/index.html)