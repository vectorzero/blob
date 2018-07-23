---
title: css
date: 2016-12-08 21:10:28
tags: 前端开发
---

## CSS
### 选中文字样式
```css
::selection{
    background-color: green;
    color: #fff;
}
```

### 垂直居中 （兼容IE6）
```css
.box{
    width: 200px;
    height: 300px;
    border: 1px solid #ccc;
    position: fixed;
    left: 50%;
    top: 50%;
    margin-left: -100px;
    margin-top: -150px;
    _position: absoulte;
    _left: expression(eval(document.documentElement.clientWidth/2+document.document.documentElement.scrollLeft));
    _top: expression(eval(document.documentElement.clientHeight/2+document.document.documentElement.scrollTop));
}
```