---
title: 在css3中有两个控制js事件行为的属性
date: 2019-12-17 20:40:16
tags: [CSS3]
description: "在css3中pointer-events，touch-action属性的详细使用"
---

# pointer-events


> 属性指定在什么情况下某个特定的图形元素可以成为鼠标事件的 `target`，这个属性主要应用在`SVG`元素上，这篇文章主要介绍的是应用在HTML的DOM元素上

**语法：**
`pointer-events: auto | none | inherit | initial | unset;`
<!-- more -->

- `auto`：自动表示使用DOM的默认行为。
- `none`：表示该元素不执行任何的js事件，包括其后代元素。但是，当其后代元素的此属性指定其他值时，鼠标事件可以指向后代元素，在这种情况下，鼠标事件将在捕获或冒泡阶段触发父元素的事件侦听器。
- `inherit`：表示继承父级的`pointer-events`的值。
- `initial`：初始化，和`auto`效果一样，表示执行元素的默认行为。
- `unset`：未定义，继承父级行为。

**兼容性：**
![image](pointer-events-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=pointer-events)

查看案例 [Demo](https://codepen.io/qwguo88/pen/MWWZWBj)

<iframe height="500" style="width: 100%;" scrolling="no" title="pointer-events" src="https://codepen.io/qwguo88/embed/MWWZWBj?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/MWWZWBj'>pointer-events</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

# touch-action

> touch-action是控制手势事件过滤的CSS属性，为开发人员提供了一种声明性机制，以有选择地禁用触摸滚动（在一个或两个轴上）或双击缩放，用于设置触摸屏用户如何操纵元素的区域

**语法：**
`touch-action: auto | none | [ [ pan-x | pan-left | pan-right ] || [ pan-y | pan-up | pan-down ] || pinch-zoom ] | manipulation;`

- `auto`：初始化值，表示根据浏览器决定当用户触控事件发生时执行默认行为。
- `none`：禁用touch事件，表示把元素上的触屏事件行为禁用，当用户在元素上触发触控行为时不进行任何操作。
- `pan-x`：表示只开启x轴的滑动行为，也就是左右滑动。
- `pan-left`：表示只开启元素向左滑动。


**兼容性：**
![image](touch-action-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=touch-action)

查看案例 [Demo](https://codepen.io/qwguo88/pen/YzzdyMd)

<iframe height="500" style="width: 100%;" scrolling="no" title="touch-action" src="https://codepen.io/qwguo88/embed/YzzdyMd?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/YzzdyMd'>touch-action</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
