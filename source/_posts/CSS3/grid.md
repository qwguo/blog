---
title: Grid网格布局
date: 2019-07-20 23:15:52
tags: [CSS3]
---

> ### css3中的grid布局学习

Grid是CSS3中网格布局系统，也是最强大的布局系统。它是一个二维系统，这意味着它可以处理列和行，不像flexbox主要是一维系统。 您可以使用网格布局，通过将CSS规则应用于父元素（成为网格容器）和该元素的子元素（它们成为网格项）。

<!--more-->

> ### 应用在父元素和子元素的Grid规则

作用在grid容器上 | 作用在grid子项上
---|---
display  | grid-column-start
[grid-template-rows](#grid-template-rows-grid-template-columns) | grid-column-end
[grid-template-columns](#grid-template-rows-grid-template-columns) | grid-row-start
[grid-template-areas](#grid-template-areas) | grid-row-end
[grid-template](#grid-template) | grid-column
grid-column-gap | grid-row
grid-row-gap | grid-area
grid-gap | justify-self
justify-items | align-self
align-items | place-self
place-items |
justify-content |
align-content |
place-content |
grid-auto-columns |
grid-auto-rows |
grid-auto-flow |
grid |

如果想让一个块级元素成为网格布局，那么给该元素添加`display:grid`；

如果要想让一个内联元素成为网格布局，那么给钙元素添加`display:inline-grid`。


> #### 把元素变成Grid元素

代码如下：
```html
  <style type="text/css">
    .grid-box{
      display: grid;
    }
  </style>
  <div class="grid-box"></div>
```
上边的代码中，div.grid-box元素现在就是一个网格布局元素。


> #### grid-template-rows, grid-template-columns


<!-- <iframe height="420" style="width: 100%;" scrolling="no" title="grid-template-rows" src="//codepen.io/qwguo88/embed/voOdMK/?height=420&theme-id=30742&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/voOdMK/'>grid-template-rows</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe> -->

从上面可以看到，通过设置`grid-template-rows: 50px auto 1fr;`把Grid元素中的子元素划分成了三行，并且给每一行分别设置高度值。

具体语法是：`<track-size> ... | <line-name> <track-size> ...;`;

1. `track-size1`：划分子元素的尺寸。可以是长度值，百分比值，以及fr单位（网格剩余空间比例单位）。
2. `[line-name]`：对划分网格分隔线进行命名，语法是使用[]包裹我们自定义的命名，可以是中文，如果是两个值情况下用空格分开。

> #### grid-template-areas

通过字面理解area是区域的意思，这个属性的作用是给父元素（网格元素）划分区域。


<!-- <iframe height="420" style="width: 100%;" scrolling="no" title="grid-template-areas" src="//codepen.io/qwguo88/embed/ZgBXoE/?height=420&theme-id=30742&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ZgBXoE/'>grid-template-areas</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe> -->

<pre>
网格元素{
  grid-template-areas:
    "<grid-area-name> | . | none | ..."
    "...";
}
子元素{
  grid-area: grid-area-name;
}
</pre>

1. `grid-area-name`：表示网格区域的名称，可以是中文，可以是英文
2. `.`：表示空的单元格
3. `none`： 表示没有定义网格区域

我们给定了网格区域名称以后，可以通过给子元素（网格单元格）设置`grid-area:a`进行设置，属性名不用使用引号。

**注意：**如果我们给网格区域命了名，但是没有给网格线命名，则会自动根据网格区域名称生成网格线名称，规则是区域名称后面加-start和-end。例如，某网格区域名称是`'a'`，则左侧column线名称就是`'a-start'`，左侧column线名称就是`'a-end'`。我们的网格区域一定要形成规整的矩形区域，什么L形，凹的或凸的形状都是不支持的，会认为是无效的属性值。


> #### grid-template

`grid-template`是`grid-template-row`、`grid-template-column`、`grid-template-area`的简写形式1

