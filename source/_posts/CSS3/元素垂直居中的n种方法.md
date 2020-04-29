---
title: 元素垂直居中的n种方法
summary:
  - '我们在做页面布局的时候经常会有上下左右居中的设计，由于大部分的页面结构都是左右式排版页面是固定宽度的，而元素是自上而下排列，高度不固定。所以在页面中css实现左右居中比较容易，垂直居中就不太好实现了。'
  - '在css3之前我们前端技术人员要实现垂直居中布局往往需要绞尽脑汁的去解决各种浏览器兼容问题，而随着时间的推移，ie浏览器已经退出历史舞台，现在的浏览器已经完全支持css3的各种布局方式，在css3中实现居中布局已经变得非常容易'
p: CSS3/元素垂直居中的n种方法
date: 2020-04-29 09:54:45
categories:
tags:
poster: poster.png
---


# 元素垂直居中的n种方法

> 本文章收集了多种实现居中布局的方法，并且按照实现的时间线，从css2到css3的各种解决方案，从代码量有少到多的排序来一一说明每种布局方法的实现方式，通过阅读此文章能够让你解决平时的开发中遇到的各种布局问题。

## 使用line-height实现单行文本垂直居中

> `line-height`：用于设置多行元素的空间量，如多行文本的间距。对于块级元素，它指定元素行盒（line boxes）的最小高度。对于非替代的 inline 元素，它用于计算行盒（line box）的高度。

```css
.box-1{
    height: 50px;
    line-height: 50px;
}
```

```html
<div class="box box-1">
    这是要垂直居中的内容。
</div>
```

