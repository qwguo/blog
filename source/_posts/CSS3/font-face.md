---
title: css3中的@font-face你真的了解吗
summary:
  - '以前我们在做页面得时候遇到设计师用特殊字体设计得特效文本效果我们得处理办法是做成固定得图片，然后应用到网站中，使用图片文字只能是固定不变的，这并不是我们期望的。'
  - '随着浏览器得更新迭代，现在的浏览器已经基本支持我们引入外部字体库，并且应用到网站，同时我们可以随时更改文本内容'
drafts: false
p: CSS3/font-face
date: 2020-05-26 14:54:57
categories:
tags: [CSS3, FontFace, font-face, font-family]
poster: poster.png
---

# css3中的自定义字体方法@font-face

> `@font-face`属性可以让我们自定义网站字体属性，然后引用到想要应用该字体的元素上。

## 基本语法：
```css
@font-face {
  font-family: <font-name>;
  src: local( <family-name> ) | <url> [format("formatName")][,<url> [format("formatName")]]*;
  unicode-range: <unicode-range>;
  font-variant: <font-variant>;
  font-feature-settings: <font-feature-settings>;
  font-variation-settings: <font-variation-settings>;
  font-stretch: <font-stretch>;
  font-weight: <font-weight>;
  font-style: <font-style>;
  font-display: <font-display>;
}
```
## 属性规则说明

###  font-family
> 给你引入的字体起一个专属的字体名字，`font-name`，然后他会在元素`font-family:`中使用，如`div{font-family:font-name}`；

### src
> 用于指定加载字体文件的路径或者加载本地字体

#### local
> 加载一个本地字体，`font-name`表示本地的字体名称，比如`Microsoft YaHei | 微软雅黑`；如果本地有应用此字体显示文本。

**示例：**
```css
/* 加载一个本地字体 */
@font-face{
  font-family: myFont;
  src: local('Microsoft YaHei');
}
/* 加载多个本地字体 */
@font-face{
  font-family: myFont;
  src:  local(黑体), local("Microsoft YaHei"), local("HelveticaNeue-Light"), local("Helvetica Neue Light"),  local("PingFang SC"), local(sans-serif);
}
/* 应用自定义字体 */
.box{
  font-family: myFont;
}
```
在上边代码中看到，可以使用一个或多个`local`，多个之间用逗号分开，括号中的字体名称可以使用单引号或者双引号括起来，也可以不带引号直接写字体名称，有空格的必须添加引号，_但是只能写一个字体名称_；
上边的写法让我们在定义字体的时候变得方便很多，我们只需要定义好自定义名称然后直接引用该字体等同于下边代码：
```css
.box{
  font-family: 黑体, "Microsoft YaHei", "HelveticaNeue-Light", "Helvetica Neue Light", "PingFang SC", sans-serif;
}
```

#### url
> 表示服务器端提供的字体地址，这个也是可以使用多个，多个之间用逗号隔开，一般写多个是为了浏览器兼容加载不同格式的字体。目前web可以加载六种格式的字体：

