---
title: 关于css中文本的换行
summary:
  - '我们经常会遇到这样的问题，纯数字不能自动换行，连续输入的英文不能换行，或者篇文章中一行到达容器的末端以后没有在我们想要的位置进行换行，换行后会截断某个单词等问题，今天我们就说说css中关于换行的一些属性，和使用技巧'
drafts: false
p: CSS/textwrap
date: 2020-05-12 13:49:17
categories: [CSS]
tags: [CSS, word-break, word-wrap, 文本换行]
poster: poster.png
---

# 关于css中换行的一些学习

在介绍之前我们先来看一下浏览器默认情况下文本的超出容器的处理情况：
**案例展示：** [https://codepen.io/qwguo88/full/RZMQgB](https://codepen.io/qwguo88/full/RZMQgB)

<iframe height="500" style="width: 100%;" scrolling="no" title="textWrap_1.html" src="https://codepen.io/qwguo88/embed/RZMQgB?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/RZMQgB'>textWrap_1.html</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

通过上边的例子可以看出：

1. 连续的数字不会自动换行；
2. 连续的字母不会自动换行；
3. 英文文章中空格是由`&nbsp;`代码实现的空格不会换行；
4. 英文单词不会在中间换行，在单词中间到达容器边缘，此单词会另起一行显示。
5. 中文不会在文字和标点符号间换行，如果遇到标点符号到达容器的边缘，那么标点符号的前一个字会跟着折下来。
6. 容器中是连续的图片的话会自动换行显示。

> 我们在处理一些文本超过容器的时候换行的问题。一般我们处理换行的css属于主要用到：

## word-break
> 用于设置浏览器处理自动换行的方式

**语法：**

```css
word-break：normal | keep-all | break-all | break-word；
```
字面理解：`word`单词的意思，`break`打破、间断的意思。连起来得意思就好理解了：单词和文本之间的间断方式。

1. `normal`：默认值，表示使用浏览器的默认的换行规则，依照亚洲语言和非亚洲语言的文本规则，允许在句内换行。
2. `keep-all`：表示保持单词和句子的完成性，也就是说，英文中不会再单词内换行，中文不会在非标点符号内换行。

**查看实例：**[https://codepen.io/qwguo88/full/eYpKjqO](https://codepen.io/qwguo88/full/eYpKjqO)

<iframe height="500" style="width: 100%;" scrolling="no" title="word-break:keep-all" src="https://codepen.io/qwguo88/embed/eYpKjqO?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/eYpKjqO'>word-break:keep-all</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

> 个人测试：连续字母和数字不会自动折行
firefox 27.01版本的支持此属性。会使中文保持不换行，一直在一行显示。只有输入<br/>强直换行，对英文貌似不起作用。
Ie6-11，利用ie11的调试模式进行测试的，对中文只有遇到标点符号后，后边的文字才能自动折行。
Chrome、Safari，对此属性不起作用，文字和normal效果一样，文字到容器边缘自动换行，单不会在标点符号内换行。

3. `break-all`：(中断全部的) 该行为与亚洲语言的normal相同。也允许非亚洲语言文本行的任意字内断开。该值适合包含一些非亚洲文本的亚洲文本，比如使连续的英文字母间断行。

**查看实例：**[https://codepen.io/qwguo88/full/YzyvjJZ](https://codepen.io/qwguo88/full/YzyvjJZ)

<iframe height="500" style="width: 100%;" scrolling="no" title="word-break:break-all" src="https://codepen.io/qwguo88/embed/YzyvjJZ?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/YzyvjJZ'>word-break:break-all</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

4. `break-word`：属性和下边的 `overflow-wrap:break-word`表现差不多，唯一的区别在表格连续英文字符串换行上，前者可以让表格单元格中的连续英文自动换行，后者不行。

>个人测试：连续的字母和数字会自动折行
Firefox,chrome,safari等浏览器在中文和英文状态下显示效果一样当内容到达容器边缘都允许在标点符号和单词中间换行，允许标点符号在行首。
Ie6-11，等浏览器在中文和英文状态下显示效果一样当内容到达容器边缘也是允许单词和句子中间换行，但是他不允许标点符号在行首显示，如果内容到达边缘后第二行行首刚好是标点符号，他会让上一个单子尾字母或中文的汉子跟随标点符号一起换行。

## word-wrap 和 overflow-wrap

> 这个属性是用来说明当一个不能被分开的字符串太长而不能填充其包裹盒时，为防止其溢出，浏览器是否允许这样的单词中断换行。
这里放到一起介绍的是因为 word-wrap 属性原本属于微软的一个私有属性，在 CSS3 现在的文本规范草案中已经被重名为 overflow-wrap 。 word-wrap 现在被当作 overflow-wrap 的 “别名”。 Chrome 和 Opera 浏览器都支持这种新语法。

**语法：**

```css
/* old */
word-wrap：normal | break-word；
/* new */
overflow-wrap: normal | break-word | anywhere;
```
1. `normal`：默认值，允许内容顶开或溢出指定的容器边界，也就是长单词不换行
2. `break-word`：在单词中间换行，当单词的长度超出了容器的长度是会在单词中间截断换到下一行显示。
3. `anywhere`：

>Web-kite,和ie各浏览器显示效果一样，允许连续的字母和数字等内容到达容器边缘后强直换行，和word-break:break-all的区别在于，word-wrap:break-word;不允许在英文单词间换行、标点符号在行首。word-break:break-all则允许英文单词间分开单词换行、标点符号在行首显示。但是ie下标点符号在行首显示不起作用。

**案例展示：**[https://codepen.io/qwguo88/full/ExVpgxj](https://codepen.io/qwguo88/full/ExVpgxj)

<iframe height="500" style="width: 100%;" scrolling="no" title="overflow-wrap:break-word" src="https://codepen.io/qwguo88/embed/ExVpgxj?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/ExVpgxj'>overflow-wrap:break-word</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


如果要在表格下让连续的字母或数字换行，使用`word-break:break-all;`可以达到换行目的但是相应的单词和标点符号会在中间折行。使用`word-wrap:break-word;`不起作用。解决方法是给表格定义`table-layout:fixed;`
**提示：**
> 当然在元素中使用了white-space:pre/nowrap的话，word-wrap:break-wrap和word-break:break-word;都将失去作用，使中文，英文都在同一行显示，不会换行.
在换行中有时还会涉及到：设置或检索对象内空格的处理方式。

## white-space
> 用于设置元素对象内空格的处理方式

**语法：**
```css
white-space: normal | pre | nowrap | pre-wrap | pre-line | break-spaces；
```
**取值说明：**
1. `normal`：浏览器的默认处理方式 连续的空白符会被合并，换行符会被当作空白符来处理 文本自动换行。
2. `pre`： 用等宽字体显示预先格式化的文本，不合并文字间的空白距离，当文字超出边界时不换行，在遇到换行符或者`<br>`元素时才会换行。
3. `nowrap`：强制在同一行内显示所有文本，合并文本间的多余空白，直到文本结束或者遭遇br对象。
4. `pre-wrap`：用等宽字体显示预先格式化的文本，不合并文字间的空白距离，当文字碰到边界时发生换行。
5. `pre-line`：保持文本的换行，不保留文字间的空白距离，当文字碰到边界时发生换行。
6. `break-spaces`：


**案例展示：**[https://codepen.io/qwguo88/full/veZQvO](https://codepen.io/qwguo88/full/veZQvO)

<iframe height="500" style="width: 100%;" scrolling="no" title="white-space" src="https://codepen.io/qwguo88/embed/veZQvO?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/veZQvO'>white-space</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

当`white-sace`设置成`nowrap`的时候`word-break`和w`ord-wrap`设置换行的将都不生效。
当`white-space`设置成pre的时候`word-break`换行将不生效。`word-wrap`换行仅对文字和字符生效如果容器中是图片的话，图片将不换行。块级元素和行内块级元素显示效果一样。
