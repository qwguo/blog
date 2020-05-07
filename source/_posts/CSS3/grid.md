---
title: Grid网格布局
date: 2019-07-20 23:15:52
categories:
  - [CSS, CSS3]
tags: [CSS3, grid, 网格布局]
poster: poster.png
summary:
  - 'Grid是CSS3中网格布局系统，也是CSS3中最强大的布局系统。它是一个二维布局系统，这意味着它可以处理列和行，不像flex弹性布局主要是一维系统，他像表格一样可以让我们控制行或者例对齐，可以控制子元素跨行或者跨列，但是他比表格更加灵活，它的子元素可以单独定位就像CSS定位元素一样，同时还可以重叠单元格。'
  - '您可以使用网格布局，通过将CSS规则应用于父元素（成为网格容器）和该元素的子元素（它们成为网格项）'
---

# css3中的grid布局学习

## 基本概念
> 我们这里用我们最熟悉城市街道来理解这些概念。

1. 网格容器

  > 一个元素应用网格布局属性后就变成了网格容器，它是由一组水平线和垂直线交叉构成，就如果我们所在的地区有小区和各个路构成。

2. 网格线

  > 使用Grid布局在显式网格中定义轨道的同时会创建网格线。网格线有水平和垂网格线。也就是东西路段和南北路段的马路。正常情况下`n`行会有`n+1`根横向网格线，`m`列有`m+1`根纵向网格线。比如`田`字就是就好像是一个三条水平线和三条垂直线构成的网格元素。


3. 网格轨道

  > 网格轨道 是两条网格线之间的空间。

4. 行

  > 即两个水平网格线之间的空间，也就是水平轨道，就好比我们面朝北边东西方向横向排列的楼房称为行。

5. 列

  > 即两个垂直网格线之间的空间，也就是垂直轨道，也就是南北方向排列的楼房

6. 单元格

  > 由水平线和垂直线交叉构成的每个区域称为单元格，网络单元格是CSS网格中的最小单元。也就是说东西和南北方向的路交叉后划分出来的土地区域

7. 区域

  > 网格区域是网格中由一个或者多个网格单元格组成的一个矩形区域。本质上，网格区域一定是矩形的。例如，不可能创建T形或L形的网格区域。

8. 网格间距

  > 是网格轨道之间的间距，这里一般值得是列和列，行和行之间的间距

9. 什么是网格项目

  > 在网格中的所有子元素统称为网格项目，这里只包括子元素，不包括子元素的后代元素。也就是每个区块中的建筑物我们成为网格项


## 应用于父级规则

### display

> 通过给元素设置：`display:grid | inline-grid`，可以让一个元素变成网格布局元素

**语法：**

```css
  display: grid | inline-grid;
```
**参数说明：**
1. `grid`：表示把元素定义为块级网格元素，单独占一行;
2. `inline-grid`：表示把元素定义为行内块级网格元素，可以和其他块级元素在同一行。



### grid-template-rows 、grid-template-columns


> rows 用来规定网格容器的每一行的高度和横向网格线的名称，columns用来规定网格容器的每一列的宽度和纵向网格线的名称

**他们的语法相同，所以一起说明**

**语法：**
`grid-template-rows: <track-size> ... | <line-name> <track-size> ... ;`
`grid-template-columns: <track-size> ... | <line-name> <track-size> ... ;`

**语法示例：**

```css
/* Keyword value */
grid-template-rows: 100px 1fr;
grid-template-rows: [linename] 100px;
grid-template-rows: [linename1] 100px [linename2 linename3];
grid-template-rows: minmax(100px, 1fr);
grid-template-rows: fit-content(40%);
grid-template-rows: repeat(3, 200px);

/* <track-list> values */
grid-template-rows: none;
grid-template-rows: 200px repeat(auto-fill, 100px) 300px;
grid-template-rows: minmax(100px, max-content) repeat(auto-fill, 200px) 20%;
grid-template-rows: [linename1] 100px [linename2] repeat(auto-fit, [linename3 linename4] 300px) 100px;
grid-template-rows: [linename1 linename2] 100px repeat(auto-fit, [linename1] 300px) [linename3];

/* Global values */
grid-template-rows: inherit;
grid-template-rows: initial;
grid-template-rows: unset;
```

