---
title: 通过css3的scrollbar功能自定义浏览器的滚动条效果
summary:
  - '在css3之前我们如果想要自定义浏览器默认的滚动条样式是无法实现的，一般的做法是通过html+css+js来实现自定义滚动条，或者网站找现成的插件，做法都比较麻烦，IE虽然可以自定义滚动条，但是也只是改一些颜色而已不能做到绚丽的效果。'
  - 'css3实现了自定义滚动条效果，可以让我们设置滚动条宽度，颜色，圆角等效果，遗憾的是只有webkit内核的浏览器支持。'
p: CSS3/scrollbar
date: 2020-04-16 18:43:42
categories: [CSS, CSS3]
tags:
  - CSS3
  - scrollbar
poster: poster.jpg
drafts: false
---

# webkit内核滚动条

> webkit内核的浏览器：chrome、safari、edge，因为自定义滚动条目前只有webkit内核的浏览器支持和FireFox支持部分功能，所以我们下边的属性都应用了`::-webkit-`前缀

![image](scrollbar.png)



## 滚动条属性选择器

这里我通过案例递增添加属性，我们可以通过下边的案例来理解各个属性指哪个位置

**案例：**[https://codepen.io/qwguo88/full/bGVmmdQ](https://codepen.io/qwguo88/full/bGVmmdQ)

<iframe height="600" style="width: 100%;" scrolling="no" title="scrollbar" src="https://codepen.io/qwguo88/embed/bGVmmdQ?height=600&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/bGVmmdQ'>scrollbar</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### scrollbar
> 设置滚动条整体部分样式，可以设置基本的css属性，包括，宽、高、背景颜色、边线等，这里需要注意的是设置高点的时候只对横线滚动条生效宽度为容器宽度，设置宽度的时候对纵向滚动条生效高度为容器高度。

**语法：**
```css
::-webkit-scrollbar { styles }
selector::-webkit-scrollbar{ styles }
```


### scrollbar-button
> 设置滚动条两端的按钮样式；

**语法：**
```css
::-webkit-scrollbar-button { styles }
selector::-webkit-scrollbar-button{ styles }
```

**注意：**
1. 横向滚动条为左右按钮，可以设置宽度，当设置高度是，并不生效高度为总的滚动条高度；
2. 纵向滚动条为上下按钮，可以设置高度，当设置宽度时也并不生效，它的宽度是总体滚动条的宽度；
3. 如果想设置按钮和滚动条有间距并不会生效，可以设置边框再通过边框颜色透明方式实现外间距，但是这里背景绘制区域需要设置为`content-box`。

### scrollbar-track
> 设置滚动条外层轨道的样式，也就是两个按钮之间的区域。

**语法：**
```css
::-webkit-scrollbar-track { styles }
selector::-webkit-scrollbar-track{ styles }
```

### scrollbar-track-piece
> 设置滚动条碎片的样式，也就是内层滚动槽的样式。

**语法：**
```css
::-webkit-scrollbar-track-piece { styles }
selector::-webkit-scrollbar-track-piece{ styles }
```

### scrollbar-thumb
> 设置滚动滑块的样式，也就是我们平时拖动的滚动条区域。

**语法：**
```css
::-webkit-scrollbar-thumb { styles }
selector::-webkit-scrollbar-thumb{ styles }
```

### scrollbar-corner
> 设置横向和纵向滚动条相交的区域的边角样式。

**语法：**
```css
::-webkit-scrollbar-corner { styles }
selector::-webkit-scrollbar-corner{ styles }
```

### scrollbar-resize
> 设置滚动条右下角拖动块的样式，这个设置我测试并不生效，如果需要显示拖动区域需要给元素设置`resize:both`

**语法：**
```css
::-webkit-scrollbar-resize { styles }
selector::-webkit-scrollbar-resize{ styles }
```

## 不同状态伪类

**案例：** [https://codepen.io/qwguo88/pen/QWjYwKd](https://codepen.io/qwguo88/pen/QWjYwKd)

<iframe height="500" style="width: 100%;" scrolling="no" title="scrollbar-pseudo" src="https://codepen.io/qwguo88/embed/QWjYwKd?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/QWjYwKd'>scrollbar-pseudo</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### :horizontal
> 水平伪类表示用来设置水平方向上的滚动条

**语法：**
```css
::-webkit-scrollbar:horizontal { styles }
selector::-webkit-scrollbar:horizontal{ styles }
```

### :vertical
> 垂直伪类表示用来设置垂直方向上的滚动条

**语法：**
```css
::-webkit-scrollbar:vertical { styles }
selector::-webkit-scrollbar:vertical{ styles }
```

### :decrement
> 适用于按钮和轨道碎片。表示递减的按钮或轨道碎片，例如可以使区域向上或者向右移动的区域和按钮

**语法：**
```css
::-webkit-scrollbar-(button | track):decrement { styles }
selector::-webkit-scrollbar-(button | track):decrement{ styles }
```
**这里说明一下：**`decrement`：应用到按钮设置的时候表示：横向按钮的左按钮，纵向按钮的上按钮，应用在轨道碎片上：横向表示碎片上半部分，纵向表示碎片左半部分


### :increment
>适用于按钮和轨道碎片。表示递增的按钮或轨道碎片，例如可以使区域向下或者向左移动的区域和按钮

**语法：**
```css
::-webkit-scrollbar-(button | track):increment { styles }
selector::-webkit-scrollbar-(button | track):increment{ styles }
```
**这里说明一下：**`increment`：应用到按钮设置的时候表示：横向按钮的右按钮，纵向按钮的下按钮，应用在轨道碎片上：横向表示碎片下半部分，纵向表示碎片右半部分

### :start
>适用于按钮和轨道碎片。表示对象（按钮轨道碎片）的前一个，他和上边的`:decrement`效果一样

### :end
>适用于按钮和轨道碎片。表示对象（按钮轨道碎片）的后一个，他和上边的`:increment`效果一样

### :double-button
>适用于按钮和轨道碎片。判断轨道结束的位置是否是一对按钮。也就是轨道碎片紧挨着一对在一起的按钮。~~没测试出来~~

### :single-button
>适用于按钮和轨道碎片。判断轨道结束的位置是否是一个按钮。也就是轨道碎片紧挨着一个单独的按钮。~~没测试出来~~

### :no-button
>表示轨道结束的位置没有按钮。~~没测试出来~~

### :corner-present
>表示滚动条的角落是否存在。~~测试的是会覆盖原有的样式，不知道什么意思~~

### :window-inactive
>适用于所有滚动条，表示包含滚动条的区域，焦点不在该窗口的时候。

```css
::-webkit-scrollbar-thumb:window-inactive{ styles }
selector::-webkit-scrollbar-thumb:window-inactive{ styles }
```

### :enabled
> 表示当前滚动条激活状态的样式。

### :disabled
> 表示滚动条禁用的样式。

### :hover
> 表示当鼠标方式去的滚动条各属性的样式。

### :active
> 表示鼠标按下时滚动条个属性的样式。



# FireFox浏览器

_案例需要使用`Firefox`浏览器查看效果_

**展示案例：** [https://codepen.io/qwguo88/full/zYvMzVJ](https://codepen.io/qwguo88/full/zYvMzVJ)

<iframe height="500" style="width: 100%;" scrolling="no" title="firefox-scrollbar" src="https://codepen.io/qwguo88/embed/zYvMzVJ?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/zYvMzVJ'>firefox-scrollbar</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



### scrollbar-width
> 用来设置滚动条出现时的厚度，横向滚动条设置高度，纵向滚动条设置的是高度。

**语法：**

```css
div{
  scrollbar-width: none | auto | thin;
}
```

**参数说明：**

1. `none`：不显示滚动条，但是dom元素任然可以正常滚动。
2. `auto`：默认值，表示走浏览器默认的样式。
3. `thin`：比默认的滚动条要小一些，横向的变低，纵向的变窄。


### scrollbar-color
> 用来设置滚动条的颜色

**语法：**
```css
div{
  scrollbar-color: thumbColor trackColor;
}
```
**参数说明：**

1. `thumbColor`：用来设置滚动条拖动的滑块颜色。
2. `trackColor`：用来设置滚动条轨道的颜色。


<!-- ## Internet Explorer(IE) -->

## 参考文章

1. [https://css-tricks.com/custom-scrollbars-in-webkit/](https://css-tricks.com/custom-scrollbars-in-webkit/)
2. [https://webkit.org/blog/363/styling-scrollbars/](https://webkit.org/blog/363/styling-scrollbars/)
3. [https://developer.mozilla.org/zh-CN/docs/Web/CSS/scrollbar-width](https://developer.mozilla.org/zh-CN/docs/Web/CSS/scrollbar-width)
