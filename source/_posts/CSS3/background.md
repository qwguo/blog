---
title: css中的背景介绍
summary:
  - '背景设置是css中常用的属性，它能用来给元素设置背景颜色和背景图片，css早起版本中背景设置的项目不是很多，只能简单的设置背景颜色，背景图片，背景图片的位置，平铺方式等；css3为背景属性增加了很多功能，包括：设置多张背景图片，背景的大小，渐变背景等更过功能，接下来我们将详细介绍背景的多有属性值和用法'
drafts: false
p: CSS3/background
date: 2020-07-14 10:22:36
categories:
tags:
poster:
---

# css中的背景详解

## background-color

> `background-color`用来设置元素的背景颜色

**语法：**

```css
/*css*/
/*关键字 透明*/
background-color: transparent;
/*关键字 inherit继承*/
background-color: inherit;
/* 颜色名称 */
background-color: red;

/* #16进制的颜色值 */
background-color: #bbff00;

/* RGB(红，绿，蓝) 0-255的色值范围值或者%百分比 */
background-color: rgb(255, 255, 128);

/*css3*/
/* RGBA(红，绿，蓝，透明度) 0-255的色值范围值或者%百分比，透明度0-1之间值 */
background-color: rgba(255, 255, 120, .5);

/* 通过颜色的饱和度：HSLA(Hue色调，Saturation饱和度，Lightness亮度，Alpha透明度)取值
1.色调：0(或360)表示红色，120表示绿色，240表示蓝色，也可取其他数值来指定颜色。取值为：0 - 360
2.饱和度和亮度：取值为：0.0% - 100.0%；
3.透明度：取值为：0-1之间
 */
background-color: hsl(50, 33%, 25%);
background-color: hsla(50, 33%, 25%, 0.75);

/*使用currentcolor关键字使用元素color的值*/
background-color: currentcolor;
```

此属性没有继承性，但是可以通过`inherit`关键字来继承父级的背景颜色。

