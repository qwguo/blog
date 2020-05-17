---
title: 通过css3的scrollbar功能自定义浏览器的滚动条效果
summary:
  - '在css3之前我们如果想要自定义浏览器默认的滚动条样式是无法实现的，一般的做法是通过html+css+js来实现自定义滚动条，或者网站找现成的插件，做法都比较麻烦，IE虽然可以自定义滚动条，但是也只是改一些颜色而已不能做到绚丽的效果。'
  - 'css3实现了自定义滚动条效果，可以让我们设置滚动条宽度，颜色，圆角等效果，遗憾的是只有webkit内核的浏览器支持。'
p: CSS3/scrollbar
date: 2020-04-16 18:43:42
categories:
tags:
poster: poster.jpg
drafts: false
---

# CSS滚动条选择器
> 应为自定义滚动条目前只有webkit内核的浏览器支持和FireFox支持部分功能，所以我们下边的属性都应用了`::-webkit-`前缀

![image](scrollbar.png)

这里我通过案例递增添加属性，我们可以通过下边的案例来理解各个属性指哪个位置

**案例：**[https://codepen.io/qwguo88/full/bGVmmdQ](https://codepen.io/qwguo88/full/bGVmmdQ)

<iframe height="600" style="width: 100%;" scrolling="no" title="scrollbar" src="https://codepen.io/qwguo88/embed/bGVmmdQ?height=600&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/bGVmmdQ'>scrollbar</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## scrollbar
> 设置滚动条整体部分样式，可以设置基本的css属性，包括，宽、高、背景颜色、边线等，这里需要注意的是设置高点的时候只对横线滚动条生效宽度为容器宽度，设置宽度的时候对纵向滚动条生效高度为容器高度。

**语法：**
```css
::-webkit-scrollbar { styles }
selector::-webkit-scrollbar{ styles }
```


## scrollbar-button
> 设置滚动条两端的按钮样式；
**注意：**
1. 横向滚动条为左右按钮，可以设置宽度，当设置高度是，并不生效高度为总的滚动条高度；
2. 纵向滚动条为上下按钮，可以设置高度，当设置宽度时也并不生效，它的宽度是总体滚动条的宽度；
3. 如果想设置按钮和滚动条有间距并不会生效，可以设置边框再通过边框颜色透明方式实现外间距，但是这里背景绘制区域需要设置为`content-box`。

## scrollbar-track
> 设置滚动条外层轨道的样式，也就是两个按钮之间的区域。


## scrollbar-track-piece
> 设置滚动条内层滚动槽的样式。

## scrollbar-thumb
> 设置滚动滑块的样式，也就是我们平时拖动的滚动条区域。

## scrollbar-corner
> 设置横向和纵向滚动条相交的区域的边角样式。


## scrollbar-resize
> 设置滚动条右下角拖动块的样式，这个设置我测试并不生效，如果需要显示拖动区域需要给元素设置`resize:both`
