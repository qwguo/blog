---
title: css3中用来设置元素的过度效果属性：transition
date: 2019-12-21 14:35:01
tags:
---

# transition过度属性

> `transition`：用于设置DOM元素在不同状态之间切换的时候应用不同的过度效果，以前如果要想实现一个非生硬的状态切换需要写很多的js来实现，现在使用`transition`变可以轻松的实现。

### 1、transition-property：

> `property`：表示属性的意思，这里用来设置元素要过度的css属性名。

**基本语法：**
`transition: none | all | property;`
- `none`：表示没有任何过度效果。
- `all`：初始值，表示所有的能过度属性都有过度效果。
- `property`：指定一个或多个属性名称执行过度效果，多个css属性名之间用逗号分隔开。
<!-- more -->

**例如：**
```css
    transition-property: width;
    transition-property: window, height, background-color, opacity;
    transition-property: all;
```

**兼容性：**

![image](transition-property-caniuse.png)

[查看兼容性详情](https://caniuse.com/#search=transition-property)


查看案例[Demo](https://codepen.io/qwguo88/pen/YzzBPYM)

能够支持过度的css属性[查看1](http://leaverou.github.io/animatable/)，[查看2](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_animated_properties)

### 2、transition-duration

> `transition-duration`：表示过渡动画在多长时间内执行完毕。值以秒（s）或毫秒（ms）为单位不接受负值。可以指定多个值，每个值之间用逗号分开并且分别应用到 `transition-property` 指定的对应属性上。

**基本语法：**
`transition-duration: time;`

- `time`：指定动画执行时长。

**例如：**
```css
    transition-duration: 10s;
    transition-duration: .5s, 10ms, .9ms, 0.5s, 10.05s; //如果是小数点左边只有一个0的话，前边的 0可以省略。
```

**兼容性：**

![image](transition-duration-caniuse.png)

[查看兼容性详情](https://caniuse.com/#search=transition-duration)


查看案例[Demo](https://codepen.io/qwguo88/pen/LYYazMY)




### 3、transition-timing-function

> `transition-timing-function`：指定一个函数，定义属性值怎么变化。缓动函数 Timing functions 定义属性如何计算。多数 timing functions 由四点定义一个 bezier 曲线。也可以从 Easing Functions Cheat Sheet 选择缓动效果。

**基本语法：**
`transition-timing-function: ease | ease-in | ease-out | ease-in-out | linear | cubic-bezier(<number>, <number>, <number>, <number>) | step-start | set-end | steps(<integer>[, <step-position>]?) | inherit`

- `ease`：慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。
- `ease-in`：慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。
- `ease-out`：慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。
- `ease-in-out`：慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。
- `linear`：以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。
- `steps(4, end)`：四次运动到结束执行过度效果。
- `cubic-bezier(x1, y1, x2, y2)`：以贝塞尔函数算法执行过度效果。生成贝塞尔曲线网站：[website1](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Tools/Cubic_Bezier_Generator)、[website2](https://cubic-bezier.com/)、[website](https://easings.net/)

![image](transition-timing-function-caniuse.png)

[查看兼容性详情](https://caniuse.com/#search=transition-timing-function)

查看案例[Demo](https://codepen.io/qwguo88/pen/zYYXypo)

### 4、transition-delay

> `transition-delay`：延迟指定时间后执行过度效果。值以秒（s）或毫秒（ms）为单位。取值为正时会延迟一段时间来响应过渡效果；取值为负时会导致过渡立即开始。可以指定多个延迟时间，每个延迟用逗号分开，分别作用于你所指定的相符合的css属性`transition-property`;

**基本语法：**
`transition: time | inherit | initial | unset`

- `time`：指定的时间，格式：10s | 10ms | 0.5s  (.5s) | -10ms | -5s (-.5s)
- `inherit`：

![image](transition-delay-caniuse.png)

[查看兼容性详情](https://caniuse.com/#search=transition-delay)

查看案例[Demo](https://codepen.io/qwguo88/pen/qBBGOBG)

### 5、transition

> `transition`：它是`transition-property`、`transition-duration`、`transition-timin-function`、`transition-delay` 的缩写形式，能够更方面的设置过渡效果，一般在开发中使用这种方式写过渡效果。


**基本语法：**
`transition: property duration timing-function delay | none`

- `none`：没有过渡效果。

**基本写法：**
```css
    /* 两个值，属性名，过渡持续时间 */
    transition: margin-right 4s;
    /* 三个值，属性名，过渡持续时间，延迟开始过渡时间 */
    transition: margin-right 4s 1s;
    /* 三个值，属性名，过渡持续时间，过渡动画效果 */
    transition: margin-right 4s ease-in-out;
    /* 四个值，属性名，过渡持续时间，过渡动画效果，延迟开始过渡时间 */
    transition: margin-right 4s ease-in-out 1s;
    /* 可以同时写多个过渡属性，每个过渡之间用逗号分开 */
    transition: margin-right 4s, color 1s;
    /* 也可以使用all表示全部属性 */
    transition: all 0.5s ease-out;
    /* 其他 */
    transition: inherit;
    transition: initial;
    transition: unset;
```

![image](transition-caniuse.png)

[查看兼容性详情](https://caniuse.com/#search=transition)