1. `EOT`：全拼：`Embedded_OpenType`，是由微软开发的字体格式规范，所以只适用于IE浏览器。[详细介绍](https://en.wikipedia.org/wiki/Embedded_OpenType)

  兼容：
  ![image](EOT_caniuse.png)
  [兼容详情](https://caniuse.com/#search=EOT)

2. `TTF`：全拼：`TrueType`，是一种轮廓字体标准，最早是由苹果公司研发，后来成为`Mac OS`、`Microsoft Windows`系统中最常用的字体格式。[详细介绍](https://en.wikipedia.org/wiki/TrueType)

  兼容：
  ![image](TTF_OTF_caniuse.png)
  [兼容详情](https://caniuse.com/#search=TTF)
3. `OTF`：全拼：`OpenType`，是可缩放计算机字体的格式，是由微软和Adobe公司联合开发。[详细介绍](https://en.wikipedia.org/wiki/OpenType)

  兼容：
  ![image](TTF_OTF_caniuse.png)
  [兼容详情](https://caniuse.com/#search=OTF)
4. `WOFF`：全拼：`Web Open Font Format`web网络开放字体格式，他是专为网络设计的一种字体格式，`WOFF`是把`OpenType`和`TrueType`字体进行了封装，并进行了压缩优化，它使用了广泛应用的`zlib`压缩，并添加了XML元数据，这种字体格式体积更小，适用于网络传输，可以使用户体验做到更好。[详细介绍](https://en.wikipedia.org/wiki/Web_Open_Font_Format)

  兼容：
  ![image](WOFF_caniuse.png)
  [兼容详情](https://caniuse.com/#feat=mdn-css_at-rules_font-face_woff)
5. `WOFF2`：它是WOFF的升级版，它使用`Brotli`进行字节级压缩，比`WOFF`体积更小

  兼容：
  ![image](WOFF2_caniuse.png)
  [兼容详情](https://caniuse.com/#feat=mdn-css_at-rules_font-face_woff_2)

6. `SVG`：全拼：`Scalable Vector Graphics`可缩放矢量图形，是一种基于可扩展标记语言（XML）的矢量图像格式，用于二维图形，并支持交互性和动画，字体中就是使用svg技术来呈现文字样式。我测试只有苹果`Safari`支持； [详细介绍](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics)

  兼容：
  ![image](SVG_caniuse.png)
  [兼容详情](https://caniuse.com/#feat=svg-fonts)

#### format
> 可选值，表示给加载的外部字体指定字体格式，用来告诉浏览器让浏览器能够识别所使用的字体格式，可用的类型有 `embedded-opentype`, `truetype`, `opentype`, `woff`, `woff2`, `svg`。分别对应上边我们介绍的字体格式。

**语法：**
```css
/* 加载一种字体格式 */
@font-face{
  font-family: "myFontName";
  src:  url('font.woff') format('woff');
}

/* 加载多个字体格式，兼容更多浏览器 */
@font-face{
  font-family: "myFontName";
  src: url('font.eot'); /* IE9*/
  src: url('font.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('font.woff2') format('woff2'),
  url('font.woff') format('woff'), /* chrome、firefox */
  url('font.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
  url('font.svg#Alibaba-PuHuiTi-Regular') format('svg'); /* iOS 4.1- */
}
```
从上边语法来看我们可以加载一个格式的字体文件，也可以加载多个格式字体，之间用逗号分开，浏览器会优先读取写在前面的字体格式并且检测是否支持，如果支持就使用该格式的字体文件。

### font-weight
> 表示自定义字体规则的字重程度，我们可以给一个字体指定不同的粗细规则引用不同规格的字体文件。

**语法：**
```css
/* Single values */
font-weight: normal;
font-weight: bold;
font-weight: 400;

/* Multiple Values */
font-weight: normal bold;
font-weight: 300 500;
```
**取值说明：**

1. `normal`：默认值，表示该字体规则是在默认情况下的字体，也就是在应用改字体的元素中不规定字体的粗细情况或者`font-weight: 400 | normal`下应用该字体；
2. `bold`：粗体，表示元素设置`font-weight: bold | 700`，或者使用`<b>`、`<strong>`元素的时候应用该字体。
3. `400`：也可以设置成数值，在CSS Fonts Level 4之前的版本只能去`100-900`的100倍数值，之后的数值可以去`1-1000`的任意数值。
4. `normal bold`：可以使用多个关键字来定义此字体规则，多个关键字之间用逗号分开，表示元素字重设置为此关键字中的其中一个值时应用该字体。
5. `300 500`：也可以使用多个数值来定义此字体规则。

**取数值情况下应该对应的每个字体：**

value | 对应的字体的自重名称
--- | ---
100	| Thin (Hairline)
200	| Extra Light (Ultra Light)
300	| Light
400	| Normal
500	| Medium
600	| Semi Bold (Demi Bold)
700	| Bold
800	| Extra Bold (Ultra Bold)
900	| Black (Heavy)

**代码示例：**因为字体有版权限制，这里我们使用阿里的免费商用字体来演示

[https://codepen.io/qwguo88/full/jObgQYG](https://codepen.io/qwguo88/full/jObgQYG)

<iframe height="400" style="width: 100%;" scrolling="no" title="font-face-font-weight" src="https://codepen.io/qwguo88/embed/jObgQYG?height=400&theme-id=30742&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/jObgQYG'>font-face-font-weight</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

从上边的案例我们可以看出，先自定义了一个名为`FW`的字体，并且使用`font-weight`定义不同字重使用不同的字体。在上边的案例中定义了5中字重样式，分别是`bold`：_阿里巴巴-普惠体-Heavy_，`100`：_杨任东竹石体-Bold_，`200`：_站酷高端黑_，`300 600`：_庞门正道标题体2_，`900`：_思源黑体-粗_
然后给div设置`font-family:FW`;最后我们分别给这个div下的每个段落设置不同的`font-weight`,段落的字体就会根据不同的字重来应用不同的字体。
我们可以把自定义字体看成我们平常使用系统内置字体一样，当我们设置字体为`微软雅黑`，并且设置不同的字重他会在系统中寻找每个自重对应的字体，然后来显示。

### font-style
> 表示自定义字体规则的样式表现形式，我们可以给一个字体指定不同的样式规则引用不同规格的字体文件。

**语法：**
```css
font-style: normal | italic | oblique <angle>{0,2}
```
**取值说明：**

1. `normal`：默认字样式使用的字体规则，当我们不设置或者设置成此值时的字体。
2. `italic`：表示字样式设置成斜体的时候使用的字体规则。
3. `oblique`：表示字样式设置成斜体的时候使用的字体规则。

当我们同时定义`italic`和`oblique`规则的字体时，写在后边的生效所设置的斜体字体显示。

**代码示例：** [https://codepen.io/qwguo88/full/RwWXONo](https://codepen.io/qwguo88/full/RwWXONo)

<iframe height="300" style="width: 100%;" scrolling="no" title="font-face-font-style" src="https://codepen.io/qwguo88/embed/RwWXONo?height=300&theme-id=30742&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/RwWXONo'>font-face-font-style</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


### unicode-range
> 表示自定义字体规则的unicode字符范围

**语法：**
```css
/* unicode-range 取值规则 */
unicode-range: U+26;                /* 单个值 */
unicode-range: U+0-7F;              /* 字符编码区间*/
unicode-range: U+0025-00FF;        /* 字符编码区间 */
unicode-range: U+4??;              /* 通配符区间 */
unicode-range: U+0025-00FF, U+4??; /* 可以写多个值，多个值之间用逗号分开 */
```
**取值说明：**
取值规则：前边是`U+`后边跟上字符的`charCode`值
1. 可以是单个值，表示文本中只有该字符的字应用该字体。
2. 可以使用一个字符区间，表示文本中如果有在此区间的文字将应用改字体规则。
3. 也可以使用通配符来设置一个区间规则其中`?`表示一个16进制`0-F`的之间的值`U+4??`表示 `U+400` 到 `U+4FF`区间的字符编码。
4. 也可以使用多个值，多个值之间使用逗号分开。

**案例：**[https://codepen.io/qwguo88/full/XWXWqmP](https://codepen.io/qwguo88/full/XWXWqmP)

<iframe height="300" style="width: 100%;" scrolling="no" title="font-face-unicode-range" src="https://codepen.io/qwguo88/embed/XWXWqmP?height=300&theme-id=30742&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/XWXWqmP'>font-face-unicode-range</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

从上边案例可以看出，`unicode-range`是用来规定应用当前字体规则的文字`unicode`码在规则内的将以此字体规则显示字体。
他能让我们来控制一个段落中的个别字的显示效果，一般要显示的字体规则排在最前面，将优先显示。

### font-variant
### font-feature-settings
### font-variation-settings
### font-stretch

### font-display
> 设置自定义字体在没有加载完的显示方式取值如下：

**语法：**
```css
font-display: auto | block | swap | fallback | optional
```

1. `auto`：字体显示策略由用户代理定义。
2. `block`：为字体提供一个短暂的阻塞周期和无限的交换周期。也就是说等字体加载完以后字体显示效果会自动更新成改字体
3. `swap`：为字体提供一个非常小的阻塞周期和无限的交换周期。也就是说等字体加载完以后字体显示效果会自动更新成改字体
4. `fallback`：为字体提供一个非常小的阻塞周期和短暂的交换周期。也就是说等字体加载在过了一定的交互周期后加载完字体将不进行更新显示
5. `optional`：为字体提供一个非常小的阻塞周期，并且没有交换周期。也就是说等字体加载不进行更新显示


## 参考网站

1. https://webplatform.github.io/docs/tutorials/typography/font-face/
