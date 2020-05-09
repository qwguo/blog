---
title: flex布局
date: 2019-12-16 18:34:00
categories:
  - [CSS, CSS3]
tags: [CSS3, flex, 弹性布局]
poster: poster.jpg
summary: ['在flex出现之前我们做页面都是使用的左右浮动，inline-block，表格等布局方式来实现页面的各种布局，在这些写法中由于浏览器的兼容问题还需要写很多的hack来解决兼容问题。','2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地在页面中使用弹性flex布局，Flex 布局也将成为未来布局的首选方案。']
---

# Flex

>  flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。我们可以把任何容器转换成(flex container)成为**弹性容器**，它的所有子元素就变为(flex item)称为**弹性项目成员**

我们可以通过给任意容器元素添加 `display: flex;` *块级弹性容器* 和 `display:inline-flex;`*行内块级弹性容器*；

***注意，设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。***


### 弹性容器的属性：

#### flex-direction

> `flex-direction`：用于设置容器中的子项目排列方向，定义主轴的方向（正反方向）

<!--more-->


**语法：**
`flex-direction: row | row-reverse | column | column-reverse;`

- `row`：默认值，容器的主轴被定义为与文本方向相同，主轴起点和主轴终点与内容方向相同。一般：主轴为水平方向，起点在左端。
- `row-reverse`：表现和row的方向相同，但是置换了主轴起点和主轴终点。一般：主轴为水平方向，起点改为在右端。
- `column`：主轴为垂直方向，起点从上端乡下开始排列。
- `column-reverse`：主轴和column一样垂直方向，起点改为相反方向，从下到上排列。

**兼容性：**
![image](flex-direction-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=flex-direction)

