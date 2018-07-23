---
title: code clip
date: 2016-12-08 22:30:04
tags: 前端开发
---

## Code Clip
### 根据屏幕大小更改样式
**jQuery**
```javascript
if (window.screen.width < 1920||$(window).width()<1920) {
            $(document.body).css({
                "overflow-y": "auto"
            });
        }; 
```
### 根据屏幕大小以及浏览器更改样式
**html**
```html
<!--[if IE 8]>
<script>
        $(document).ready(function () {
            window.onresize = function () { location = location };
            if ($(window).width() < 1400) {
                $(".spanFont").css("font-size", "16px");
            } else {}
        })
</script>
<![endif]-->
```
### 回车登录
**html**
```html
<body onkeydown="keyLogin(et)">
```

**jQuery**

```javascript
function keyLogin(et){
        if (et.keyCode==13||et.which==13)
            document.getElementById("login-btn").click();
}
```
### 禁止右键
**jQuery**
```javascript
$(document).ready(function(){ 
    $(document).bind("contextmenu",function(e){ 
        return false; 
    }); 
});
```

### 页面样式切换
**jQuery**
```javascript
$(document).ready(function() { 
    $("a.Styleswitcher").click(function() { 
        $('link[rel=stylesheet]').attr('href' , $(this).attr('rel'));
    }); 
});
```

**html**
```html
<head>
    <link rel=stylesheet type=text/css href="default.css">
</head>
    <a class="Styleswitcher" href="#" rel="default.css">Default Theme</a> 
    <a class="Styleswitcher" href="#" rel="red.css">Red Theme</a> 
    <a class="Styleswitcher" href="#" rel="blue.css">Blue Theme</a>     
```
