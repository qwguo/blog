---
title: blend-mode的使用详解
summary:
  - blend-mode字面上理解就是混合模式，它主要用来设置两个不同元素或者元素多个背景，背景图叠加以后用什么样的滤镜模式来显示叠加部分的效果，类似于Photoshop中的图层的模式
  - 混合模式和filter滤镜效果很想，只是滤镜效果是用来单独设置一个图片的各种效果。
drafts: false
p: CSS3/blend-mode
date: 2020-08-01 19:10:29
categories:
tags:
poster:
---

# blend-mode的使用详解
> 用于设置两个元素叠加以后的混合模式，类似于photoshop中的正片叠底等效果，它的取值非常多能做出不同的效果，接下来我们将详细介绍各值效果。
> 需要注意的是混合模式目前可以使用在元素的多个背景的混合模式`background-blend-mode`，和设置元素本身和父级的混合模式`mix-blend-mode`

**效果示例：**[https://codepen.io/qwguo88/full/pogMYbq](https://codepen.io/qwguo88/full/pogMYbq)

<iframe height="500" style="width: 100%;" scrolling="no" title="blend-mode" src="https://codepen.io/qwguo88/embed/pogMYbq?height=500&theme-id=30742&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/qwguo88/pen/pogMYbq'>blend-mode</a> by qwguo
  (<a href='https://codepen.io/qwguo88'>@qwguo88</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## normal
> 默认值，保持原来的各自颜色，没有任何混合效果

## multiply
> 字面意思乘积，最终混合效果为顶层颜色与底层颜色相乘的结果。