**案例说明：** [https://codepen.io/qwguo88/full/voOdMK](https://codepen.io/qwguo88/full/voOdMK)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-template-rows or grid-template-columns" src="https://codepen.io/qwguo88/embed/voOdMK?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/voOdMK'>grid-template-rows or grid-template-columns</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

**我们通过上边案例分析一下取值详情：**

#### none
> 这个关键字表示不明确的网格。所有的行和其大小都将由`grid-auto-rows` 属性隐式的指定。

![image](row_column_auto.png)

如上图所示，是借助谷歌开发者工具查看，在我们只设置`grid-template-rows: auto;`和`grid-template-columns: auto;`属性的情况下，网格项横向100%铺满网格容器，然后纵向排列分部，高度按照项目个数平均分配网格容器总高度。

#### length
> 非负值的长度大小。列（宽度）或者行（高度）值可以是用css绝对单位如：`px`、`em`、`rem`等。

![image](row_column_length.png)

图上所示，我们设置了`grid-template-rows: 100px 50px 200px;`和`grid-template-columns: 150px 300px 500px;`表示把网格容器划分成三行三列的网格，当划分列的宽度总合宽于容器宽度并不会自动换到下一行而且溢出，相应的划分的行总和也一样。

#### percentage
> 非负值且相对于网格容器的 <百分比>`%`。 如果网格容器的尺寸大小依赖网格轨道的大小（比如 inline-grid ），则百分比值将被视为auto。

![image](row_column_percentage.png)
我们在开发的过程中更多的是使用百分百来设置网格划分项，上图是通过设置%+auto的值来划分`grid-template-rows: 30% 40% auto;`和`grid-template-columns: 40% auto 50%;`表示把网格容器划分成三行三列，第一行占网格容器的高度的`30%`，第二行占`40%`,剩下的高度分配给`auto`也就是`100%-(40%+30%)=30%`，同样的列也是如此计算

#### flex
> 非负值，用单位 `fr`（fraction 的缩写，意思是"分数"）。表示网格按照给定数字来等分行或者列，当我们划分的行或列单位都用`fr`的时候表示把网格划分出指定等分

![image](row_column_fr_1.png)

上图中我们给的值为：`grid-template-rows: 1fr 2fr 3fr;`和`grid-template-columns: 2fr 5fr 1fr;`表示三行三列的网格，其中把行分成5等份第一行占`1/5`第二行占`2/5`第三行占`3/5`，把列分成8等份第一列占`2/8`第二列占`5/8`第三列占`1/8`

![image](row_column_fr_2.png)

上图中我们给的值为：`grid-template-rows: 1fr 200px;`和`grid-template-columns: auto 200px 10% 2fr 3fr;`表示两行五列的网格，其中第二行是200像素，第一行占总高度减去`200px`后的1份，在这个例子中就是`300(总高度)-200=100`,`1fr`就是`100px`高度；
列的分配是：第二列是固定的`200px`，第三列是占总宽度的`10%`也就是`82px`，在同时有`fr`和`auto`单位的行或列中计算比较特殊，这里的第一列是`auto`表示取这一列中最多的`内容`宽度这里就是`child-6`字符的站位宽，第四列和第五列分别是`2fr`和`2fr`表示把剩余的宽度分成5份，一个占剩余宽度的`2/5`一个占剩余宽度的`3/5`，在这个例子中表示`(820-'child-6字符宽(53)'-200-(820/10))/5 = 97`剩余宽度的每一份就是97，第四列就是`97*2=194`，第五列就是`97*3=291`

#### min-content、max-content
> 一个用来表示以网格项的最大的最小内容来占据网格轨道的关键字。
> 一个用来表示以网格项的最大的内容来占据网格轨道的关键字。

chrome | firefox
--- | ---
![image](row_column_minmax-content_chrome.png) | ![image](row_column_minmax-content_firefox.png)

上图中案例使用：`grid-template-rows: 1fr 100px;`和`grid-template-columns: repeat(2, min-content max-content  minmax(min-content, max-content));`表示两行六列的网格；其中行不用说，这里主要说列，列使用了`repeat`函数来重复；
- 第一列和第四列使用的是关键字`min-content`表示此列的宽度应用此列最宽的单元格中最小内容宽度，怎么理解呢就是这一列中能够自动换行后的最宽文字或者单词，从图上可以看出，Chrome浏览器第一列中在字符`child-`后面进行了换行然后取的`child-`这个字符的站位宽度，Firefox浏览器没有在`child-`后换行。但是在第四列中因为有中文所以两个浏览器都执行了换行，但是换行的位置有所不同。
- 第二列和第五列使用的是关键字`max-content`表示此列的宽度应用此列最宽的单元格最大内容宽度，意思是内容尽量不自定换行然后取最大内容字符的宽度作为此列的宽度。
- 第三列和第六列使用的是minmax()函数定义列宽，里边最大最小值也是应用了`min-content`和`max-content`这里去的是最大内容宽度


#### repeat()
> 此方法可以让我们用一种简单快捷的方式划分比较多而且有规律的网格单元格，比如说我们要划分一个1行12列网格，如果我们划分的列宽很有规律，我没必要写12遍

  - **此方法语法：** `repeat( [ <positive-integer> | auto-fill | auto-fit ] , <track-list> )`

  - **参数说明**

    - `positive-integer`：表示要重复的`track-list`规则次数
    - `auto-fit`：用于不确定列的情况下，当`track-list`规则指定的所有子元素宽度之和不大于网格容器总宽度时平均拉升子元素填充剩余空间
    - `auto-fill`：用于不确定列的情况下，当`track-list`规则指定的所有子元素宽度之和不大于网格容器总宽度时子元素不拉升填充剩余空间

  - **图例：**
  ![image](row_column_repeat_length.png)
  上图案例中我们给的值为：`grid-template-rows: repeat(2, 100px);`和`grid-template-columns: repeat(2, 100px 1fr auto);`表示两行六列的网格，其中两行的高度都是`100px`，这里使用`repeat()`函数表示重复定义，第一个参数表示重复次数，第二个参数表示要重复的值，多个值用空格隔开，案例表示划分2行每行都是100像素的行，从图上可以看出两行高度加起来不大于网格容器高度所以空出来留给网格中多出来的子项目；其中六列的宽度分别是第一列和第四列宽度为`100px`第三列和第六列宽度为该列中最长字符占位宽度，第二列和第五列宽度为`(820-(100px*2)-('child-3'字符宽+'child-6'字符宽)/2)`，第二个参数为多个值得时候表示按照循序分配第一个参数的次数。

  ![image](row_column_repeat_auto-fit.png)
  上图案例中取值为：`grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));` 我们使用`auto-fit`关键字不固定列，同时每一列宽度最小值为`100px`最大值为`1fr`，因为子项取最小值总合加起来不大于容器宽度，所以每个子项都拉升填满整个容器。

  ![image](row_column_repeat_auto-fill.png)
  上图案例中取值为：`grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));` 我们使用`auto-fill`关键字不固定列，同时每一列宽度最小值为`100px`最大值为`1fr`，每个子项取最小值综合加起来不大于容器宽度，这个时候继续按照最小值分隔列，直到剩余宽度不大于`100px`，然后所以每个子项再平均分隔剩余空间。

#### minmax(min, max)
>此方法表示取值一个范围，最小值和最大值，大于等于min值，并且小于等于max值。如果max值小于min值，则该值会被视为min值。最大值可以设置为网格轨道系数值<flex> ，但最小值则不行。

![image](row_column_minmax.png)

上图案例中我们使用`minmax()`函数定义值：`grid-template-rows: minmax(100px, 1fr) 150px;`和`grid-template-columns: repeat(2, 100px 1fr minmax(100px, auto));`表示两行六列的网格，其中行中因为有固定值,所以第二行高度`150px`，然后第一行中的`minmax()`方法再根据剩余空间计算取值，如果剩余高度大于最小值`100px`那么就取`1fr`，如果剩余高度小于最小值`100px`那么高度取`100px`，当此方法第二个参数是固定值时，如果剩余高度大于这个固定值，那么高度取最大值得固定值。

#### fit-content()

> 字面理解是`fit`适合后面跟内容，就是适合内容宽度，这里我测试的是不超过给定值得宽度（当给定宽度不大于内容最小宽度时会超过），同时固定值分配宽度后的剩余宽度小于给定值时候自动缩小宽度但是不能小于换行后的最宽项的最小内容宽度。

Chrome | Firefox
--- | ---
![image](row_column_fit-content_chrome.png) | ![image](row_column_fit-content_firefox.png)

上图案例中我们使用`fit-content()`函数定义列值：`grid-template-columns: fit-content(10px) fit-content(70px) 50% 35%;`表示第一列按内容计算宽度最大值为`10px`但是截图中第一列的换行后的最小宽度`child-`字符已经超过`10px`所以宽度取值为`child-`字符宽度，第二列给定按内容计算宽度最大值为`70px`这个时候此列取值为`70px`并且此列的所有项都能在`70px`内换行，第三列宽度是固定的总宽度的50%：`820px*0.5=410px`，第四列宽度是总宽度的30%：`820px*0.35=287px`；

#### [line-name]
> 定义垂直和水平线的名称，同时可以使用多个名字来命名一条分隔线多个名字之间用空格分开，给分隔线命名的字符不许用`[]`括起来

```css
grid-template-rows: [row-one-start] 30% [row-one-end row-two-start] 40% [row-two-end row-three-start] auto [row-three-end];
grid-template-columns: repeat(3, 33% [col-line]);
```

### grid-template-areas

通过字面理解area是区域的意思，这个属性的作用是给网格布局容器划分区域。

**语法：**`grid-template-areas:  "<grid-area-name> | . | none | ..." "...";`

**取值说明：**
1. `grid-area-name`：给区域定义名称，这里主要按照行来定义用双引号或者单元号括起来代表一行，一行中多列可以定义相同的名称(代表同一个区块)或不同名称（代表不同区块），名称之间用空格分开，第二行
2. `.`：表示空网格区块
3. `none`：表示没有定义网格区块名称

**案例说明：** [https://codepen.io/qwguo88/full/ZgBXoE](https://codepen.io/qwguo88/full/ZgBXoE)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-template-areas" src="https://codepen.io/qwguo88/embed/ZgBXoE?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true" loading="lazy">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ZgBXoE'>grid-template-areas</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

在这里我们借助Firefox工具查看我们定义的区块划分：

![image](grid-template-areas_1.png)

在上图中我们定义了：`grid-template-areas: 'head head head' '. body-content body-right' 'foot foot none'`，从图中我们可以看到第一行划分了一个区块，区块名`head`占据三列，第二行划分了三个区块左边的是用`.`划分的空区块，中间的区块名：`body-content`，右边的区块名：`body-right`，第三行划分了两个区块，左边的区块名：`foot`占据两列，右边的区块名：`none`没有名称占据一列
我们给定了网格区域名称以后，可以通过给子元素（网格单元格）设置`grid-area:head`进行设置一个单元格所占空间，属性名不用使用引号。

![image](grid-template-areas_2.png)

上图是我们通过给子元素设置区块名称得到的效果，子元素设置区块名我们将在后面进行介绍。

<!--
**注意：**如果我们给网格区域命了名，但是没有给网格线命名，则会自动根据网格区域名称生成网格线名称，规则是区域名称后面加-start和-end。例如，某网格区域名称是`'a'`，则左侧column线名称就是`'a-start'`，左侧column线名称就是`'a-end'`。我们的网格区域一定要形成规整的矩形区域，什么L形，凹的或凸的形状都是不支持的，会认为是无效的属性值。 -->


### grid-template

`grid-template`是`grid-template-row`、`grid-template-column`、`grid-template-area`的简写形式

**语法：**

```css
/* 值为关键词 */
grid-template: none;

/* 为 grid-template-rows / grid-template-columns */
grid-template: 100px 1fr / 50px 1fr;
grid-template: auto 1fr / auto 1fr auto;
grid-template: [linename] 100px / [columnname1] 30% [columnname2] 70%;
grid-template: fit-content(100px) / fit-content(40%);

/* 为 grid-template-areas grid-template-rows / grid-template-column */
grid-template: "a a a"
               "b b b";
grid-template: "a a a" 20%
               "b b b" auto;
grid-template: [header-top] "a a a"     [header-bottom]
               [main-top] "b b b" 1fr [main-bottom]
                            / auto 1fr auto;

/* 为全局值 */
grid-template: inherit;
grid-template: initial;
grid-template: unset;
```

**案例说明：** [https://codepen.io/qwguo88/full/ZgBXoE](https://codepen.io/qwguo88/full/ZgBXoE)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-template" src="https://codepen.io/qwguo88/embed/pMwBpv?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/pMwBpv'>grid-template</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

从案例中可以看到，`grid-template`定义行或者列要简单很多 行和列之间用`/`分开，前面的部分是定义的`grid-template-rows`后面的部分是定义的`grid-template-columns`，还可以只定义区块，然后网格会根据给定的规则等比例划网格。

这里我们介绍一下引用区块划分的代码，效果图如下

![image](grid-template-area_3.png)

上图引用的代码是：`grid-template: "a a c" "b b c";`只给网格容器划分区块，此代码给网格容器划分了两行三列，第一行的第一列和第二列合并成一个区块，第二行的第一列和第二列合并成一个区块，第一行的第三列和第二行的第三列竖向合并一个区块。然后通过给子项目应用区块。

![image](grid-template-area_4.png)

上图引用的代码是：`grid-template: "a a a" 40px "b c c" 40px "b c c" 40px / 1fr 1fr 1fr;`代码说明`/`前面的属于行划分，第一行划分成一个区块`a`高度为`40px`，第二行划分成两个区块`b`和`c`高度也是`40px`，第三行划分成两个区块`b`和`c`高度也是`40px`，第二行和第三行的第一列区块属于一个所以上下合并，第二行和第三行的第二列第三列区块一样整体合并。`/`后面的列规定按照整体宽度划分为三份每列的宽度是1/3。

### grid-column-gap、grid-row-gap

> 此属性分别定义列和列之间的间距、行和行之间的间距

Chrome | Firefox
--- | ---
![image](grid-row-gap_1_chrome.png) | ![image](grid-row-gap_1_firefox.png)

图上我们定义了：三行三列的网格，`grid-row-gap: 10px;`给行与行之间定义`10px`的间距，图中我们借助Firefox可以看虚斜线的区域属于行与行之间的间距区域。

Chrome | Firefox
--- | ---
![image](grid-column-gap_1_chrome.png) | ![image](grid-column-gap_1_firefox.png)

图上我们定义了：三行三列的网格，`grid-column-gap: 10px;`给列与列之间定义`10px`的间距，图中我们借助Firefox可以看虚斜线的区域属于列与列之间的间距区域。

### grid-gap
> 他是`grid-column-gap`和`grid-row-gap`的简写形式，如果提供一个值，那么应用于行和列的间距，如果提供两个值需要用空格分开，空格前边的是行间距，空格后边的是列间距
![image](grid-gap_1_firefox.png)

上图我们给的定义是：`grid-gap: 20px 10px`;表示网格的行间距是`20px`列间距是`10px`;

### grid-auto-rows or grid-auto-columns

> 此属性定义了，子项目的个数超出了我们定义的行和列的情况下，多出的子项目的宽度高度的尺寸大小；

![image](grid-auto-rows_firefox.png)

上图我们给定的规则是：`grid-template-rows: 20px 30px 40px;`和`grid-auto-rows: 80px;`，我们给网格元素划分了三行，每一行都给定了高度，网格中有5个子元素。从图上可以看出前三个子深色虚线的行是我们规定好的高度，中间实线一下的浅色点虚线是应用的`grid-auto-rows`定义的`80px`高度。

Chrome | Firefox
--- | ---
![image](grid-auto-columns_chrome.png) | ![image](grid-auto-columns_firefox.png)

要解释`grid-auto-columns`属性需要用区域定义属性，上图效果中我们定义了`grid-template: 'a b c d e f g' / 90px 90px 90px;`一行7个区域(隐式定义了7类)的网格，但是我们只定义了前三列`90px`的宽度，并且占据了前三个区域a、b、c，剩下的两个子元素和多余的区域宽度将会应用我们定义的`grid-auto-columns: 50px;`；这是的chrome和Firefox表现一直，宽度都是50像素。


### grid-auto-flow
> 控制子元素的排列顺序，默认子元素排序是按照自左到右自上而下一行一行排列。

**语法：**

```css
/* Keyword values */
grid-auto-flow: row;
grid-auto-flow: column;
grid-auto-flow: dense;
grid-auto-flow: row dense;
grid-auto-flow: column dense;

/* Global values */
grid-auto-flow: inherit;
grid-auto-flow: initial;
grid-auto-flow: unset;
```
**取值说明：**
1. `row`：按行顺序排列，默认值，子元素出现的顺序先填充行，第一行填充完毕，在填充第二行；
2. `column`：按照列顺序排列，子元素出现的顺序先填充列，第一列填充完毕，在填充第二列
3. `dense`：该关键字使用一种“稠密”堆积算法，如果后面出现了稍小的元素，则会试图去填充网格中前面留下的空白。这样做会填上稍大元素留下的空白，但同时也可能导致原来出现的次序被打乱。
4. `row dense`：和`dense`值基本相同
5. `column dense`：这个是纵向“稠密””堆积算法；


**案例说明：** [https://codepen.io/qwguo88/full/OJyzQLj](https://codepen.io/qwguo88/full/OJyzQLj)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-auto-flow" src="https://codepen.io/qwguo88/embed/OJyzQLj?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/OJyzQLj'>grid-auto-flow</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 对齐方式

> 基本布局分析完毕，我们来说一下网格容器中的对齐方式，网格中对齐方式有：


#### align-items

> 是指网格项目元素在单元格中的垂直呈现方式，是垂直拉伸显示，还是上中下对齐

chrome | Firefox
--- | ---
![image](align-items_chrome.png) | ![image](align-items_firefox.png)

我们还是可以借助上面的截图图片再结合下边的案例来理解各个取值的区别，图中虚线的位置代表的是网格的单元格，色块代表的是网格项目

**案例演示：** [https://codepen.io/qwguo88/full/jObYKzd](https://codepen.io/qwguo88/full/jObYKzd)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-align-items" src="https://codepen.io/qwguo88/embed/jObYKzd?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/jObYKzd'>grid-align-items</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### justify-items

> 是指网格项目元素在单元格中的水平呈现方式，是水平拉伸显示，还是左中右对齐

chrome | Firefox
--- | ---
![image](justify-items_chrome.png) | ![image](justify-items_firefox.png)

我们可以借助上面的截图图片再结合下边的案例来理解各个取值的区别，图中虚线的位置代表的是网格的单元格，色块代表的是网格项目

**案例演示：** [https://codepen.io/qwguo88/full/JjYMvMz](https://codepen.io/qwguo88/full/JjYMvMz)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-justify-items" src="https://codepen.io/qwguo88/embed/JjYMvMz?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/JjYMvMz'>grid-justify-items</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

通过上边的案例我们发现，一般使用 `stretch`、`start`、`end`、`center`这几个值，`stretch`是默认值


#### place-items

> 此属性是 `align-items`和`justify-items`的缩写形式

**语法**

```css
/* 单个值 */
place-items: center;
/* 两个值 */
place-items: align-items justify-items;
```

**说明：**
如果是单个值的情况下，将应用于垂直和水平对齐，如果是两个值的话需要用空格分开，前边的表示垂直对齐，后边的表示水平对齐。

chrome | Firefox
--- | ---
![image](place-items_chrome.png) | ![image](place-items_firefox.png)

我们还是可以借助上面的截图图片再结合下边的案例来理解各个取值的区别，图中虚线的位置代表的是网格的单元格，色块代表的是网格项目

**案例演示：** [https://codepen.io/qwguo88/full/ExVoRJy](https://codepen.io/qwguo88/full/ExVoRJy)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-place-items" src="https://codepen.io/qwguo88/embed/ExVoRJy?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ExVoRJy'>grid-place-items</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

#### align-content

> 指的是把网格布局中的所以子项成一个整体，然后让整体在网格容器中垂直对齐，这个需要两行以上才能看到效果。

center | start | end
---|---|---
![image](align-content_center.png) | ![image](align-content_start.png) | ![image](align-content_end.png)

我们还是结合上图Firefox截图理解各个支的表现形式。在图上我们可以看到，取值为`start`的时候网格项整体会靠上显示，取值为`center`的时候网格项整体的上边会填充`gap`使其整体垂直居中显示，取值为`end`的时候所取的`gap`会更大，使网格项整体靠下对齐。他可取的值还有很多，我们可以结合下边的实例来查看效果。

**案例展示：**[https://codepen.io/qwguo88/full/mdeXWxy](https://codepen.io/qwguo88/full/mdeXWxy)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-align-content" src="https://codepen.io/qwguo88/embed/mdeXWxy?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/mdeXWxy'>grid-align-content</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


#### justify-content

> 指的是把网格布局中的所以子项成一个整体，然后让整体在网格容器中水平对齐，这个需要两列以上才能看到效果。

center | start | end
---|---|---
![image](justify-content_center.png) | ![image](justify-content_start.png) | ![image](justify-content_end.png)

我们还是结合上图Firefox截图理解各个支的表现形式。在图上我们可以看到，取值为`start`的时候网格项整体会靠左显示，取值为`center`的时候网格项整体的左边会填充`gap`使其整体水平居中显示，取值为`end`的时候所取的`gap`会更大，使网格项整体靠右对齐。他可取的值还有很多，我们可以结合下边的实例来查看效果。

**案例展示：**[https://codepen.io/qwguo88/full/ExVopyW](https://codepen.io/qwguo88/full/ExVopyW)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-justify-content" src="https://codepen.io/qwguo88/embed/ExVopyW?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ExVopyW'>grid-justify-content</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


#### place-content

> 此属性是 `align-content`和`justify-content`的缩写形式

**语法**

```css
/* 单个值 */
place-content: center;
/* 两个值 */
place-content: align-content justify-content;
```

**说明：**
如果是单个值的情况下，将应用于垂直和水平对齐，如果是两个值的话需要用空格分开，前边的表示垂直对齐，后边的表示水平对齐。

start | center | end
--- | ---
![image](place-content_start.png) | ![image](place-content_center.png) | ![image](place-content_end.png)

我们还是可以借助上面的截图图片再结合下边的案例来理解各个取值的区别

**案例演示：** [https://codepen.io/qwguo88/full/JjYpvex](https://codepen.io/qwguo88/full/JjYpvex)

<iframe height="500" style="width: 100%;" scrolling="no" title="grid-place-content" src="https://codepen.io/qwguo88/embed/JjYpvex?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/JjYpvex'>grid-place-content</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### grid


最后推荐一个学习网格布局的地址：[https://grid.layoutit.com/](https://grid.layoutit.com/)
