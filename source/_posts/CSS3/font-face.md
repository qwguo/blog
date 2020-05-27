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

1. `EOT`：只适用于IE浏览器。
2. `TTF`：
2. `woff`：

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
