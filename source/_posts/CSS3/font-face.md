---
title: css3中的@font-face
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

> `@font-face`属性可以让我们自定义字体名称，然后引入一个我们提供的特殊字字体文件。

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
> 给你引入的字体起一个名字，`font-name`你定呀的名字，他会在元素`font-family:`中使用，如`div{font-family:font-name}`；

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
  src:  local(黑体),
        local("Microsoft YaHei");
}
/* 应用自定义字体 */
.box{
  font-family: myFont;
}
```
在上边代码中看到，可以使用一个或多个`local`，多个之间用都好分开，括号中的字体名称可以使用单引号或者双引号括起来，也可以不带引号直接写字体名称，_但是只能写一个字体名称_

#### url
> 表示服务器端提供的字体地址，这个也是可以使用多个，多个之间用都好隔开，一般写多个是为了浏览器兼容加载不同格式的字体。目前网上可以加载四种格式的字体：

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
> 可选值，表示给加载的外部字体指定字体格式，用来告诉浏览器让浏览器能够识别，可用得类型有 `woff`, `woff2`, `truetype`, `opentype`, `embedded-opentype`, `svg`。

```css
@font-face{
  font-family: "myFontName";
  font-display: swap;
  src: url('font.eot'); /* IE9*/
  src: local(<family-name>)
  url('font.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('font.woff2') format('woff2'),
  url('font.woff') format('woff'), /* chrome、firefox */
  url('font.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
  url('font.svg#Alibaba-PuHuiTi-Regular') format('svg'); /* iOS 4.1- */
}
```


## 参考网站

1. https://webplatform.github.io/docs/tutorials/typography/font-face/
