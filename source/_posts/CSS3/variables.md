---
title: css3中的变量
summary:
  - '在css中一提到变量大家都会想到css预处理LESS、SCSS、Stylus等语言中提供的变量使用，能够很方便的把我们经常需要更改的值统一归类管理，在我们需要更改色系样式的时候直接更改我们事先定义好的变量值，然后编辑成css就可以了。css预处理虽然让我们在写css变得更方便，但是毕竟还需要编译，需要去学习他们的语法。'
  - 'css3为我们提供了变量的功能，并且比预处理更强大，更简单...'
drafts: false
p: CSS3/variables
date: 2020-05-21 19:26:58
categories: [CSS, CSS3]
tags:
  - variables
  - CSS3
poster:
---

# CSS3新功能之变量：variables

> css3为我们提供了一个强大的功能自定义属性，也就是变量，他能让我们更改色系、皮肤、自适配变得简单。我们只需要更改一些我们事先定义好的变量就可以轻松实现各种效果。特别是我们在开发大型项目的时候有多处使用相同的值来表示，这个时候我们就可以吧相同的属性值抽离出来定义成变量方便我们后期统一修改

## 变量声明

```css
/* 定义全局变量 */
:root{
  --navColor: #c00;
  --navPadding: 10px;
}

/* 定义局部变量 */
selector{
  --nameFont: italic small-caps 400 12px / 20px '微软雅黑';
  --boxBorder: 2px solid rgba(0, 0, 0, .2);
}
/* 使用var函数定义变量 */
selector{
  --borderWidth: 8px;
  --borderColor: red;
  --borderStyle: solid;
  --border: var(--borderWidth) var(--borderColor) var(--borderStyle);
  border: var(--border);
}
```

从上面可以看出在css中定义变量和声明一条css规则差不多只是前边使用`--`两个中横线后边跟着变量名。上面的代码`:root`中定义的变量为全局变量可以在任何元素中使用；`selector`中定义的变量为局部变量，只能在选择器范围内，和他的子元素中使用。

**需要注意：**
1. css中的变量名是区分大小写的`--navColor`和`--navcolor`是两个不同的变量;
2. 定义变量的时候`:`号和`;`中间是一个整体，整体是变量的值;
3. 变量值也就是css的规则值，任何规则值都可以存入变量，并且变量值不用加引号;

**兼容性：**
![image](custom-variables-caniuse.png)

[查看兼容详情](https://caniuse.com/#search=--)


## 变量使用
> 要想使用上边我们定义的变量，就要用到`var()`函数

**语法：**

```css
  var( <custom-variable-name> , <declaration-value>? )
```
**参数说明：**

1. `custom-variable-name`：必填，表示我们定义的变量名；
2. `declaration-value`：可选，后补值，当自定义变量值不存在的情况下将使用这个值，他会将把自定义变量名后边的所有参数看成一个整体，所以这个值可以包含逗号`,`、空格`  `、括号`()`等css有效的规则值，他不能使用自定义变量名，不能有回车换行，不能有`;`。

**实例：**

```css
.nav{
  color: var(--navColor);
  padding: var(--navPadding);
}
selector{
  font: var(--nameFont, normal 700 16px/ 30px '黑体');
  border: var(--boxBorder, 1px solid #c00);
}
```
**兼容性：**
![image](var-caniuse.png)

[查看兼容详情](https://caniuse.com/#search=css%20var)

## 变量的作用域
> 上面我们提到过css的变量是有它的作用域的，在全局和布局同时定义了一个变量，会优先应用局部作用域。

**代码说明：**
```html
<div class="div-1">这里显示绿色文字</div>
<div class="div-2">这里显示红色文字</div>
<div class="div-3" style="--fontColor:blue;">这里显示蓝色文字</div>
<style>
:root{
  --fontColor: red;
}
.div-1{
  --fontColor: green;
  /* 这里将应用绿色的文字样式，也就是自己定义的局部变量 */
  color: var(--fontColor);
}
.div-2{
  /* 这里将应用红色的文字样式，也就是根目录的变量 */
  color: var(--fontColor);
}
.div-3{
  /* 这里将应用蓝色的文字样式，也就是元素中style行内定义的变量 */
  color: var(--fontColor);
}
</style>
```

## 变量的优先级
> css中应用变量时的优先级和css定义用选择器定义属性优先级差不多

**代码说明：**
```html
<div class="box-1" id="box">
  <span class="span">这里显示绿色文字<span>
</div>
<style>
:root{
  --bgColor: red;
}
#box{
  --bgColor: blue;
}
.box-1{
  --bgColor: green;
}
.span{
  --bgColor: purple;
}
.box-1{
  /* 这里将应用蓝色的背景样式，也就是通过id定义的变量 */
  background-color: var(--bgColor);
}
.span{
  /* 这里将应用自色的背景样式，也就是通过自己class名定义的变量 */
  background-color: var(--bgColor);
}
</style>
```

从上边代码可以看出，css获取变量和css的样式优先级一样，顺序是：`!important` > `style=""` > `#id` > `.class` > `tagName` > `:root`; 但是需要注意的是这里的`span`是先找自己定义作用域下的变量，如果没有才找父级作用域的变量，上边代码`span`自身定义的有变量，所以背景就是紫色。

**案例演示：**[https://codepen.io/qwguo88/full/eYpXGGQ](https://codepen.io/qwguo88/full/eYpXGGQ)

<iframe height="500" style="width: 100%;" scrolling="no" title="css-variables" src="https://codepen.io/qwguo88/embed/eYpXGGQ?height=500&theme-id=30742&default-tab=result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/eYpXGGQ'>css-variables</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## javascript中操作变量
> css3中的变量我们也可以使用javascript来获取和操作它

```javascript
// 获取行内样式的变量名
element.style.getPropertyValue("--variableName");

// 获取样式表里定义的变量
getComputedStyle(element).getPropertyValue("--variableName");

// 设置变量的值
element.style.setProperty("--variableName", value);
```

## 检测浏览器支持情况
> 我们可以通过css语法和javascript语法来检测浏览器是否支持css变量

css通过`@supports`性能查询语法来检测

**语法：**
```css
@supports (--a: 0){
  .box{
    background-color:#c00;
  }
}
@supports(not(--a: 0)){
  .box{
    background-color:#cc0;
  }
}
```
**js语法检测：**

```javascript
const isSupported = window.CSS && window.CSS.supports && window.CSS.supports('--a', 0);

if (isSupported) {
  /* supported */
} else {
  /* not supported */
}
```

**参考链接：**

1. 阮一峰老师：[http://www.ruanyifeng.com/blog/2017/05/css-variables.html](http://www.ruanyifeng.com/blog/2017/05/css-variables.html)
2. google developers： [https://developers.google.com/web/updates/2016/02/css-variables-why-should-you-care](https://developers.google.com/web/updates/2016/02/css-variables-why-should-you-care)
3. MDN：[https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