**查看案例：** [https://codepen.io/qwguo88/full/dyYvBQv](https://codepen.io/qwguo88/full/dyYvBQv)


<iframe height="500" style="width: 100%;" scrolling="no" title="vertical-middle-line-height" src="https://codepen.io/qwguo88/embed/dyYvBQv?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/dyYvBQv'>vertical-middle-line-height</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## 使用inline-block元素和vertical-align特性实现垂直居中
> 此方法不限制元素的宽高，兼容性好

1. `vertical-align`：用来指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。

```html
<div class="box">
    <div class="content">
        这是要垂直居中的内容。
    </div>
</div>
```

```css
.box{
  text-align: center;
  letter-spacing: -.3em;
}
.box::before{
  content: '';
  height: 100%;
  width: 1px;
  margin-right: -1px;
  display:inline-block;
  vertical-align: middle;
}
.content{
  display:inline-block;
  vertical-align: middle;
  letter-spacing: normal;
}
```

**查看案例：** [https://codepen.io/qwguo88/full/KKdmvdj](https://codepen.io/qwguo88/full/KKdmvdj)

<iframe height="500" style="width: 100%;" scrolling="no" title="vertical-middle-inline-block" src="https://codepen.io/qwguo88/embed/KKdmvdj?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/KKdmvdj'>vertical-middle-inline-block</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



上面的案例通过利用`display:inline-block`的高度100%于父级高度，再利用`vertical-aling:middle`垂直居中属性，让行内块级元素剧中与父级。在元素设置成行内块级元素的时候代码中如果元素后边有空格，可以通过设置父级元素`letter-spacing:-.3em`，然后在通过居中元素还原文字间隔，或者通过设置父级的`font-size:0;`也可以取消空格的间距。其中红色竖线是通过父元素的伪类设置的。


## 使用表格单元格和vertical-align特性实现垂直居中

```html
<div class="box">
  <div class="content">
    这是要垂直居中的内容。
  </div>
</div>
```
```css
.box{
  display: table-cell;
  vertical-align: middle;
  text-align:center;
}
.content{
  display:inline-block;
}
```

此方法需要设置父级的父级为`diaplay:table;`，并且设置父元素：`display:table-cell`，然后在设置`vertical-align:middle`，实现元素居中，但是此方法子元素需要是行内元素，和行内块级元素;

**查看案例：** [https://codepen.io/qwguo88/full/qBOmPaM](https://codepen.io/qwguo88/full/qBOmPaM)

<iframe height="500" style="width: 100%;" scrolling="no" title="vertical-middle-table-cell" src="https://codepen.io/qwguo88/embed/qBOmPaM?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/qBOmPaM'>vertical-middle-table-cell</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## 使用绝对定位absolute和margin负值

> 此方法用于固定宽高的元素，或者通过js获取不固定元素宽高

```html
<div class="box">
  <div class="content">
    这是要垂直居中的内容。
  </div>
</div>
```
```css
.box{
  position: relative;
}
.content{
  position: absolute;
  width: 100px;
  height: 100px;
  left: 50%;
  top: 50%;
  margin: -50px 0 0 -50px;
}
```

此方法需要设置元素依照父级绝对定位，left和top都按照父元素50%定位。且需要知道要居中元素的宽高，也可以通过javascript获取元素的宽高，并且设置`margin`的上和左为负值元素宽高的一半；


## 使用绝对定位absolute和margin:auto

> 此方法需要设置居中元素为固定宽高

```html
<div class="box">
  <div class="content">
    这是要垂直居中的内容。
  </div>
</div>
```
```css
.box{
  position: relative;
}
.content{
  position: absolute;
  width: 100px;
  height: 100px;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
```

此方法利用`margin: auto;`居中特性加决定定位上下左右为0来实现元素居中，此方法需要固定元素的宽高，并且决对定位于父元素。兼容ie8以上浏览器.

## 使用绝对定位absolute和css3的transform:translate属性

```html
<div class="box">
  <div class="content">
    这是要垂直居中的内容。
  </div>
</div>
```
```css
.box{
  position: relative;
}
.content{
  position: absolute;
  left: 50%;
  top: 50%;
  transform:translate(-50%, -50%);
}
```
此方法利用了css3的新特性元素偏移属性，先让元素绝对定位于父元素的右、上的50%，然后通过`transform:translate(-50%, -50%);`设置元素按照自身的右上便宜50%实现居中，此方法不用的优点：不用固定元素宽高，缺点：兼容需要支持css3的浏览器。


**案例说明：** [https://codepen.io/qwguo88/full/jObmLaN](https://codepen.io/qwguo88/full/jObmLaN)


<iframe height="500" style="width: 100%;" scrolling="no" title="vertical-middle-absolute-margin" src="https://codepen.io/qwguo88/embed/jObmLaN?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/jObmLaN'>vertical-middle-absolute-margin</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## 使用flex实现居中

>通过flex弹性布局有好多种方式可以居中对齐，可以给父级单独设置，或者父级子级结合设置实现

**html代码结构完全一样：**
```html
<div class="box">
    <div class="content">
      这是要垂直居中的内容。
    </div>
</div>
```

### 方法1：

```css
.box{
    display: flex;
    justify-content: center;
    align-items: center;
}
```
> 最简单的方法，只通过父级设置，把父元素设置成弹性很模型，然后设置父元素的子元素横向纵向居中显示。

### 方法2：

```css
.box{
    display: flex;
    justify-content: center;
    align-content: center;
    flex-wrap: wrap;
}
```

> 也是只通过父级设置，把父元素设置成弹性很模型，然后设置父元素的子元素横向居中显示，然后通过弹性很模型的子元素组`align-content:center`对齐方式，配合`flex-wrap:wrap`实现。

### 方法3：

```css
.box{
    display: flex;
    flex-direction: column;
    align-items: center;
}
.box:before{
    content: '';
    flex-grow: .5;
}
```

> 这个也只只给父级设置，不同的是这个需要借助父级的伪元素；先把父元素设置成弹性很模型，然后设置纵向排列，然后设置横轴左右居中，然后再借助父元素伪类，设置纵向占据父元素的.5大小，实现上下居中。

### 方法4：

```css
.box{
    display: flex;
}
.content{
    margin: auto;
}
```

> 把父元素设置成弹性很模型，然后通过要居中的子元素设置margin:auto，元素外间距依照父级自适应外间距。

### 方法5：

```css
.box{
    display: flex;
    justify-content: center;
}
.content{
    align-self: content
}
```

> 把父元素设置成弹性很模型，然后子元素设置align-self: content。

**查看案例：** [https://codepen.io/qwguo88/full/ZEbKgXG](https://codepen.io/qwguo88/full/ZEbKgXG)

<iframe height="500" style="width: 100%;" scrolling="no" title="vertical-middle-flex" src="https://codepen.io/qwguo88/embed/ZEbKgXG?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ZEbKgXG'>vertical-middle-flex</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## 使用grid网格布局实现居中
> 通过css的最新布局形式`grid`网格布局，也有多种方式，网格布局也可以给父级单独设置，或者父级子级结合设置实现

**html代码结构完全一样：**
```html
<div class="box">
    <div class="content">
      这是要垂直居中的内容。
    </div>
</div>
```
### 方法1：

```css
.box{
    display: grid;
    place-content: center;
}
```


### 方法2：

```css
.box{
    display: grid;
    place-items: center;
}
```

### 方法3：

```css
.box{
    display: grid;
    justify-content: center;
    align-content: center;
}
```
### 方法4：

```css
.box{
    display: grid;
    justify-content: center;
    align-items: center;
}
```

### 方法5：

```css
.box{
    display: grid;
}
.content{
    margin: auto;
}
```
### 方法6：

```css
.box{
    display: grid;
    justify-content: center;
}
.content{
    align-self: center;
}
```
**查看案例：** [https://codepen.io/qwguo88/full/PoPmJbo](https://codepen.io/qwguo88/full/PoPmJbo)

<iframe height="500" style="width: 100%;" scrolling="no" title="vertical-middle-grid" src="https://codepen.io/qwguo88/embed/PoPmJbo?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/PoPmJbo'>vertical-middle-grid</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



