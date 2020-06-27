---
title: 页面布局之两列布局的n种方法
summary:
  - 两列布局使我们再做页面的时候用的最多的布局方式，也是设计稿种最常见的一种布局类型，一般分为：一列固定宽度另一列自适应宽度，两列自适应宽度，两列相同高度等形式
  - 这篇文章将详细介绍各种两列布局的实现方式
drafts: false
p: CSS/两列布局的n种方法
date: 2020-06-24 21:57:54
categories:
tags:
poster:
---
# 页面布局之两列布局的n种方法

## 两列布局之表格布局
> 说起表格布局是在css3之前兼容性最好的一种布局方式，使用表格做两列自适应宽度或者高度布局能够在ie6浏览器中得到很好的兼容。

**示例：**
查看案例：[https://codepen.io/qwguo88/full/pogwJRK](https://codepen.io/qwguo88/full/pogwJRK)
<iframe height="500" style="width: 100%;" scrolling="no" title="two-columns-layout-table" src="https://codepen.io/qwguo88/embed/pogwJRK?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/pogwJRK'>two-columns-layout-table</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

从上边的案例中可以看到通过使用表格能够轻松实现左右列高度一样的效果，而不用担心左右内容不同意的问题。优点：自适应强，兼容性好；缺点html结构代码量多。

## 两列布局之浮动布局
> 浮动布局是继表格布局后比较常用的一种布局方式，它通过给元素设置左右浮动实现。

**示例：**
查看案例： [https://codepen.io/qwguo88/full/eYJRNXq](https://codepen.io/qwguo88/pen/eYJRNXq)
<iframe height="500" style="width: 100%;" scrolling="no" title="two-columns-layout-float" src="https://codepen.io/qwguo88/embed/eYJRNXq?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/eYJRNXq'>two-columns-layout-float</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

通过上边的各种案例可以看出，浮动布局在html结构代码上比表格精简了很多，但是要想实现一些特殊效果还需要些通过不同方式实现，同时还需要解决由浮动带来的各种问题
1. 比如浮动后父级高度不能自适应内容高度，需要给父级设置overflow来触发父级的BFC，或者给父级设置伪类，或者添加空div清除浮动方式来解决高度塌陷问题。
2. 不能做到两列高度统一，也需要借助其他方式解决，给一个列添加外部div并且设置和另一列一样的背景颜色来在视觉上达到一样高度的效果。

浮动布局的优点：结构代码量少，代码看上区可读性强；缺点：需要解决由浮动带来的一系列问题，无法实现真正意义上的左右高度一样效果。

## 两列布局之行内块元素

**示例：**
查看案例：[https://codepen.io/qwguo88/full/wvMeMGB](https://codepen.io/qwguo88/pen/wvMeMGB)

<iframe height="500" style="width: 100%;" scrolling="no" title="two-columns-layout-inline-block" src="https://codepen.io/qwguo88/embed/wvMeMGB?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/wvMeMGB'>two-columns-layout-inline-block</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

行内块元素布局优点：
它能够解决浮动布局带来的问题，
1.  两列高度不一样的问题（前提必须给父级设置高度）；
2. 不存在父级高度塌陷问题。
缺点：
1. 不能做一列固定另一列自适应宽度，
2. 只能设置百分比宽度做到两列宽度自适应；
3. 由于浏览器对代码中的空格渲染站位问题，需要代码不能有换行空格，或者通过其他方式处理如：font-size:0;letter-spacing: -.35em;

## 两列布局之定位布局
> 两列定位布局通常为父级设置相对定位，一列设置绝对定位固定宽度或者百分比宽度，然后按照父级靠左或者靠右定位，然后另一列设置间距来空出定位列的位置

**示例：**
查看案例：[https://codepen.io/qwguo88/full/BajZwWR](https://codepen.io/qwguo88/pen/BajZwWR)

<iframe height="500" style="width: 100%;" scrolling="no" title="two-columns-layout-position" src="https://codepen.io/qwguo88/embed/BajZwWR?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/BajZwWR'>two-columns-layout-position</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

定位布局的优点：
1. 它可是使比较低的列能够自适应比较高的列的高度（前提需要低的列绝对定位然后设置100%高度或者上下位置为0）
缺点：
1. 当非定位列不够高还是撑不开父元素高度，导致后边的内容上移也就是父级高度塌陷。

## 两列布局之多列布局columns属性
> 严格意义上讲columns使用来实现文字类似于报纸一样的排版效果，但是他也能用来布局页面

**示例：**
查看案例：[https://codepen.io/qwguo88/full/RwrgyMz](https://codepen.io/qwguo88/pen/RwrgyMz)

<iframe height="300" style="width: 100%;" scrolling="no" title="two-columns-layout-columns" src="https://codepen.io/qwguo88/embed/RwrgyMz?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/RwrgyMz'>two-columns-layout-columns</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

从上边案例可以看出，columns更适合多列等宽布局，并且是那种层次不齐的瀑布流效果。它并不能为单独列设置单一宽度


## 两列布局之弹性盒模型布局
> css3中的`flex`弹性盒模型布局的出现弥补了上边所介绍的布局的不足之处

**示例：**
查看案例：[https://codepen.io/qwguo88/full/KKVqQwy](https://codepen.io/qwguo88/pen/KKVqQwy)

<iframe height="500" style="width: 100%;" scrolling="no" title="two-columns-layout-flex" src="https://codepen.io/qwguo88/embed/KKVqQwy?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/KKVqQwy'>two-columns-layout-flex</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## 两列布局之网格布局
>css3中的`grid`网格布局是更加灵活的一种布局模式，用网格布局实现两列布局更加方便

**示例：**
查看案例：[https://codepen.io/qwguo88/full/ZEQyjzN](https://codepen.io/qwguo88/pen/ZEQyjzN)

<iframe height="300" style="width: 100%;" scrolling="no" title="two-columns-layout-grid" src="https://codepen.io/qwguo88/embed/ZEQyjzN?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ZEQyjzN'>two-columns-layout-grid</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

上边案例可以看到，使用网格布局实现两列布局最简单的方法就是直接给父级设置样式就能实现，而且还可以轻松实现高度统一。通过使用网格可以用多种方式实现两列布局


