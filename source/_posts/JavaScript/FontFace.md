---
title: FontFace对象
summary:
  - 'js中的FontFace对象它能够让我们给网站应用非安全字体变得方便，它和css中得@font-face相对应，@font-face是通过css来引入字体库文件，然后通过css的font-family来应用字体，此对象是用js来声明一个字体对象然后应用倒网站中。'
drafts: false
p: JavaScript/FontFace
date: 2020-05-25 21:11:07
categories: JavaScript
tags: [JavaScript, FontFace]
poster: poster.png
---

# JavaScript中FontFace对象的使用
> `FontFace`字面理解就是字体脸，也就是文字字体样式的意思，它是通过使用javascript来定义字体对象，并且引入客户端没有安装得字体文件，可以是者服务器端，或者是第三方字体库文件

## 介绍

**基本语法：**
```javascript
concat fontFace  = new FontFace('fontFamily', 'url(fontUrl) | ArrayBuffer', descriptors);
```
**参数说名：**
1. `fontFamily`：字符串，自定义的要应用到页面或者元素中得字体名称；
2. `fontUrl`：字符串，字体文件的路径，可以是第三方字体文件路径,但是需要请求的地址服务器开启跨越访问，此值必须要用`url()`包裹起来；
3. `ArrayBuffer`：用于描述的外部资源构建的二进制编码数组
4. `descriptions`：对象形式，可选值，用来设置字体显示，和样式等，可以设置得值：
  - `family`: 定义字体名称，这里的设置会被第一个参数值替代，但是我们可以通过实例对象的`fontFace.family`属性进行更改。
  - `style`: 设置字体是样式，对应css中的`font-style`取值；
  - `weight`: 设置字体的粗细，对应css中的`font-weight`取值；
  - `stretch`: 设置如何拉伸字体，对应css中的`font-stretch`取值；
  - `unicodeRange`: 定义字体支持的UNICODE字符范围
  - `variant`: variant
  - `featureSettings`: Feature settings
  - `display`：设置字体在没有加载完的显示规则取值如下：
    - `auto` 字体显示策略由用户代理定义。
    - `block` 为字体提供一个短暂的阻塞周期和无限的交换周期。也就是说等字体加载完以后字体显示效果会自动更新成改字体
    - `swap` 为字体提供一个非常小的阻塞周期和无限的交换周期。也就是说等字体加载完以后字体显示效果会自动更新成改字体
    - `fallback` 为字体提供一个非常小的阻塞周期和短暂的交换周期。也就是说等字体加载在过了一定的交互周期后加载完字体将不进行更新显示
    - `optional` 为字体提供一个非常小的阻塞周期，并且没有交换周期。也就是说等字体加载不进行更新显示

进过测试发现，上边的`descriptions`对象的属性，处理`display`能测试出效果外，其他并没有生效，可能是我应用的字体不支持原因


## 兼容性

![image](FontFace_caniuse.png)

从图上可以看出这是一个新的对象方法，`IE`，`Edge18-`，等低版本浏览器基本不兼容这个对象，如果我们要做兼容可以使用下边介绍的异步加载方式；


## 创建FontFace对象
> 创建`FontFace`对象和创建普通对象基本相同，用new 关键字创建

**实例：**

```javascript
var myFonts = new FontFace('myFontName', 'url(ShouShu.ttf)', {
    style: 'italic',  //这里需要字体的支持
    weight: 700,  //这里需要字体的支持
    display: 'swap',
    family: 'ali',  //这个值被第一个参数代替
    variant: 'small-caps'  //这里需要字体的支持
});
```

### FontFace对象属性

![image](fontFace_object_property.png)

从图上可以看出，FontFace对象的属性跟`descriptions`参数基本相同。我们可以通过对象属性来更改这些值。比如可以通过`fontFace.family="newName"`来更改之前我们new实例化时定义得第一个参数的值。

### FontFace对象方法

1. `load()`：`FontFace`对象为我们提供了一个方法，表示当字体文件加载完毕以后的方法，它返回一个`Promise`对象，并且使用当前的`FontFace`对象进行解析


## 将创建的FontFace字体添加到页面中
> 我们创建完对象以后并不能直接在页面中生效，需要我们通过`FontFaceSet`对象方法将字体添加到页面中，才能使页面中的字体生效，我们可以通过使用`document.fonts`隐式引用`FontFaceSet`对象，并且使用它的`add()`方法将字体添加到页面。

### 通过字体Promise回调添加
**语法：**

```javascript
var myFonts = new FontFace('myFontName', 'url(ShouShu.ttf)',{});
myFonts.load().then(function(loadFace){
  document.fonts.add(loadFace);
});
```
上面代码我们使用了`load()`方法，当字体文件加载完毕以后再执行添加操作。

### 通过Ajax获取字体文件后回调添加
_**这里我们也可以使用异步的方式加载字体文件**_

**语法：**

```javascript
var xhr = new XMLHttpRequest(); // 定义一个异步对象
xhr.open('GET', 'ShouShu.ttf', true); // 异步GET方式加载字体
xhr.responseType = "arraybuffer"; //把异步获取类型改为arraybuffer二进制类型
xhr.onload = function(){
  // 这里做了一个判断：如果浏览器支持FontFace方法执行
  if(typeof FontFace != 'undefined'){
    var buffer = this.response;  //获取字体文件二进制码
    var myFonts = new FontFace('myFontName', buffer);  // 通过二进制码实例化字体对象
    document.fonts.add(myFonts); // 将字体对象添加到页面中
  }else{
    // 如果浏览器不支持FontFace方法，直接添加样式到页面
    var styles = document.createElement('style');
    styles.innerHTML = '@font-face{font-family:"myFontName";src:url("ShouShu.ttf") format("truetype");font-display:swap;}';
    console.log(document.getElementsByTagName('head'));
    document.getElementsByTagName('head')[0].appendChild(styles);
  }
}
xhr.send();
```

## 页面中使用我们添加的字体

> 我们使用字体文件有两种方式，一种是事先在css中定义，另一种是通过js改变

### css事先定义好

```html
<!-- css -->
<style>
  .box{
    font-family: myFont; /*这里我们先定义好使用的字体*/
  }
</style>

<!-- html -->
<div class="box">执子之手，方知子丑，泪流满面，子不走我走</div>

<!-- js -->
<script>
  // 页面加载完以后加载字体文件
  window.onload = function(){
    var myFonts = new FontFace('myFont', 'url(ShouShu.ttf)',{display: 'swap'});
    myFonts.load().then(function(loadFace){
      document.fonts.add(loadFace);
    });
  }
</script>
```
### 通过js更改元素的字体

```javascript
// 页面加载完以后加载字体文件
window.onload = function(){
  var myFonts = new FontFace('myFont', 'url(ShouShu.ttf)',{display: 'swap'});
  myFonts.load().then(function(loadFace){
    document.fonts.add(loadFace);
    // 给body设置字体样式 Arial为后补字体
    document.body.style.fontFamily = 'myFont, Arial';
    //或者单独给元素设置
    var box = document.getElementsByClassName("box");
    for (var i = 0; i < box.length; i++) {
      box[i].style.fontFamily = "myFont, Arial";
    }
  });
}
```

## 参考网站
1. https://webplatform.github.io/docs/tutorials/typography/fontface/