**示例：** [https://codepen.io/qwguo88/full/BajEjLQ](https://codepen.io/qwguo88/full/BajEjLQ)


<iframe height="500" style="width: 100%;" scrolling="no" title="background-color" src="https://codepen.io/qwguo88/embed/BajEjLQ?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/BajEjLQ'>background-color</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## background-image

> `background-image`属性为元素定义一个或多个背景图片

**语法：**

```css
/*无背景图*/
background-color: none;
/*继承背景图*/
background-color: inherit;
/*单个背景*/
background-image: url('图片地址');
/*背景渐变形式*/
background-image: inear-gradient(to bottom, rgba(255,255,0,0.5), rgba(0,0,255,0.5));
/*多个背景*/
background-image: url("图片地址1"),
                  url('图片地址2'),
                  url(图片地址3);
/*多个渐变背景*/
background-image: linear-gradient(217deg, rgba(255,0,0,.8), rgba(255,0,0,0) 70.71%),
                  linear-gradient(127deg, rgba(0,255,0,.8), rgba(0,255,0,0) 70.71%),
                  linear-gradient(336deg, rgba(0,0,255,.8), rgba(0,0,255,0) 70.71%);
/*多个背景，背景图片和背景渐变混合使用*/
background-image: inear-gradient(to bottom, rgba(255,255,0,0.5), rgba(0,0,255,0.5)),
                  url("图片地址1"),
                  url('图片地址2'),
                  url(图片地址3);
```

背景图片中图片地址可以使用：单引号，双引号，不加引号；同时背景图片页可以实现继承通过设置`inherit`值来继承父级_**只能继承父级**_元素的背景图
多图片是css3新增的特性，多张图片需要使用逗号分隔开，多图片背景的显示顺序为先写的在最上层，最后写的在最底层。

背景图片属性基本浏览器都兼容，这里说一下多张图片背景和渐变背景兼容性：
**多背景：**
![image](background-image-multiple-caniuse.png)
**渐变背景：**
![image](background-image-gradients-caniuse.png)

**示例：** [https://codepen.io/qwguo88/full/xxZeRdV](https://codepen.io/qwguo88/full/xxZeRdV)

<iframe height="500" style="width: 100%;" scrolling="no" title="background-image" src="https://codepen.io/qwguo88/embed/xxZeRdV?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/xxZeRdV'>background-image</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## background-position

> `background-position`用于设置元素背景的位置信息，可以设置单个或者多个

**语法：**

```css
/*取值：位置关键字*/
background-position: left top;
/*or*/
background-position: left;

/*取值：百分比单位*/
background-position: 10% 20%;
/*or*/
background-position: 30%;

/*取值：具体单位值 px\pt\rem\em\cm等*/
background-position: 10px 1pt;
background-position: 1em 20rem;
/*or*/
background-position: 30px;

/*设置多个背景的位置*/
background-position: 20% 10%, 20px -10px, right bottom, left -10%;

/*通过给定位置关键字后边跟单位值实现相对于位置的偏移定位*/
background-position: bottom 10px right 20px;
background-position: right 3em bottom 10px;
background-position: bottom 10px right;
background-position: top right 10px;
```
**可取值列表：**
1. 关键字：可以取一个或者两个值，取单个值时，第二个值默认为center，所有的值都是以该元素作为定位依据
如果取单个值表示背景在元素的某个方向坐标的位置，当取值：`left | center | right`：表示设置横向坐标的位置，这个时候纵坐标为`center`；当取值：`top | bottom`：表示设置纵坐标位置，这个时候横向坐标为`center`；
如果取两个值表示同时设置横坐标和纵坐标的位置，第一个值表示横坐标，第二个值表示纵坐标。可取的值有：`left top` 、`left center` 、`left bottom` 、`right top` 、`right center` 、`right bottom` 、`center top` 、`center center` 、`center bottom`；
2. 百分比值：也是可以取一个值或者两个值，取单个值时表示设置横向坐标位置，这时第二个值默认为50%也就是纵坐标居中位置。
取值说明：当取正值得时候：`30% 20%`表示背景图片的左上角以元素的左上角为起点，向右平移元素的30%宽度，向下平移元素的20%高度；取负值：`-10% -30%`表示背景图片的左上角以元素的左上角为起点，向左平移元素的30%宽度，向上平移元素的20%高度(会到元素的外边不可见)
3. 具体单位值：也是可以取一个值或者两个值，取单个值时表示设置横向坐标位置，这时第二个值默认为50%也就是纵坐标居中位置。
像素值得取值是以实际的平移像素来左右或上下平移；
4. 设置多个背景的位置，当元素中设置了多张背景图片，我们也可以分别给每张背景图设置不同位置，并且用逗号分开每组值，每组值和多张背景图一一对应。如果给的的值少于背景图片，那么剩余的背景图片以默认位置显示。
5. 在设置的位置关键字后边跟具体单位值来设置背景先定位到设置的方向位置，然后按照这个位置再向左有，或者上下偏移给定的具体大小，这里的位置关键字只支持：`right`、`bottom`、`left`、`top`，不能给`center`设置偏移

前四个取值基本浏览器都兼容，第五个取值兼容性：
![image](background-position-offsets-caniuse.png)
[兼容详情](https://caniuse.com/#feat=css-background-offsets)

### background-position-x
> 单独定义横向坐标的位置

可取值：`left` | `right` | `center` | `length` | `percentage` | `left | right 偏移值`

### background-position-y

可取值：`top` | `bottom` | `center` | `length` | `percentage` | `top | bottom 偏移值`

一般情况下这两个属性没有`background-position`更方便，这两个属性的双值经过测试只有Firefox浏览器支持；


**示例：**[https://codepen.io/qwguo88/full/GRoLWGN](https://codepen.io/qwguo88/full/GRoLWGN)

<iframe height="500" style="width: 100%;" scrolling="no" title="background-position" src="https://codepen.io/qwguo88/embed/GRoLWGN?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/GRoLWGN'>background-position</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## background-repeat

> `background-repeat`用于设置元素背景是否重复平布显示

**语法：**
```css
/*repeat 默认值，表示横坐标，纵坐标重复平铺*/
background-repeat: repeat;

/*repeat-x 横坐标重复平铺*/
background-repeat: repeat-x;

/*repeat-y 纵坐标重复平铺*/
background-repeat: repeat-y;

/*no-repeat 不进行重复平铺*/
background-repeat: no-repeat;

/*space 自适应增加间距平铺*/
background-repeat: space;

/*round 当单张背景图片不大于容器会拉伸*/
background-repeat: round;

/*也可以使用两个值来分别设置横向坐标和纵向坐标*/
background-repeat: space repeat;
```
前四个值都是css2中有的属性，图片平铺是如果图片过大会益处容器裁切掉不显示，在css3中增加了这方面的处理，这里重点说一下新属性值得特性，这里说的是单个背景图：
1.`space`：平铺处理，但是条件是如果图片大于容器会裁切和`repeat`效果一样，当图片小于容器的时候会计算容器宽度上能放下几个背景图然后根据横向平铺会以第一次平铺的图片左边对齐容器的左边最后一次平铺的右边对齐容器右边然后中间的剩余部分平均间距平铺容器不进行拉伸，以增加间距的方式铺满容器，类似于布局中的平均分布。
2. `round`：当图片大于容器的时候会做缩小处理来适应容器宽高，当图片小于容器的时候进行计算，按照尽可能少放的原则进行缩放图片。
3. 还可以使用两个值来分别设置横向平铺和纵向平铺方式，第一个值表示横向平铺方式，第二个值表示纵向平铺方式。

**示例：**[https://codepen.io/qwguo88/full/LYGvzzx](https://codepen.io/qwguo88/full/LYGvzzx)

<iframe height="500" style="width: 100%;" scrolling="no" title="background-repeat" src="https://codepen.io/qwguo88/embed/LYGvzzx?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/LYGvzzx'>background-repeat</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

**关于双值得兼容性**：[查看兼容](https://caniuse.com/#feat=mdn-css_properties_background-repeat_2-value)
![image](background-repeat-tow-value-caniuse.png)

## background-attachment

> 用于设置当元素出现滚动条的情况下，背景图片的显示效果

**语法：**
```css
background-attachment: scroll;
background-attachment: fixed;
background-attachment: local;
background-attachment: scroll, fixed;
```

**示例：**


## background-size

> 用于设置背景图片的大小，可以对背景图片进行拉伸放大，等比例放大，强制缩小，等比例缩小等

**语法：**
```css
/*取值为关键字*/
/*等比例缩小或者放大背景图片，以容器的宽或高进行缩放，保证完全填充满容器，当图片大的时候会有一边益处*/
backgorund-size: cover;
/*等比例缩小或者放大背景图片，以容器的宽或高和图片的宽高比例进行缩放，保证宽或者高一项能填充满，另一边会有空白露出背景颜色*/
backgorund-size: contain;

```
