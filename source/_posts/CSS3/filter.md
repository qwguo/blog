---
title: css3中的filter滤镜使用
date: 2020-02-23 18:54:41
categories: [web前端]
tags: [CSS3, 前端]
description: "在css3中使用filter滤镜设置图像的灰度，褐色，亮度，对比度等效果"
---

# css3中的filter滤镜使用

> `filter` 滤镜，借鉴了Photoshop的滤镜效果，在ps中主要用来设置图层图片的模糊，颜色的高亮，对比度等效果，在css中滤镜通常用于调整图像，背景和边框的渲染和效果。

| 函数名      | 取值              | 作用              |
| ----------- | ----------------- | ----------------- |
| grayscale   | 值为0-1之间的小数, 或0%-100%百分数 | 灰度              |
| sepia       | 值为0-1之间的小数, 或0%-100%百分数 | 褐色              |
| saturate    | 值为num           | 饱和度            |
| hue-rotate  | 值为angle         | 色相旋转          |
| invert      | 反色              | 值为0-1之间的小数 |
| opacity     | 值为0-1之间的小数 | 透明度            |
| brightness  | 值为0-1之间的小数 | 亮度              |
| contrast    | 值为num           | 对比度            |
| blur        | 值为length        | 模糊              |
| drop-shadow | 和投影取值相同    | 阴影              |

<!-- more -->
**兼容性：**

