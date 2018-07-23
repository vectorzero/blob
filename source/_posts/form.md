---
title: 表单
date: 2017-01-20 23:22:49
tags: 前端开发
---

### 优雅的表单
```css
input:not([type="range"]), textarea, select {
 border: 1px solid #bfbfbf;
 padding: 0.2em;
 font-size: 1.1em;
 line-height: 1.2em;
 background: #ffffff;
 background: linear-gradient(top, #ffffff 0%,#ededed 8%,#ffffff 100%);
 border-radius: 4px;
 box-shadow: 2px 2px 5px hsla(0, 0%, 16.6667%, 0.1);
} 
```

### 针对表单的 CSS3 伪类选择器
 input:required：选择必填表单域；
 input:focus:invalid：选择当前聚焦的且含有非法输入值的表单域；
 input:focus:valid：选择当前聚焦的且含有合法输入值的表单域。
我们使用上面的伪类选择器再编写三条新规则：
```css
input:required {
 border: 1px solid rgba(253, 8, 8, 0.29);
}
input:focus:invalid {
 background: url('../img/cross.png') no-repeat right;
 padding-right: 3px;
}
input:focus:valid {
 background: url('../img/tick.png') no-repeat right;
 padding-right: 3px;
}
```

第一个规则给必填表单域加了一点红色边框：当用户输入时，如果所输入的值不符合规
定格式;

第二个样式会给当前的输入框加上一个红色叉号：如果输入值符合格式；

第三个样式会给其加上一个绿色对号。

<!--more-->

### 响应式网站中的有趣过渡
```css
* {
 transition: all 1s;
} 
```

### list
list 属性以及对应的 datalist 元素可以让用户在输入框中开始输入值的时候，显示一组备选值。
下面是一个包含在 div 中的使用 list 属性及对应 datalist 元素的代码:

```html
<div>
    <label for="awardWon">Award Won</label>
    <input id="awardWon" name="awardWon" type="text" list="awards">
    <datalist id="awards">
    <select>
        <option value="Best Picture"></option>
        <option value="Best Director"></option>
        <option value="Best Adapted Screenplay"></option>
        <option value="Best Original Screenplay"></option>
    </select>
    </datalist>
</div> 
```

使用了 list 属性的输入框看起来就是一个普通的文本输入框，当开始输入时，输入框下面就会显示一个数据选择框，其中包含从 datalist 中检索到的匹配数据。

### type="color"
type="color"——会在支持该特性的浏览器中生成一个颜色选择器，让用户可以选择
十六进制的颜色值。示例代码如下：
```html
<div>
 <label for="color">Your favorite color</label>
 <input id="color" name="color" type="color">
</div> 
```

### 媒体查询能检测那些特性
创建媒体查询时，最常用的是设备的视口宽度（width）和屏幕宽度（device-width）。

依我的经验，很少需要检测其他特性。但是，为方便查阅，下面列出了所有可供媒体查询检测的特性，希望其中有能让你心动的特性。

width：视口宽度。

height：视口高度。

device-width：渲染表面的宽度（对我们来说，就是设备屏幕的宽度）。

device-height：渲染表面的高度（对我们来说，就是设备屏幕的高度）。

orientation：检查设备处于横向还是纵向。

aspect-ratio：基于视口宽度和高度的宽高比。一个 16∶9 比例的显示屏可以这样定义 aspect-ratio: 16/9。
 
device-aspect-ratio：和 aspect-ratio 类似，基于设备渲染平面宽度和高度的宽高比。

color：每种颜色的位数。例如 min-color: 16 会检测设备是否拥有 16 位颜色。

color-index：设备的颜色索引表中的颜色数。值必须是非负整数。

monochrome：检测单色帧缓冲区中每像素所使用的位数。值必须是非负整数。

resolution：用来检测屏幕或打印机的分辨率，如 min-resolution: 300dpi。还
可以接受每厘米像素点数的度量值，如 min-resolution: 118dpcm。

scan：电视机的扫描方式，值可设为 progressive（逐行扫描）或 interlace（隔行扫描）。

如 720p HD 电视（720p 的 p 即表明是逐行扫描）匹配 scan: progressive，

而 1080i HD 电视（1080i 中的 i 表明是隔行扫描）匹配 scan: interlace。

grid：用来检测输出设备是网格设备还是位图设备。

在上述所有特性中，除 scan 和 grid 之外，都可使用 min 和 max前缀来创建一个查询范围。

例如，分析如下所示的代码片段：

