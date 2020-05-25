---
title: FontFace对象
summary:
  - 'js中得FontFace对象它能够让我们给网站应用非安全字体变得方便，它和css中得@font-face相对应，@font-face是通过css来引入字体库文件，然后通过css的font-family来应用字体，此对象是用js来声明一个字体对象然后应用倒网站中。'
drafts: false
p: JavaScript/FontFace
date: 2020-05-25 21:11:07
categories: JavaScript
tags: [JavaScript, FontFace]
poster: poster.png
---

# JavaScript 中FontFace对象的使用
> `FontFace`字面理解就是字体脸，也就是文字字体样式的意思，它是通过使用javascript来定义字体对象，并且引入客户端没有安装得字体文件，可以是者服务器端，或者是第三方字体库文件

**基本语法：**
```javascript
concat fontFace  = new FontFace('fontFamily', 'url(fontUrl)', descriptors);
```
**参数说名：**
1. `fontFamily`：字符串，自定义的要应用到页面或者元素中得字体名称；
2. `fontUrl`：字符串，字体文件的路径，可以是第三方字体文件路径,但是需要请求的地址服务器开启跨越访问，此值必须要用`url()`包裹起来；
3. `descriptions`：对象形式，可选值，用来设置字体显示，和样式等，可以设置得值：
  - `family`: Family
  - `style`: 设置字体是样式，对应css中的`font-style`取值；
  - `weight`: 设置字体的粗细，对应css中的`font-weight`取值；
  - `stretch`: 设置如何拉伸字体，对应css中的`font-stretch`取值；
  - `unicodeRange`: 定义字体支持的UNICODE字符范围
  - `variant`: variant
  - `featureSettings`: Feature settings