![image](filter.png)
[查看兼容性详情](https://caniuse.com/#search=filter)

## 1、grayscale 灰度模式

> 用来设置图像或者元素的灰度模式，也就是去掉所有颜色以灰色显示元素

**基本语法：** `filter:grayscale(val)`

`val` ：值为100%则完全转为灰度图像，值为0%图像无变化。值在0%到100%之间，则是效果的线性乘子。若未设置，值默认是0，同时也可以去0-1之间小数；

``` css
/* 100%灰度 */
filter:grayscale(1);
/* 50%灰度 */
filter:grayscale(0.5);
/* 0%灰度 */
filter:grayscale(0);
```

**案例:** [Demo](https://codepen.io/qwguo88/pen/MWYQyqK)
**颜色灰度：**
<iframe height="500" style="width: 100%;" scrolling="no" title="filter-color-grayscale" src="https://codepen.io/qwguo88/embed/MWYQyqK?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/MWYQyqK'>filter-color-grayscale</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
**图片灰度：**
<iframe height="500" style="width: 100%;" scrolling="no" title="filter-img-grayscale" src="https://codepen.io/qwguo88/embed/yLNVdBp?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/yLNVdBp'>filter-img-grayscale</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## 2、sepia 褐色

> 将图片或者元素以褐色的形式显示，也就是复古效果。

**基本语法：** `filter:sepia(val)`

`val` ：值定义转换的比例。值为100%则完全是深褐色的，值为0%图像无变化。值在0%到100%之间，则是效果的线性乘子。若未设置，值默认是0，同时也可以去0-1之间小数；

``` css
/* 0%深褐色 */
filter:sepia(0);
/* 10%深褐色 */
filter:sepia(10%);
/* 100%深褐色 */
filter:sepia(100%);
```

**案例：** [Demo](https://codepen.io/qwguo88/pen/Jjdbzyg)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-sepia" src="https://codepen.io/qwguo88/embed/Jjdbzyg?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/Jjdbzyg'>filter-sepia</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## 3、saturate 饱和度

> 用于设置图像的饱和度。

**基本语法：** `filter: saturate(val)`

`val` ：取值为0%则是完全不饱和，值为100%则图像无变化。其他值，则是效果的线性乘子。超过100%的值是允许的，则有更高的饱和度。 若值未设置，值默认是1，同时也可以去0-1之间小数。

``` css
/* 0%深褐色 */
filter:saturate(0);
/* 10%深褐色 */
filter:saturate(10%);
/* 100%深褐色 */
filter:saturate(100%);
```
**案例：** [Demo](https://codepen.io/qwguo88/pen/qBdqvPW)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-saturate" src="https://codepen.io/qwguo88/embed/qBdqvPW?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/qBdqvPW'>filter-saturate</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### 4、hue-rotate 色相旋转

> 给图像应用色相旋转。

**基本语法：** `filter: hue-rotate(angle)`

`angle` ：用于设定图像被调整的色环角度值。值为0deg，则图像无变化。若值未设置，默认值是0deg。该值虽然没有最大值，超过360deg的值相当于又绕一圈。

```css
/* 无变化 */
filter: hue-rotate(0deg);
/* 色相旋转30度 */
filter: hue-rotate(30deg);
/* 色相旋转360度 */
filter: hue-rotate(360deg);
```
**案例：** [Demo](https://codepen.io/qwguo88/pen/XWbNLmx)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-hue-rotate" src="https://codepen.io/qwguo88/embed/XWbNLmx?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/XWbNLmx'>filter-hue-rotate</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### 5、invert 反色

> 给图片进行反转取色显示

**基本语法：** `filter: invert(val)`

`val` ：取值为100%表示完全反转。值为0%则图像无变化。值在0%和100%之间。 若值未设置，值默认是0。，同时也可以去0-1之间小数。

```css
/* 无变化 */
filter: invert(0);
/* 取反30% */
filter: invert(30%);
/* or */
filter: invert(.3);
```

**案例：** [Demo](https://codepen.io/qwguo88/pen/PoqbMWe)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-invert" src="https://codepen.io/qwguo88/embed/PoqbMWe?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/PoqbMWe'>filter-invert</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 6、opacity 透明度

> 给图像或者元素设置透明度，该函数与已有的opacity属性很相似，不同之处在于通过filter，一些浏览器为了提升性能会提供硬件加速。

**基本语法：** `filter: opacity(val)`

`val` ： 取值为0%则是完全透明，值为100%则图像无变化。值在0%和100%之间。 若值未设置，值默认是1。

```css
/* 无变化 */
filter: opacity(0);
/* 透明度30% */
filter: opacity(30%);
/* or */
filter: opacity(.3);
```

**案例：** [Demo](https://codepen.io/qwguo88/pen/MWwbNPa)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-opacity" src="https://codepen.io/qwguo88/embed/MWwbNPa?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/MWwbNPa'>filter-opacity</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### 7、brightness 亮度

> 用于设置图像的亮度，给图片应用一种线性乘法，使其看起来更亮或更暗。

**基本语法：** `filter: brightness(val)`

`val` ： 取值如果是0%，图像会全黑。取值是100%，则图像无变化。其他的值对应线性乘数效果。值超过100%也是可以的，图像会比原来更亮。如果没有设定值，默认是1。

```css
/* 无变化 */
filter: brightness(0);
/* 图像变暗70% */
filter: brightness(30%);
/* or */
filter: brightness(.3);
```
**案例：** [Demo](https://codepen.io/qwguo88/pen/xxGRveL)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-brightness" src="https://codepen.io/qwguo88/embed/xxGRveL?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/xxGRveL'>filter-brightness</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 8、contrast 对比度

> 用于设置图像的对比度，

**基本语法：** `filter: contrast(val)`

`val` ： 值是0%的话，图像会全灰。值是100%，图像不变。值可以超过100%，意味着会运用更低的对比。若没有设置值，默认是1。

```css
/* 无变化 */
filter: contrast(0);
/* 图像对比度变暗70% */
filter: contrast(30%);
/* or */
filter: contrast(.3);
```
**案例：** [Demo](https://codepen.io/qwguo88/pen/OJVbKKG)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-contrast" src="https://codepen.io/qwguo88/embed/OJVbKKG?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/OJVbKKG'>filter-contrast</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### 9、blur 模糊度

> 用于设置图像的高斯模糊度

**基本语法：** `filter: blur(radius)`

`radius` ：设定高斯函数的标准差，或者是屏幕上以多少像素融在一起，所以值越大越模糊；如果没有设定值，则默认是0；这个参数可设置css长度值（em、px、rem、pt）等，但不接受百分比值。

```css
/* 无变化 */
filter: blur(0);
/* 设置图像高斯模糊2个像素融合 */
filter: blur(2px);
/* 设置图像高斯模糊5个像素融合 */
filter: blur(5px);
```
**案例：** [Demo](https://codepen.io/qwguo88/pen/OJVbKKG)

<iframe height="500" style="width: 100%;" scrolling="no" title="filter-contrast" src="https://codepen.io/qwguo88/embed/OJVbKKG?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/OJVbKKG'>filter-contrast</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### 10、drop-shadow 投影

> 设置图像或元素的投影效果，他和box-shadow效果一样

**基本语法：** `filter: drop-shadow()`