查看案例：[https://codepen.io/qwguo88/full/abbqyVY](https://codepen.io/qwguo88/full/abbqyVY)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex-direction" src="https://codepen.io/qwguo88/embed/abbqyVY?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/abbqyVY'>flex-direction</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


#### flex-wrap

> `flex-wrap`：属性定义容器中的子项目如果在一条轴线上排不下时如何显示。默认情况下，项目都排在一条线（又称"轴线"）上。

**语法：**
`flex-wrap: nowrap | wrap | wrap-reverse`

- `nowrap`：默认值，不换行，容器中的子项目强制在一条轴上显示，容器内的子元素会溢出显示。
- `wrap`：强制换行，当子项目排列超出容器后会自动换到下一行（*默认*）或者下一列，取决于flex-direction的设置。
- `wrap-reverse`：和 wrap 的行为一样强制换行，但是排列会从下开始往上排列换行，或者从右开始向左排列换行。

**兼容性：**
![image](flex-wrap-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=flex-wrap)

查看案例：[https://codepen.io/qwguo88/full/dyydwLr](https://codepen.io/qwguo88/full/dyydwLr)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex-wrap" src="https://codepen.io/qwguo88/embed/dyydwLr?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/dyydwLr'>flex-wrap</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### flex-flow

> `flex-flow`：属性是`flex-direction` 和 `flow-wrap` 的简写形式，字面上理解就是flex容器中字项目的流向。

**语法：**
`flex-flow: <'flex-direction'> || <'flex-wrap'>;`

**兼容性：**
![image](flex-flow-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=flex-flow)

查看案：[https://codepen.io/qwguo88/full/KKKQYBN](https://codepen.io/qwguo88/full/KKKQYBN)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex-flow" src="https://codepen.io/qwguo88/embed/KKKQYBN?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/KKKQYBN'>flex-flow</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### justify-content

> `justify-content`：属性定义容器中的子项目在主轴线上的对齐方式

**语法：**
`justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;`

- `flex-start`：默认值、弹性容器的子项目将以行或列的起始位置对齐；
- `flex-end`：弹性容器的子项目将以行或列的结束位置对齐；
- `center`：弹性容器的子项目将居中对齐；
- `space-between`：弹性容器的子项目将平局分布对齐，每个子项之间间距相同，首尾子项将贴近容器边缘；
- `space-around`：弹性容器的子项目将平局分布对齐，首尾子项将不贴近容器边缘，每个子项的左右或上下边距相同；
- `space-evenly`：弹性容器的子项目将平局分布对齐，首尾子项将不贴近容器边缘，首尾子项贴近容器的间距和子项之间的间距相同；

**兼容性：**
![image](justify-content-caniuse.png)
[查看兼容性详情](https://caniuse.com/#feat=mdn-css_properties_justify-content_flex_context)

查看案：[https://codepen.io/qwguo88/full/LYYQoop](https://codepen.io/qwguo88/full/LYYQoop)

<iframe height="500" style="width: 100%;" scrolling="no" title="justify-content" src="https://codepen.io/qwguo88/embed/LYYQoop?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/LYYQoop'>justify-content</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### align-items

> `align-items`：属性设置弹性容器中的子项目在侧轴（纵轴 | 副轴）方向上的对齐方式

**语法：**
`align-items: flex-start | flex-end | center | baseline | stretch;`

- `flex-start`：弹性容器的子项目以侧轴的起始位置对齐
- `flex-end`：弹性容器的子项目以侧轴的结束位置对齐
- `center`：弹性容器的子项目以侧轴的中点对齐
- `baseline`：弹性容器的子项目以项目的第一行文字的基线对齐
- `stretch`：默认值，弹性容器的子项目如果不设置高度或者高度是auto，那么子项目将占满整个容器的高度

**兼容性：**
![image](flex-align-items-caniuse.png)
[查看兼容性详情](https://caniuse.com/#feat=mdn-css_properties_align-items_flex_context)

查看案：[https://codepen.io/qwguo88/full/NWWMjPG](https://codepen.io/qwguo88/full/NWWMjPG)

<iframe height="500" style="width: 100%;" scrolling="no" title="align-items" src="https://codepen.io/qwguo88/embed/NWWMjPG?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/NWWMjPG'>align-items</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### align-content

> `align-content`：属性定义了弹性容器中多根轴线的对齐方式。如果项目只有一根轴线或（设置了flex-wrap-nowrap属性的弹性容器）将不起作用，也可以理解为子项目整体的对齐方式，会把子项目划分成一个组。

**语法：**
`align-content: flex-start | flex-end | center | space-between | space-around | stretch;`

- `flex-start`：弹性容器的子项目以主轴的起始位置对齐
- `flex-end`：弹性容器的子项目以主轴的结束位置对齐
- `center`：弹性容器的子项目以主轴的中点对齐
- `space-between`：弹性容器的子项目以容器的两端对齐
- `space-around`：弹性容器的子项目平均分配容器的空间子项目间上下（或左右）间距相同
- `stretch`：默认值，弹性容器的子项目如果不设置高度或者高度是auto，那么子项目将拉伸平均占满整个容器的高度活宽度

**兼容性：**
![image](flex-align-content-caniuse.png)
[查看兼容性详情](https://caniuse.com/#feat=mdn-css_properties_align-content_flex_context)

查看案：[https://codepen.io/qwguo88/full/ExxLoGv](https://codepen.io/qwguo88/full/ExxLoGv)

<iframe height="500" style="width: 100%;" scrolling="no" title="align-centent" src="https://codepen.io/qwguo88/embed/ExxLoGv?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ExxLoGv'>align-centent</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 弹性容器中的子项目的属性：

#### flex-grow

> `flex-grow`：属性设置弹性容器的子项是否拉伸填充容器的剩余空间

**语法：**
`flex-grow: number | 0`

- `0`：初始化值，表示不进行拉伸处理。
- `number`：只能取正整数。当容器中的子项目填充不满容器的时候，每个子项目将按照自身设置的`flew-grow:number`值来放大填充满剩余的空间。
    - 假设容器的宽度为400px, 子项1的占用的基础空间(flex-basis)为50px，子项2占用的基础空间是70px，子项3占用基础空间是100px，剩余空间为 400-50-70-100 = 180px。 其中子项1的flex-grow: 0(未设置默认为0)， 子项2flex-grow: 2，子项3flex-grow: 1，剩余空间分成3份，子项2占2份(120px)，子项3占1份(60px)。所以 子项1真实的占用空间为: 50+0 = 50px， 子项2真实的占用空间为: 70+120 = 190px， 子项3真实的占用空间为: 100+60 = 160px。

**兼容性：**
![image](flex-grow-caniuse.png)
[查看兼容详情](https://caniuse.com/#search=flex-grow)

查看案：[https://codepen.io/qwguo88/full/xxxjJZo](https://codepen.io/qwguo88/full/xxxjJZo)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex-grow" src="https://codepen.io/qwguo88/embed/xxxjJZo?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/xxxjJZo'>flex-grow</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### flex-shrink

> `flex-shrink`：属性设置弹性容器的子项目在所有子项宽度之和大于容器总宽度是是否收缩。

**语法：**
`flew-shrink: number | 1`

- `1`：初始化值，表示每个子项目都进行缩放。
- `number`： 取值==0==表示不进行缩放，取值其他正整数表示进行缩放。具体计算规则是：


```html
<div class="box">
  <div class="sub-1">11111</div>
  <div class="sub-2">2</div>
  <div class="sub-3">3</div>
</div>
```
```less
.box{
  display: flex;
  width: 500px;
  height: 200px;
  .sub-1{
    width: 100px;
    flex-shrink: 1;
  }
  .sub-2{
    width: 200px;
    flex-shrink: 2;
  }
  .sub-3{
    width: 300px;
    flex-shrink: 3;
  }
}
```

> 先计算总权重TW = 100px * 1(flex-shrink) + 200px *2(flex-shrink) + 300px *3(flex-shrink) = 1400px 也就是每个div的宽度乘以flex-shrink系数的总和。

> 每个div收缩的空间为：div的宽度 - div的宽度 * flex-shrink系数/ 总权重TW * 需要收缩的总宽度（在我们的例子中是600px - 500px = 100px）


**兼容性：**
![image](flex-shrink-caniuse.png)
[查看兼容详情](https://caniuse.com/#search=flex-shrink)

查看案：[https://codepen.io/qwguo88/full/vYYrEmp](https://codepen.io/qwguo88/full/vYYrEmp)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex-shrink" src="https://codepen.io/qwguo88/embed/vYYrEmp?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/vYYrEmp'>flex-shrink</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### flex-basis

> `flex-basis`：定义弹性容器的子项目在主轴方向上占容器的空间大小。*它要比`width`或者`height`权重高*


**语法：**
`flex-basis: <length> | auto;`
- `length`：用于设置元素的宽度或者高度。
- `auto`：默认值，表示元素按照内容来分配宽度或高度。


**兼容性：**
![image](flex-basis-caniuse.png)
[查看兼容详情](https://caniuse.com/#search=flex-basis)

查看案：[https://codepen.io/qwguo88/full/NWWzemV](https://codepen.io/qwguo88/full/NWWzemV)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex-basis" src="https://codepen.io/qwguo88/embed/NWWzemV?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/NWWzemV'>flex-basis</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### flex

> `flex`：属性规定了弹性元素如何伸长或缩短以适应flex容器中的可用空间，它是`flex-basis`、`flex-grow`、`flex-shrink`三个属性的简写形式。可以指定1个，2个或3个值

**语法：**
`flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ];`

- `none`：元素会根据自身宽高来设置尺寸。它是完全非弹性的：既不会缩短，也不会伸长来适应 flex 容器。相当于将属性设置为`flex: 0 0 auto`。
- **单值语法：** 值必须为以下其中之一：
    -  一个无单位数(<number>): 它会被当作<flex-grow>的值。
    -  一个有效的宽度(width)值: 它会被当作 <flex-basis>的值。
    -  关键字none，auto或initial.
- **双值语法：** 第一个值必须为一个无单位数，并且它会被当作 <flex-grow> 的值。第二个值必须为以下之一：
    - 一个无单位数：它会被当作 <flex-shrink> 的值。
    - 一个有效的宽度值: 它会被当作 <flex-basis> 的值。
- **三值语法：**
    - 第一个值必须为一个无单位数，并且它会被当作 <flex-grow> 的值。
    - 第二个值必须为一个无单位数，并且它会被当作  <flex-shrink> 的值。
    - 第三个值必须为一个有效的宽度值， 并且它会被当作 <flex-basis> 的值。

- `initial`：元素会根据自身宽高设置尺寸。它会缩短自身以适应 flex 容器，但不会伸长并吸收 flex 容器中的额外自由空间来适应 flex 容器 。相当于将属性设置为`flex: 0 1 auto`。
- `auto`：元素会根据自身的宽度与高度来确定尺寸，但是会伸长并吸收 flex 容器中额外的自由空间，也会缩短自身来适应 flex 容器。这相当于将属性设置为 `flex: 1 1 auto`.



**兼容性：**
![image](flex-caniuse.png)
[查看兼容详情](https://caniuse.com/#search=flex)

查看案：[https://codepen.io/qwguo88/full/JjjBpWO](https://codepen.io/qwguo88/full/JjjBpWO)

<iframe height="500" style="width: 100%;" scrolling="no" title="flex" src="https://codepen.io/qwguo88/embed/JjjBpWO?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/JjjBpWO'>flex</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### order

> `order`：属性定义弹性容器的子项目在显示中的排列顺序，数值越小越靠前，默认值为0。如果两个子项目的 ` order ` 值相同那么就按照他们的代码出现结构排序。

**语法：**
`order: integer;`

- `integer`：取整数，可以取负数、0、正数。


**兼容性：**
![image](flex-order-caniuse.png)
[查看兼容详情](https://caniuse.com/#feat=mdn-css_properties_order)

查看案：[https://codepen.io/qwguo88/full/rNNrbxb](https://codepen.io/qwguo88/full/rNNrbxb)

<iframe height="500" style="width: 100%;" scrolling="no" title="order" src="https://codepen.io/qwguo88/embed/rNNrbxb?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/rNNrbxb'>order</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### align-self

> `align-self`：属性可以对弹性容器中的单个子项目进行设置对齐方式，并且覆盖容器中设置的`align-items`值。

**语法：**
`align-self: auto | flex-start | flex-end | center | baseline | stretch | inherit`

- `auto`：按照父元素的 `align-items` 值对齐，如果该元素没有父元素的话，就设置为 stretch。
- `flex-start`：按照弹性容器的主轴的开始位置对齐。
- `flex-end`：按照弹性容器的主轴结束位置对齐。
- `center`：按照弹性容器的主轴中间对齐。
- `baseline`：按照弹性容器中项目的第一行文字的基线对齐。
- `stretch`：按照弹性容器的宽或者高进行拉伸。
- `inherit`：继承父容器的 `align-items`对齐方式。


**兼容性：**
![image](flex-align-self-caniuse.png)
[查看兼容详情](https://caniuse.com/#feat=mdn-css_properties_align-self_flex_context)

查看案：[https://codepen.io/qwguo88/full/GRRXxQg](https://codepen.io/qwguo88/full/GRRXxQg)

<iframe height="500" style="width: 100%;" scrolling="no" title="align-self" src="https://codepen.io/qwguo88/embed/GRRXxQg?height=300&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/GRRXxQg'>align-self</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 相关网站

#### flex在线演示，和在线代码生成网址：

1. 在线演示：[https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/](https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/)
2. 一个有趣的游戏学习flex布局：[http://flexboxfroggy.com/](http://flexboxfroggy.com/)
3. flex布局在线代码生成：[https://the-echoplex.net/flexyboxes/](https://the-echoplex.net/flexyboxes/)

#### flex相关文章：

1. 阮一峰老师的flex详解：[http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
2. 张鑫旭老师flex详解：[https://www.zhangxinxu.com/wordpress/2018/10/display-flex-css3-css/](https://www.zhangxinxu.com/wordpress/2018/10/display-flex-css3-css/)