@import url("phone.css") screen and (min-width:200px) and (max-width:360px);

这里对 width 应用了 min 和 max 来设定查询范围。

这样 phone.css 文件只会引入视口宽度介于 200 像素至 360 像素的显示屏设备。

CSS3可以让我们将一段或多段内容分布到多列网格中。请看如下代码：
```html
<div id="main" role="main">
 <p>lloremipsimLoremipsum dolor sit amet, consectetur
 // 任意文字 //
</p>
 <p>lloremipsimLoremipsum dolor sit amet, consectetur
 // 任意文字 //
</p>
<p>lloremipsimLoremipsum dolor sit amet, consectetur
 // 任意文字 //
</p>
</div>
```
你可以通过设定具体栏位宽度（如 12em）或者栏位数量（如 3）来使内容分布在多列网格中，做法如下。

如果设定栏位宽度，语法如下所示（注意，为简洁起见代码中省略了私有前缀）：
```css
#main {
 column-width: 12em;
}
```
按照上述的设定，无论视口尺寸是多少，内容都会分布在宽度为 12em 的栏位中。视口尺寸发生变化之后，浏览器会自动调整栏位数量。

如果你想保持栏位数量不变而让栏位宽度根据视口自动调整，可以参考如下代码：
```css
#main {
 column-count: 4;
} 
```
增加栏位间隙和分割线可以让多列布局的效果更好，代码如下：
```css
#main {
 column-gap: 2em;
 column-rule: thin dotted #999;
 column-width: 12em;
} 
```

### 文字换行
适合给超长url换行
`word-wrap: break-word;` 

### CSS3 的子字符串匹配属性选择器
CSS3 可以让我们基于属性选择器的子字符串来选择元素。听起来有点复杂，实际上并不深奥。换句话说，现在我们可以根据属性的部分内容来选择元素。三种匹配模式分别是：
    以特定前缀开头；
    包含特定字符串；
    以特定后缀结尾。
我们来看看具体用法。
(1)“匹配开头”的属性选择器。
“匹配开头”的属性选择器语法如下：
`Element[attribute^="value"]`
在实际使用中，如果我想选择网站中所有 alt 属性值以 film 开头的图片，则对应代码如下：
```css
img[alt^="film"] {
 border: 3px dashed #e15f5f;
}
```
该选择器的关键字符是^符号，它的意思是“以此开头”。
(2)“匹配包含内容”的属性选择器。
“匹配包含内容”的属性选择器语法如下：
`Element[attribute*="value"]`
在实际使用中，如果我想选择网站中所有 alt 属性值中包含 film 字符串的图片，则对
应代码如下：
```css
img[alt*="film"] {
 border: 3px dashed #e15f5f;
}
```
该选择器的关键字符是*符号，它的意思是“包含”。
(3)“匹配结尾”的属性选择器。
“匹配结尾”的属性选择器语法如下：
`Element[attribute$="value"]`
在实际使用中，如果我想选择网站中所有 alt 属性值以 film 结尾的图片，则对应代码
如下：
```css
img[alt$="film"] {
 border: 3px dashed #e15f5f;
}
```
该选择器的关键字符是$，它的意思是“以此结尾” 

### HSL 颜色

除了 RGB，CSS3 还可使用 HSL（色相、饱和度、亮度）模式来声明颜色。

`hsl(315, 100%, 60%)`

顺口溜 黄绿青蓝紫

HSL 模式基于一个 360°的色相环，第一个数字代表色相，60°时为黄色，120°时为绿色，180°时为青色，240°时为蓝色，300°时为洋红色，360°时为红色。

所以前面提到的 HSL 颜色色相为315，

所以很容易看出它介于洋红（300°）和红（360°）之间。

其后的两个值分别表示饱和度和亮度，值为百分比，用于改变基础的色相。

如果想要更加饱满的颜色，则第二个值使用一个高一点的百分比即可。

最后一个值控制亮度，可在 0%的全黑到 100%的全白之间变化。

CSS3 还允许通过 opacity 声明来设置元素的透明度。

该透明度的值也是一个介于 0 到 1 之间的小数（如将 opacity 设置为 0.1 表示为 10%透明）。

但是这种透明度与 RGBA 及 HSLA有所不同，这种方式设置的透明度会对整个元素产生影响（元素的内容都会透明）。

反之，使用 HSLA或 RGBA 则可以仅让元素的某些部分有透明效果。

这样，一个元素可以带有 HSLA 透明背景，但内部的文字仍然不透明。