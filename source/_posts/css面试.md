---
title: css面试
date:
updated:
type: "tags"
categories: 面试
comments:
description: css面试
keywords: css面试
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 1.居中为什么用transform，而不是margin top/left
```js
Chrome渲染主要包括Parse Html、Recalculate Style、Layout、Paint、Image Decode、Image Resize和Composite Layers等。相对应的中文表述就是：html解析、查找并计算样式、排布、绘制、图片解码、图片大小设置、合并图层并输出页面到屏幕。浏览器最终渲染出来的页面
top/left是布局类的样式，这个样式的变化会导致重排（reflow/relayout），所谓重排即指对这些节点以及受这些节点影响的其它节点，进行CSS计算->布局->重绘过程，这个过程的前2步是消耗大量资源的translate是一个绘制样式（这名词我瞎编的），这个样式的变化会导致重绘（repaint），即在屏幕上重新画一下，不会进行CSS计算和布局这2个性能大户，所以我们认为translate性能上要明显好于top/lefttranslate3D传说因为走的是3D，所以能得到更完整的GPU加速的支持，在GPU中还有贴图缓存等手段帮你优化性能，所以更快
```

# 2.粘性布局(sticky)
```js
设置了position: sticky的元素并不脱离文档流，仍然保留元素原本在文档流中的位置。
当元素在容器中被滚动超过指定的偏移值时，元素在容器内固定在指定位置。亦即如果你设置了top: 50px，那么在sticky元素到达距离相对定位的元素顶部50px的位置时固定，不再向上移动（相当于此时fixed定位）。
元素固定的相对偏移是相对于离它最近的具有滚动框的祖先元素，如果祖先元素都不可以滚动，那么是相对于viewport来计算元素的偏移量
```

# 3.分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景
```js
总结一下：
结构：
display:none: 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击，
visibility: hidden:不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击
opacity: 0: 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击

继承：
display: none和opacity: 0：是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示。
visibility: hidden：是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式。

性能：
displaynone : 修改元素会造成文档回流,读屏器不会读取display: none元素内容，性能消耗较大
visibility:hidden: 修改元素只会造成本元素的重绘,性能消耗较少读屏器读取visibility: hidden元素内容
opacity: 0 ： 修改元素会造成重绘，性能消耗较少

联系：它们都能让元素不可见
```

# 4.介绍下 BFC 及其应用
```js
BFC 就是块级格式上下文，是页面盒模型布局中的一种 CSS 渲染模式，相当于一个独立的容器，里面的元素和外部的元素相互不影响。创建 BFC 的方式有：

html 根元素
float 浮动
绝对定位
overflow 不为 visiable
display 为表格布局或者弹性布局
BFC 主要的作用是：

清除浮动
防止同一 BFC 容器中的相邻元素间的外边距重叠问题
```

# 5.理解@import和link引入样式的区别
```js
1.从属关系区别@import是 CSS 提供的语法规则，只有导入样式表的作用；link是HTML提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。
2.加载顺序区别加载页面时，link标签引入的 CSS 被同时加载；@import引入的 CSS 将在页面加载完毕后被加载。
3.兼容性区别@import是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link标签作为 HTML 元素，不存在兼容性问题。
4.DOM可控性区别可以通过 JS 操作 DOM ，插入link标签来改变样式；由于DOM方法是基于文档的，无法使用@import的方式插入样式。
5.权重区别
```

# 6.css reset 和 normalize.css 有什么区别
```js
两者都是通过重置样式，保持浏览器样式的一致性
前者几乎为所有标签添加了样式，后者保持了许多浏览器样式，保持尽可能的一致
后者修复了常见的桌面端和移动端浏览器的bug：包含了HTML5元素的显示设置、预格式化文字的font-size问题、在IE9中SVG的溢出、许多出现在各浏览器和操作系统中的与表单相关的bug。
前者中含有大段的继承链
后者模块化，文档较前者来说丰富
```

# 7.圣杯布局
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style type="text/css">
    *{
        margin: 0;
        padding: 0;
        color: black;
        font-size: 45px
    }
    .main>div{
        float: left;
    }
    .main{
       width: 100%;
       background: yellow
    }
    .center{
        background: red;
        margin-left: 200px;
        margin-right: -200px;
        width: 100%
    }
    .left{
       background: pink ;
       width: 200px;
       margin-left: -100%
    }
    .right{
       background: blue ;
       width: 200px;
       margin-right: -200px
    }
