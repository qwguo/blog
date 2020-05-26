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

**基本语法：**
```css
@font-face {
  [ font-family: <family-name>; ] ||
  [ src: <src>; ] ||
  [ unicode-range: <unicode-range>; ] ||
  [ font-variant: <font-variant>; ] ||
  [ font-feature-settings: <font-feature-settings>; ] ||
  [ font-variation-settings: <font-variation-settings>; ] ||
  [ font-stretch: <font-stretch>; ] ||
  [ font-weight: <font-weight>; ] ||
  [ font-style: <font-style>; ]
}
```

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
