---
title: columns多列属性2
date: 2019-12-13 16:02:03
tags: [CSS3]
---

## columns样式属性使用

> `columns`：用于设置元素的列宽和列数。它是`column-width`和`column-count`的简写属性。

**语法：**
 `columns: <'column-width'> || <'column-count'>;`

- `column-width`：用来设置列宽，取值`auto`和`像素值`，实际宽度可能会更宽或更窄以适合可用空间。
- `column-count`：用来设置元素内容被划分成几列，取值`auto`和`正整数`。如果取值和列的宽度都非`auto` ，则它仅指示允许的最大列数。

<!-- more -->

**兼容性：**

![image](columns-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=columns)

<iframe height="400" style="width: 100%;" scrolling="no" title="columns" src="https://codepen.io/qwguo88/embed/jOOagVB?height=400&theme-id=default&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/jOOagVB'>columns</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### column-width样式属性使用

> `column-width`：用于单独设置元素的列宽。

**语法：**
`column-width: auto | length;`


- `auto`：默认值，由浏览器决定宽度。
- `length`：单位值，用来这只每一列的宽度，当设置了`column-count`的时候优先把内容划分指定列数，宽度将自适应。

**兼容性：**

![image](column-width-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=column-width)

查看案例 [Demo](https://codepen.io/qwguo88/pen/poodMNw)


### column-count样式属性使用

> `column-count`：用于单独设置元素的列数。

**语法：**
`column-count: auto | number;`

- `auto`：默认值，由其他属性决定列数，比如 `column-width`，当`column-width`设置后会根据元素的总宽度和`column-width`的值来自动划分列数。
- `number`：划分元素以多少列来显示内容。

**兼容性：**

![image](column-count-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=column-width)

查看案例 [Demo](https://codepen.io/qwguo88/pen/poodMNw)


## column-gap样式属性使用

> `column-gap`：用于设置每一列之间的间隔

**语法：**
`column-gap: length | normal;`

- `length`：设置列间的间隔为指定的长度。
- `normal`：规定列间间隔为一个常规的间隔。W3C 建议的值是 1em。

**兼容性：**
![image](column-gap-caniuse.png)
[查看兼容性详情](https://caniuse.com/#feat=mdn-css_properties_column-gap_multicol_context)

查看案例 [Demo](https://codepen.io/qwguo88/pen/wvvpNmp)

## column-span样式属性使用

> `column-span`：用于设置元素中的子元素横向跨越的列数

**语法：**
`column-span: 1 | all;`

- `1`：设置元素横跨一列，默认值。
- `all`：设置元素横跨所有列，也就是单独占一行显示。

**兼容性：**
![image](column-span-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=column-span)

查看案例 [Demo](https://codepen.io/qwguo88/pen/GRRQZQW)


## column-rule样式属性使用

> `column-rule`：字面意思是设置多列规则，它是一个简写属性，用于整体设置所有 `column-rule-*` 的规则属性，规定列之间的==宽度==、==样式==和==颜色==规则，此属性类似于设置边框。

**语法：**
`column-rule: width | style | color`

- `width`：规定列之间的宽度规则，非简写：`column-rule-width`
    - 取值：`thin | medium | thick | length`;
        - `thin`：很细
        - `medium`：中等
        - `thick`：宽厚
        - `length`：自定义单位值

- `style`：规定列之间的样式规则，非简写：`column-rule-style`

    - 取值：`none | hidden | dotted | dashed | solid | double | groove | ridge | inset | outset`;
        - `none`：无规则
        - `hidden`：隐藏
        - `dotted`：点线效果
        - `dashed`：虚线效果
        - `solid`：实线效果
        - `double`：双线效果
        - `groove`：定义3D凹槽效果。该效果取决于宽度和颜色值。
        - `ridge`：定义3D凸起效果。该效果取决于宽度和颜色值。
        - `inset`：定义3D内显示效果。该效果取决于宽度和颜色值。
        - `outset`：定义3D外显示效果。该效果取决于宽度和颜色值。

- `color`：规定列之间的颜色规则，非简写：`column-rule-color`
    - 取值：`color` 颜色值;

**兼容性：**

![image](column-rule-caniuse.png)
[查看兼容性详情](https://caniuse.com/#search=column-rule)

查看案例 [Demo](https://codepen.io/qwguo88/pen/jOOZrwo)


## column-fill样式属性使用

> `column-fill`：规定如何填充列

**语法：**
`column-fill: balance | auto;`

- `balance`：对列进行协调。浏览器应对列长度的差异进行最小化处理。
- `auto`：按顺序对列进行填充，列长度会各有不同。

**兼容性：** 暂时无浏览器支持此属性，这里就不做讨论了。