</style>
</head>
<body>
    <div class="main">
        <div class="center">中间</div>
        <div class="left">左边</div>
         <div class="right">右边</div>
    </div>

</body>
</html>

```

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
    *{
        margin: 0;
        padding: 0;
        color: black;
        font-size: 45px
    }
    .main div{
        box-sizing: border-box;
    }
    .main{
       width: 100%;
       background: red;
       position: relative;
       padding-left: 200px;
       padding-right: 200px;
    }
    .center{
        width: 100%;
        background: pink
    }
    .left{
       background: yellow ;
       width: 200px;
      position: absolute;
      left: 0;
      top: 0;
    }
    .right{
       background: blue ;
       width: 200px;
        position: absolute;
      top: 0;
      right:0
    }
</style>
</head>
<body>
    <div class="main">
        <div class="center">z中间</div>
        <div class="left">左</div>
        <div class="right">右</div>
    </div>

</body>
</html>
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    *{
        margin:0;padding:0;
    }
    .container{
        display: flex;
        height: 100vh;
        flex-direction: column;
    }
    header{
        background: #000;
    }
    section{
        flex:1;
        background: pink;
        display: flex;
    }
    footer{
        background: #000;
    }
    .left{
        background: red;
        flex:0 0 100px;
    }
    .center{
        flex:1;
        background: blue;
    }
    .right{
        flex:0 0 100px;
        background: red;
    }
    </style>
</head>
<body>

<div class='container'>

    <header>头部</header>
    <section>
        <div class='left'>左</div>
        <div class='center'>中</div>
        <div class='right'>右</div>
    </section>
    <footer>底部</footer>

</div>

</body>
</html>
```

### 8.css的两种盒模型
```js
W3C的标准盒模型:在标准的盒子模型中，width指content部分的宽度
IE的盒模型:在IE盒子模型中，width表示content+padding+border这三个部分的宽度
我们可以看出我们上面的使用的默认正是W3C标准盒模型
 /* 是W3C盒子模型 */
box-sizing: content-box
/* 是IE盒子模型 */
box-sizing: border-box 
```

# 8.清除浮动的方法（最常用的4种）
```js
 .fahter{
        width: 400px;
        border: 1px solid deeppink;
    }
    .big{
        width: 200px;
        height: 200px;
        background: darkorange;
        float: left;
    }
    .small{
        width: 120px;
        height: 120px;
        background: darkmagenta;
        float: left;
    }
    .footer{
        width: 900px;
        height: 100px;
        background: darkslateblue;
    }
    .clear{
        clear:both;
    }
    <div class="fahter">
        <div class="big">big</div>
        <div class="small">small</div>
        <div class="clear">额外标签法</div>
    </div>
    <div class="footer"></div>
</body>
</html>
```
父级添加overflow属性（父元素添加overflow:hidden）（不推荐）
```js
.fahter{
        width: 400px;
        border: 1px solid deeppink;
        overflow: hidden;
    }
```

使用after伪元素清除浮动（推荐使用）
```js
.clearfix:after{/*伪元素是行内元素 正常浏览器清除浮动方法*/
        content: "";
        display: block;
        height: 0;
        clear:both;
        visibility: hidden;
    }
    .clearfix{
        *zoom: 1;/*ie6清除浮动的方式 *号只有IE6-IE7执行，其他浏览器不执行*/
    }

<body>
    <div class="fahter clearfix">
        <div class="big">big</div>
        <div class="small">small</div>
        <!--<div class="clear">额外标签法</div>-->
    </div>
    <div class="footer"></div>
</body>
```
使用before和after双伪元素清除浮动
```js
 .clearfix:after,.clearfix:before{
        content: "";
        display: table;
    }
    .clearfix:after{
        clear: both;
    }
    .clearfix{
        *zoom: 1;
    }

 <div class="fahter clearfix">
        <div class="big">big</div>
        <div class="small">small</div>
    </div>
    <div class="footer"></div>
```