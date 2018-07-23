---
title: hack
date: 2016-12-08 21:12:04
tags: 前端开发
---

### 常用的CSS hack方式
方式一 **条件注释法**

只在IE下生效
```
<!--[if IE]>
  这段文字只在IE浏览器显示
<![endif]-->
```

只在IE6下生效
```
<!--[if IE 6]>
  这段文字只在IE6浏览器显示
<![endif]-->
```

只在IE6以上版本生效
```
<!--[if gte IE 6]>
  这段文字只在IE6以上(包括)版本IE浏览器显示
<![endif]-->
```

只在IE8上不生效
```
<!--[if ! IE 8]>
  这段文字在非IE8浏览器显示
<![endif]-->
```

非IE浏览器生效
```
<!--[if !IE]>
  这段文字只在非IE浏览器显示
<![endif]-->
```

<!-- more -->

方式二 **类内属性前缀法**

`-`减号是IE6专有的hack

`\9` IE6/IE7/IE8/IE9/IE10都生效

`\0` IE8/IE9/IE10都生效，是IE8/9/10的hack

`\9\0` 只对IE9/IE10生效，是IE9/10的hack

方式三 **选择器前缀法**

`*` 只对IE6生效

`*+` 只对IE7生效

`@media screen\9{ body { background: green; }}` 只对IE6/7生效

`@media \0screen {body { background: green; }}` 只对IE8有效

`@media \0screen\,screen\9{ body { background: green; }}` 只对IE6/7/8有效

`@media screen\0{body { background: green; }}` 只对IE8/9/10有效

`@media screen and (min-width:0\0) {body { background: gray; }}` 只对IE9/10有效

`@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {body { background:orange; }}` 只对IE10有效

### 区别FF，IE7，IE6
**css**
```css
body{
  background:green !important; 
  background:orange; 
  *background:blue;
}
```

IE6能识别*和下划线，但不能识别 !important

IE7能识别*，不能识别下划线但能识别!important

FF不能识别*和下划线，但能识别!important

另外再补充一个，下划线”_“,IE6支持下划线，IE7和firefox均不支持下划线

**css**
```css
body{
  background:green!important; 
  *background:orange; 
  _background:blue;
  }
```

注：不管是什么方法，书写的顺序都是firefox的写在前面，IE7的写在中间，IE6的写在最后面

\9:支持IE浏览器

\0:支持IE8浏览器

### IE8 兼容placeholder
**jQuery**
```javascript
if( !('placeholder' in document.createElement('input')) ){  
    $('input[placeholder],textarea[placeholder]').each(function(){   
      var that = $(this),   
      text= that.attr('placeholder');   
      if(that.val()===""){   
        that.val(text).addClass('placeholder');   
      }   
      that.focus(function(){   
        if(that.val()===text){   
          that.val("").removeClass('placeholder');   
        }   
      })   
      .blur(function(){   
        if(that.val()===""){   
          that.val(text).addClass('placeholder');   
        }   
      })   
      .closest('form').submit(function(){   
        if(that.val() === text){   
          that.val('');   
        }   
      });   
    });   
  }  
```
**css**
```css
.placeholder{
    color: #888;
}
```

<!-- more -->

### Bootstrap 3兼容IE8浏览器
**html**
```html
<!doctype html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="author" content="Jophy" />
    <title>ie8</title>
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <link rel="stylesheet" href="bootstrap/css/style.css">
    <!--[if lte IE 9]>
    <script src="bootstrap/js/respond.min.js"></script>
    <script src="bootstrap/js/html5.js"></script>
    <![endif]-->
    <script src="http://libs.baidu.com/jquery/1.10.2/jquery.js"></script>
    <script src="bootstrap/js/bootstrap.min.js"></script>
</head>
<body>
</body>
</html>
```

### 兼容IE8的rgba()的方法
**css**
```css
//一般的高级浏览器都支持
background: rgba(255,255,255,0.1);

//IE8下
filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#19ffffff,endColorstr=#19ffffff);
```

第二句话的意思就是当上一行的透明度不起作用的时候执行。这句话的意思本来是用来做渐变的。但是这个地方不需要渐变。所以两个颜色都设置成了相同的颜色。

这个颜色“#19ffffff”是由两部分组成的。
第一部是#号后面的19 。是rgba透明度0.1的IEfilter值。从0.1到0.9每个数字对应一个IEfilter值。

第二部分是19后面的六位 。这个是六进制的颜色值。要跟rgb函数中的取值相同。比如rgb(255,255,255)对应#ffffff；就是白色。

| rgba透明值 | IEfilter值 |
| :-: | :-: |
| 0.1 | 19 |
| 0.2 | 33 |
| 0.3 | 4C |
| 0.4 | 66 |
| 0.5 | 7F |
| 0.6 | 99 |
| 0.7 | B2 |
| 0.8 | C8 |
| 0.9 | E5 |

### IE8里点击按钮、链接会出现虚线边框的问题
**css**
```css
a,button,input{
    outline:none!important;
}
```
