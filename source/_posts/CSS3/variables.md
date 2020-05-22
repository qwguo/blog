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
```

从上面可以看出在css中定义变量和声明一条css规则差不多只是前边使用`--`两个中横线后边跟着变量名。上面的代码`:root`中定义的变量为全局变量可以在任何元素中使用；`selector`中定义的变量为局部变量，只能在选择器范围内，和他的子元素中使用。

css中的变量名是区分大小写的`--navColor`和`--navcolor`是两个不同的变量。

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
2. `declaration-value`：可选，后补值，当自定义变量值不存在的情况下将使用这个值，他会将把自定义变量名后边的所有参数看成一个整体，所以这个值可以包含逗号`,`、空格` `、括号`()`等css有效的规则值，他不能使用自定义变量名，不能有回车换行，不能有`;`。

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
