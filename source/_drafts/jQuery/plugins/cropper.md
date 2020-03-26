---
title: cropper.js 图片处理插件
categories: [JavaScript, plugins]
tags: [JavaScript, jQuery插件, 图片处理, 图片裁剪]
poster: poster.jpg
summary: ['cropper.js一个用来处理图片的插件，可以使用它来实现图片的各种模式下的裁切效果，当我们在做一个上传头像或者上传图片功能的时候，需要用户裁切出用户想要的图片位置就可以利用这个插件来实现','cropper.js支持移动设备的图片剪裁。它基于HTML5 canvas，可以通过Base64编码导出剪裁后的图片。']
---
# 图片剪裁插件Image Cropper使用方法
> cropper是一款使用简单且功能强大的图片剪裁jQuery插件。该图片剪裁插件支持图片放大缩小，支持鼠标滚轮操作，支持图片旋转，支持触摸屏设备，支持canvas，并且支持跨浏览器使用。
- 支持Promise API。
- 支持移动触摸事件。
- 基于canvas技术，支持canvas的浏览器都可以使用该插件。
- 通过Base64编码导出剪裁后的图片。
- 可以通过json数据来获取图片的位置和大小。
- 可以通过json数据来设置图片的位置和大小。
- 可以通过URL来获取图片。

## 下载使用

### 网站
- 官网：https://github.com/fengyuanchen/cropper
- 演示地址：https://fengyuanchen.github.io/cropper/
- 衍生产品-_Photo Editor_：https://fengyuanchen.github.io/photo-editor/

### 下载安装
```shell
# 可以使用npm下载
npm install cropper jquery
# 通过bower安装
$ bower install cropper jquery
# 通过yarn安装
$ yarn add cropper jquery
```

### 引入文件
```html
<!-- 引入css样式 -->
<link  href="cropper.css" rel="stylesheet">
<!-- 引入js文件 -->
<script src="jquery.js"></script>
<script src="cropper.js"></script>
```
### 构建html
```html
<!-- 可以将图片或canvas直接包裹到一个块级元素中 -->
<div class="container">
  <img id="image" src="picture.jpg">
</div>
```
### 设置样式
```css
/* 给container元素设置宽高 并且限制图片的宽避免图片溢出容器 */
.container{
  width: 500px;
  height: 500px;
}
.container img {
  max-width: 100%;
}
```
### 初始化插件。
```javascript
// jquery获取元素
var $image = $('#image');
// 通过jquery Dom 的cropper方法初始化
$image.cropper({
  aspectRatio: 16 / 9,
  crop: function(event) {
    console.log(event.detail.x);
    console.log(event.detail.y);
    console.log(event.detail.width);
    console.log(event.detail.height);
    console.log(event.detail.rotate);
    console.log(event.detail.scaleX);
    console.log(event.detail.scaleY);
  }
});
// 可以通过Dom对象的data的cropper属性获取初始化后获取Cropper.js实例
var cropper = $image.data('cropper');
```
## 详细说明
### 参数(options)
> 在调用cropper方法的时候我们可以传递可选的参数选项options，也可以通过setDefaults(options)设置选项，cropper支持39个可选属性

```javascript
$('img').cropper(options);
// or
// 设置全局cropper属性
$.fn.cropper.setDefaults(options)

// 参数项说明
options = {
  viewMode: 0,
  dragMode: DRAG_MODE_CROP,
  initialAspectRatio: NaN,
  aspectRatio: NaN,
  data: null,
  preview: '',
  responsive: true,
  restore: true,
  checkCrossOrigin: true,
  checkOrientation: true,
  modal: true,
  guides: true,
  center: true,
  highlight: true,
  background: true,
  autoCrop: true,
  autoCropArea: 0.8,
  movable: true,
  rotatable: true,
  scalable: true,
  zoomable: true,
  zoomOnTouch: true,
  zoomOnWheel: true,
  wheelZoomRatio: 0.1,
  cropBoxMovable: true,
  cropBoxResizable: true,
  toggleDragModeOnDblclick: true,
  minCanvasWidth: 0,
  minCanvasHeight: 0,
  minCropBoxWidth: 0,
  minCropBoxHeight: 0,
  minContainerWidth: 200,
  minContainerHeight: 100,
  ready: null,
  cropstart: null,
  cropmove: null,
  cropend: null,
  crop: null,
  zoom: null
}
```

#### viewMode
>  定义裁纸器的查看模式。如果设置viewMode到0，裁剪框可以画布外的延伸，而一个值1，2或3将限制裁剪框画布的大小。甲viewMode的2或3将另外限制画布到容器上。请注意，如果画布和容器的比例相同，则2和之间没有区别3。

- 类型： `Number`
- 默认： `0`
- 选项：
  - 0：无限制
  - 1：限制裁切框不要超过图片的大小, 图片可以小于容器框。
  - 2：限制裁剪框不能超出图片的范围，且图片填充模式为 cover 最长边填充满容器，有短边填充不满的情况
  - 3：限制裁剪框不能超出图片的范围，且图片填充模式为 contain 最短边填充，最短边填充，有长边超出的现象

0 | 1 | 2 | 3
---------|----------|---------|---------
![image](viewMode_0.jpg) | ![image](viewMode_1.jpg) | ![image](viewMode_2.jpg) | ![image](viewMode_3.jpg)

#### dragMode
> 定义裁切器的拖动模式

- 类型： `string`
- 默认：`crop`
- 选项：
  - `crop`：创建一个新的裁剪框, 图片不能移动
  - `move`：不从新创建裁切框，可以拖动图片位置，这个时候需要确保`movable`属性设置为`true`
  - `none`：不从新创建裁切框，也不能拖动图片

#### initialAspectRatio
> 定义裁剪框的初始宽高比。默认情况下，它与画布（图像包装器）的纵横比相同。_这个值只有在`aspectRatio`值不进行设置的时候生效_

- 类型： `Number` _可以是数字，或者数学计算公式如16/9、4/3_
- 默认： `NaN`

#### aspectRatio
> 定义裁剪框的可拖动的长宽比。默认情况下是自由拖动，设置后将按照设置比例缩放大小

- 类型： `Number` _可以是数字，或者数学计算公式如16/9、4/3_
- 默认： `NaN` 自由比例

#### data
> 定义初始化裁切框的位置，大小等信息

- 类型：`object`
- 默认：''

#### preview
> 指定额外的dom元素（容器）以进行选择区域预览效果，元素或元素数组或节点列表对象或Document.querySelectorAll的有效选择器。

- 类型： `Element`：dom元素、`Array`：多个dom元素的数组形式，`nodeList`：dom列表，`String` dom的选择器，可以是`#id`、`.class`、`标签名`等
- 默认： `''` 没有任何元素
- 注意：
  - 一定要设置元素的宽度和高度。
  - 如果设置了`aspectRatio`属性的话最好按照这个比例设置宽高。
  - 并且给元素设置`overflow:hidden`让元素多余截取隐藏

效果展示：可以同时添加多个预览元素
![image](preview.jpg)

#### responsive
> 在调整窗口大小的时候是否重新渲染裁切区域

- 类型：`Boolean`
- 默认：`true`

#### restore
> 在调整完窗口大小后，恢复裁剪区域

- 类型：`Boolean`
- 默认：`true`

#### checkCrossOrigin

> 检查当前图像是否是跨源图像。
如果是这样，则在克隆图像时，crossOrigin会将属性添加到克隆的图像元素，_并将时间戳添加到该src属性以重新加载源图像，以避免浏览器缓存错误_。
通过向crossOrigin图像元素添加属性将停止向图像URL添加时间戳并停止重新加载图像，但是读取图像数据以进行方向检查的请求（XMLHttpRequest）将需要一个时间戳来破坏缓存，以免现在浏览器缓存出错，您可以设置取消此请求的checkOrientation选项false。
如果图像的crossOrigin属性值为"use-credentials"，则当XMLHttpRequest读取图像数据时，该withCredentials属性将设置为true。。

- 类型：`Boolean`
- 默认：`true`

#### checkOrientation

>检查当前图像的Exif方向信息。请注意，只有JPEG图像可以包含Exif方向信息。用于在旋转或翻转图像时做一些处理，以避免在iOS设备上一些问题。
此属性需要同时将`rotatable`和`scalable`选项设置为`true`才生效。

- 类型：`Boolean`
- 默认：`true`

#### modal

>是否在裁切框的下方显示半透明的黑色遮罩。_当设置为`false`遮罩的dom元素是一直显示的只是把元素设置成透明_

- 类型：`Boolean`
- 默认：`true`


true | false
---------|----------
![image](modal_true.jpg) | ![image](modal_false.jpg)


#### guides

> 在裁切框中是否显示网格

- 类型：`Boolean`
- 默认：`true`

true | false
---------|----------
![image](guides_true.jpg) | ![image](guides_false.jpg)

#### center

> 在裁切框中是否显示中心控制器，也就是中间的小加号

- 类型：`Boolean`
- 默认：`true`

true | false
---------|----------
![image](center_true.jpg) | ![image](center_false.jpg)

#### highlight

> 是否高亮显示裁切框中的图片，查看源码后发现，也就是在上边添加了一个白色背景的dom元素，并且透明度设置为0.1看上去有点变亮的感觉

- 类型：`Boolean`
- 默认：`true`

true | false
---------|----------
![image](highlight_true.jpg) | ![image](highlight_false.jpg)


#### background

> 是否显示容器的网格背景，这个在`viewMode`模式设置成非3时可以看到效果

- 类型：`Boolean`
- 默认：`true`

true | false
---------|----------
![image](background_true.jpg) | ![image](background_false.jpg)

#### autoCrop

>是否自动创建裁切框，默认自动创建，如果有`data`属性按照`data`给定的数据创建，如果没有，按照图片的宽高比创建合适的裁切框
如果设置`false`, 不自动创建，在`dragMode`属性设置为：`crop`的情况下可以拖动创建裁切框，其他值不能拖动创建

- 类型：`Boolean`
- 默认：`true`


#### autoCropArea

>定义自动裁剪区域的大小，取0到1之间的数字。（百分比）。

- 类型：`Number`
- 默认：`0.8`(取图像的80%)



#### movable

> 定义图片是否可以拖动移动

- 类型：`Boolean`
- 默认：`true`


#### rotatable

>是否开启图片旋转功能，默认开启

- 类型: `Boolean`
- 默认: `true`

#### scalable

>是否开启图片缩放功能，默认开启

- 类型: `Boolean`
- 默认: `true`

#### zoomable

>是否开启图片可缩放功能，默认开启，如果关闭后，鼠标滚轮，和触摸放大缩小将不可用

- 类型: `Boolean`
- 默认: `true`

#### zoomOnWheel

>是否开启通过鼠标滚轮缩放图片功能，默认开启，需要在`zoomable`属性设置为`true`情况下才可用

- 类型: `Boolean`
- 默认: `true`

#### zoomOnTouch

>是否开启通过拖动触摸缩放图片功能，默认开启，需要在`zoomable`属性设置为`true`情况下才可用

- 类型: `Boolean`
- 默认: `true`

#### wheelZoomRatio

>定义使用鼠标滚轮缩放的时候缩放的比例值，默认是`0.1`，表示滚动滑轮一下缩小或放大图片的`10%`

- 类型: `Number`
- 默认: `0.1`


#### cropBoxMovable

>是否开启裁切框可拖动，默认开启表示可以移动裁切框

- 类型: `Boolean`
- 默认: `true`


#### cropBoxResizable

>是否开启裁切框可调整大小，默认开启表示可以调整裁切框大小，如果设置为`false`将不显示可拖动缩放句柄

- 类型: `Boolean`
- 默认: `true`

#### toggleDragModeOnDblclick

>是否开启双击裁切框后可以从新创建裁切框功能，如果设置为`true`表示开启，可以双击裁切框后，在图片上拖动从新创建新的裁切框，再次双击关闭。

- 类型: `Boolean`
- 默认: `true`


#### minContainerWidth

>表示默认容器的最小宽度，默认最小宽度是200像素。

- 类型: `Number`
- 默认: `200`


#### minContainerWidth

>表示默认容器的最小高度，默认最小宽度是100像素。

- 类型: `Number`
- 默认: `100`

#### minCanvasWidth

>表示默认画布（图片容器）的最小宽度，默认最小宽度是0像素。

- 类型: `Number`
- 默认: `0`

#### minCanvasHeight

>表示默认画布（图片容器）的最小高度，默认最小高度是0像素。可以大于容器高度

- 类型: `Number`
- 默认: `0`


#### minCropBoxHeight

>表示可改变裁切框的最小高度，默认最小高度是0像素。当设置了`aspectRatio`属性，应该按照此属性的比例计算高度，高度可能会小于此值

- 类型: `Number`
- 默认: `0`

#### minCropBoxWidth

>表示默认裁切框的最小宽度，默认最小宽度是0像素。当设置了`aspectRatio`属性，应该按照此属性的比例计算宽度，宽度可能会小于此值

- 类型: `Number`
- 默认: `0`

#### ready

> 当实例化对象后触发的方法(只执行一次)

- 类型: `Function`
- 默认: `null`

#### cropstart

> 当裁切开始时触发的事件，包括开始创建裁切框，移动裁切框开始，移动图片开始等都会触发此方法，滚轮放大缩小图片不执行此方法

- 类型: `Function`
- 默认: `null`

#### cropmove

> 当裁切开始拖动时触发的事件，滚轮放大缩小图片不执行此方法

- 类型: `Function`
- 默认: `null`

#### cropend

> 当裁切结束时触发的事件，就是鼠标抬起触发的事件

- 类型: `Function`
- 默认: `null`

#### crop

> 当裁切时触发的事件，包括改变裁切框大小，移动裁切框，移动图片，滚轮放大缩小图片等，都执行此方法，此方法中的的`event`参数里边包括裁切的数据

- 类型: `Function`
- 默认: `null`

```javascript
options:{
  crop: function(event) {
    console.log("crop-event", event);
    console.log(event.detail.x);
    console.log(event.detail.y);
    console.log(event.detail.width);
    console.log(event.detail.height);
    console.log(event.detail.rotate);
    console.log(event.detail.scaleX);
    console.log(event.detail.scaleY);
  }
}
```

#### zoom

> 当通过鼠标滚轮，或者触摸缩小放大图片的时候执行此方法

- 类型: `Function`
- 默认: `null`

### 方法(methods)

> 由于加载图像时存在异步过程，因此应在`ready`之后调用大多数方法，`setAspectRatio`，`replace`和“`destroy`除外。
如果方法没有被设置返回任何值，那么它会返回一个cropper的实例 因此多个方法可以使用链式写法

#### crop()

> 手动显示裁切框，在实例化裁切器的时候我们可以先把`autoCrop`设置成`false`不显示裁切框，然后通过手动调`crop`方法来显示裁切框

```javascript
/* 两种方法手动显示裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
cropper.crop(); //调用实例对象上的crop方法
// 通过dom元素的jquery方法调用，crop是要执行的方法名，后边可以添加参数
$image.cropper('crop');
```

#### clear()

> 手动隐藏裁切框

```javascript
/* 两种方法手动移除裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
cropper.clear(); //调用实例对象上的clear方法
// 通过dom元素的jquery方法调用，clear是要执行的方法名，后边可以添加参数
$image.cropper('clear');
```

#### reset()

> 重置裁切框，从新初始化裁切框

```javascript
/* 两种方法手动初始化裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
cropper.reset(); //调用实例对象上的reset方法
// 通过dom元素的jquery方法调用，reset是要执行的方法名，后边可以添加参数
$image.cropper('reset');
```

#### replace(url[, hasSameSize])

> 从新更换裁切器的图片，替换图像的src并重建裁剪器

- `url`:
  - 类型：`String`
  - 新图片的地址路径

- `hasSameSize`:
> `false`：替换图片地址，并从新创建裁切器；`true`：不重新创建裁切器只更换图片地址；
如果新图像的大小与旧图像的大小相同，则设置为`true`将不会重建裁剪器，而只会更新所有相关图像的URL。这可以用于应用过滤器。

  - 类型：`Boolean`
  - 默认：`false`

```javascript
/* 两种方法手动初始化裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
cropper.replace('800-7.jpg'); //调用实例对象上的replace方法
// 通过dom元素的jquery方法调用，replace是要执行的方法名，后边可以添加参数
$image.cropper('replace', '800-7.jpg', true);
```

#### disable()
> 锁定裁切器使裁切器不可用，包括裁切器的各种方法都不能用，`destroy()`方法除外。调用方式和上边方法调用方式相同。

#### enable()
> 解除锁定裁切器使裁切器从新可用，包括裁切器的各种方法都恢复可用。

#### destroy()
> 销毁当前的裁切器，并移除所有裁切器的dom元素，只留下原始图片。销毁后所有方法不可再用。

#### move(offsetX[, offsetY])
> 移动图片方法，调用此方法来左右，或者上下移动指定像素位。调用这个方法移动完毕后，会调用`crop`参数的方法

- `offsetX`
> 水平方左右移动指定大小，单位像素（px）。取正直图片向右移动，取负值图片向左移动

  - 类型：`Number`

- `offsetY`
> 垂直方上下移动指定大小，单位像素（px）。取正直图片向下移动，取负值图片向上移动

  - 类型：`Number`

#### moveTo(x[, y])
> 移动图片到指定位置，调用此方法来左右，或者上下移动图片到指定位置，调用这个方法移动完毕后，会调用`crop`参数的方法

- `x`
> 水平方左右移动图片到指定位置，单位像素（px）。取正直图片向右移动，取负值图片向左移动

  - 类型：`Number`

- `y`
> 垂直方上下移动图片到指定位置，单位像素（px）。取正直图片向下移动，取负值图片向上移动

  - 类型：`Number`

#### zoom(ratio)
> 图片缩放比。调用这个方法缩放完毕后，会调用`crop`参数的方法，和`zoom`参数的方法

- `ratio`
> 图片的缩放比例，-1 - 0 - 1之间的数字取正直图片放大，取负值图片缩小

  - 类型：`Number`

#### zoomTo(ratio,[, pivot])
> 图片缩放到指定比例大小。调用这个方法移动完毕后，会调用`crop`参数的方法，和`zoom`参数的方法

- `ratio`
> 图片的缩放比例，大于0的数字，表示缩放的倍数

  - 类型：`Number`

- `pivot`
> 图片缩放的时候设置的缩放中心点，基于裁剪容器的左上角

  - 类型：`Object`
  - 格式：`{ x: Number, y: Number }`

```javascript
/* 两种方法手动初始化裁切框 */
const $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
const cropper = $image.data('cropper');
const containerData = cropper.getContainerData();//获取裁切器的宽高等数据
cropper.zoomTo(.5, {
  // 已裁切器宽度10%的位置作为x轴坐标
  // 已裁切器高度10%的位置作为y轴坐标
  // 已得到的x，y作为缩放的中心点开始缩放
          x: containerData.width / 10,
          y: containerData.height / 10,
        });
// 通过dom元素的jquery方法调用，zoomTo是要执行的方法名，后边可以添加参数
$image.cropper('zoomTo', .5, {
          x: containerData.width / 10,
          y: containerData.height / 10,
        });
```
#### rotate(degree)
> 图片旋转的方法。调用这个方法旋转完毕后，会调用`crop`参数的方法，此方法用到了css3中的2D旋转属性`transform`，需要浏览器支持css3

- `degree`
> 图片的旋转角度，取正直图片顺时针旋转，取负值图片逆时针旋转

  - 类型：`Number`

#### rotateTo(degree)
> 图片旋转到指定角度方法。调用这个方法旋转完毕后，会调用`crop`参数的方法，此方法用到了css3中的2D旋转属性`transform`，需要浏览器支持css3

- `degree`
> 图片的旋转角度，取正直图片顺时针旋转，取负值图片逆时针旋转

  - 类型：`Number`

#### scale(scaleX, [scaleY])
> 翻转图片的方法。调用这个方法旋转完毕后，会调用`crop`参数的方法，此方法需要把参数中的`scalable`值设置为真，此方法用到了css3中的2D旋转属性`transform`，需要浏览器支持css3

- `scaleX`
> 水平翻转图片，-1表示水平翻转，1不做任何处理，

  - 类型：`Number`

- `scaleY`
> 垂直翻转图片，-1表示垂直翻转，1不做任何处理

  - 类型：`Number`

#### scaleX(scaleX)
> 水平翻转图片，-1表示水平翻转，1不做任何处理，

  - 类型：`Number`
  - 默认：`1`

#### scaleY(scaleY)
> 垂直翻转图片，-1表示垂直翻转，1不做任何处理，

  - 类型：`Number`
  - 默认：`1`

#### getData([rounded])

> 获取最终裁切图片的信息

- 参数`rounded`
> 获取的值是否进行四舍五入, 取`true`表示进行

  - 类型：`Boolean`
  - 默认：`false`

- 返回值
> 输出最终裁切区域的位置和尺寸数据（基于原始图像的自然尺寸）。

  - 类型：`Object`
  - 特征：
    - `x`：裁剪区域的左偏移值
    - `y`：裁剪区域的上偏移值
    - `width`：裁切区域的宽度
    - `height`：裁剪区域的高度
    - `rotate`：图像的旋转角度
    - `scaleX`：应用于图像横坐标的比例因子，图片左右翻转量
    - `scaleY`：应用于图像纵坐标的比例因子，图片上下翻转量

![image](getData.jpg)

```javascript
/* 两种方法手动初始化裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
const getData = cropper.getData(); //调用实例对象上的getData方法
// 通过dom元素的jquery方法调用，getData是要执行的方法名，后边可以添加参数
const getData = $image.cropper('getData', true);
```
设置参数的返回值：

true | false
---------|----------
![image](getData_true.jpg) | ![image](getData_false.jpg)


#### setData(data)
> 设置裁切框的数据，然后根据传过去的数据从新定位裁切框的位置大小，调用这个方法设置完毕后会同时执行`crop`方法两遍

- 参数：
> 格式和`getData`方法返回的数据格式一样，可以传递一到多个值可选的值

  - 类型：`Object`

```javascript
/* 两种方法手动初始化裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
var setData1 = {x: 213.5, y: 215.3,width: 370,height: 370,rotate: 0,scaleX: 1,scaleY: 1};
var setData2 = {x: 213.5};
var setData3 = {x: 213.5,width: 370,height: 370};
cropper.setData(setData3); //调用实例对象上的setData方法
// 通过dom元素的jquery方法调用，setData是要执行的方法名，后边可以添加参数
$image.cropper('setData', setData1);
```

#### getContainerData()

> 获取裁切器容器的大小

- 返回值
  - 类型 `Object`
    - `width`：裁切器的宽度，也就是设置的Dom容器的宽度
    - `height`：裁切器的高度，也就是设置的Dom容器的高度

```javascript
//调用实例对象上的getContainerData方法
var containerData = cropper.getContainerData();
// 通过dom元素的jquery方法调用，getContainerData是要执行的方法名
var containerData = $image.cropper('getContainerData');
console.log(containerData);
```
![image](getContainerData.jpg)

#### getImageData()

> 获取图像的相关信息，包括大小，位置，缩放大小等和其他相关数据。

- 返回值
  - 类型 `Object`
    - `left`：图像的左偏移量
    - `top`：图像的上偏移量
    - `width`：图像当前的宽度
    - `height`：图像当前的高度
    - `naturalWidth`：图片的原始宽度
    - `naturalHeight`：图片的原始高度
    - `aspectRatio`：图像的高宽比
    - `rotate`：旋转图像的旋转角度
    - `scaleX`：图片X轴的翻转量
    - `scaleY`：图片Y轴的翻转量

```javascript
//调用实例对象上的getImageData方法
var getImageData = cropper.getImageData();
// 通过dom元素的jquery方法调用，getImageData是要执行的方法名
var getImageData = $image.cropper('getImageData');
console.log(getImageData);
```

![image](getImageData.jpg)


#### getCanvasData()

> 获取图像的相关信息，包括大小，位置，缩放大小等和其他相关数据。

- 返回值
  - 类型 `Object`
    - `left`：画布的左偏移量
    - `top`：画布的上偏移
    - `width`：画布的宽度
    - `height`：画布的高度
    - `naturalWidth`：画布的自然宽度（只读）
    - `naturalHeight`：画布的自然高度（只读）

```javascript
// 获取画布信息
var getCanvasData = cropper.getCanvasData();
// var getCanvasData = $image.cropper('getCanvasData');
console.log(getCanvasData);
```
![image](getCanvasData.jpg)



#### setCanvasData(data)
> 使用新数据更改画布（图像包装器）的位置和大小，调用这个方法设置完毕后会同时执行`crop`方法两遍

- 参数：
> 格式和`getCanvasData`方法返回的数据格式一样，可以传递一到多个值可选的值，更改是按照`viewMode`的参数值进行放大和缩小

  - 类型：`Object`

```javascript
/* 两种方法手动初始化裁切框 */
var $image = $('#image');
$image.cropper(options);
// 方法一通过实例化裁切器的dom元素上一个cropper实例来调用
var cropper = $image.data('cropper');
var setData1 = {left: 213.5, top: 215.3,width: 370,height: 370,naturalWidth: 0,naturalHeight: 1};
var setData2 = {left: 213.5};
var setData3 = {top: 213.5,width: 370,height: 370};
cropper.setCanvasData(setData3); //调用实例对象上的setCanvasData方法
// 通过dom元素的jquery方法调用，setCanvasData是要执行的方法名，后边可以添加参数
$image.cropper('setCanvasData', setData1);
```

#### getCropBoxData()

> 获取裁切框的相关信息，包括大小，位置，等相关数据。

- 返回值
  - 类型 `Object`
    - `left`：裁切框左偏移像素
    - `top`：裁切框的上偏移像素
    - `width`：裁切框的宽度
    - `height`：裁切框的高度

```javascript
// 获取画布信息
var getCropBoxData = cropper.getCropBoxData();
// var getCropBoxData = $image.cropper('getCropBoxData');
console.log(getCropBoxData);
```
![image](getCropBoxData.jpg)

#### setCropBoxData(data)
> 设置裁切框的位置和大小，调用这个方法设置完毕后会同时执行`crop`方法

- 参数：
> 格式和`getCropBoxData`方法返回的数据格式一样，可以传递一到多个值可选的值，更改是按照`viewMode`的参数值进行放大和缩小

  - 类型：`Object`

```javascript
// 设置裁切框大小和位置
setCropBoxData = {left: 10, top: 10, width: 100, height:20}
// cropper.setCropBoxData(setCropBoxData)
$image.cropper('setCropBoxData', setCropBoxData);
```

#### getCroppedCanvas()

> 获取裁切框的相关信息，包括大小，位置，等相关数据。

- 返回值
  - 类型 `Object`
    - `left`：裁切框左偏移像素
    - `top`：裁切框的上偏移像素
    - `width`：裁切框的宽度
    - `height`：裁切框的高度

```javascript
// 获取画布信息
var getCropBoxData = cropper.getCropBoxData();
// var getCropBoxData = $image.cropper('getCropBoxData');
console.log(getCropBoxData);
```
![image](getCropBoxData.jpg)

#### setAspectRatio(aspectRatio)

> 设置裁切框的裁切比例，参数需要为正数，调用这个方法设置完毕后会同时执行`crop`方法

- 参数
  - 类型：`Number`

#### setDragMode([mode])

> 设置裁切器的拖动模式，您可以通过双击裁剪器来切换“裁剪”和“移动”模式。

- 参数
  - 类型：`String`
  - 默认：`none`
  - 选项：`none`、`crop`、`move`

### 事件(Events)
> 可以通过给绑定了裁切器的Dom图片元素绑定事件，来执行一些方法，可以通过两种方式绑定，
1、通过jQuery的on绑定；
2、通过原生js的addEventListener方法绑定；

#### ready
> 当目标图像已加载且裁剪器实例已准备好运行时，将触发此事件。

- 类型：`Event`

```javascript
// 通过jquery绑定事件
$image.on('ready', function (event) {
  // 这里的事件是通过jquery处理的事件对象
  console.log(event);
});
// 通过js原生绑定
$image[0].addEventListener('ready', function (event) {
  // 这里的事件是原生js事件对象
  console.log(event);
});
```
#### cropstart
> 当裁剪开始，或裁剪框开始更改的时候触发此事件

执行方法后的`event`参数对象详细介绍

- event.detail.originalEvent 事件的详细信息
  - 类型：`Event`
  - 可能的事件类型：`mousedown`、`touchstart`、`pointerdown`
- event.detail.action 事件动作的详细信息
  - 类型：`Sting`
  - 可能的值：
    - `crop`：创建一个新的裁剪框
    - `move`：移动画布（图像包装器）
    - `zoom`：通过触摸放大/缩小画布（图像包装器）。
    - `e`：调整裁切框东侧的大小
    - `w`：调整裁切框西侧的大小
    - `s`：调整裁切框南侧的大小
    - `n`：调整裁剪框北侧的大小
    - `se`：调整裁切框东南侧的大小
    - `sw`：调整裁切框西南侧的大小
    - `ne`：调整裁切框东北的大小
    - `nw`：调整裁切框西北侧的大小
    - `all`：移动裁剪框（所有方向）

可以通过下列方式得到：

```javascript
  // 通过js原生绑定
  $image[0].addEventListener('cropstart', (event) => {
    console.log(event.detail.originalEvent);
    console.log(event.detail.action);
  });
  // 通过jquery绑定
  $image.on('cropstart', (event) => {
    console.log(event.detail.originalEvent);
    console.log(event.detail.action);
  });
```

#### cropmove
> 当移动或者更改裁剪框时候触发此事件

执行方法后的`event`参数对象详细介绍

- event.detail.originalEvent 事件的详细信息
  - 类型：`Event`
  - 可能的事件类型：`mousemove`、`touchmove`、`pointermove`
- event.detail.action 事件的详细信息和`cropstart`的一样

#### cropend

> 当停止移动或者停止更改裁剪框时候触发此事件

执行方法后的`event`参数对象详细介绍

- event.detail.originalEvent 事件的详细信息
  - 类型：`Event`
  - 可能的事件类型：`mouseend`、`touchend`、`pointerend`
- event.detail.action 事件的详细信息和`cropstart`的一样

#### crop

> 当画布或裁切框发生变化时触发。

执行方法后的`event`参数对象详细介绍

- event.detail 事件中的数据详细信息，和`getDate`方法得到的数据相同，，能够得到最终裁切区域的位置和尺寸数据（基于原始图像的原尺寸）。
  - 类型：`Object`
    - `x`：裁剪区域的左偏移值
    - `y`：裁剪区域的上偏移值
    - `width`：裁切区域的宽度
    - `height`：裁剪区域的高度
    - `rotate`：图像的旋转角度
    - `scaleX`：应用于图像横坐标的比例因子，图片左右翻转量
    - `scaleY`：应用于图像纵坐标的比例因子，图片上下翻转量

#### zoom
>裁剪器开始放大或缩小其画布（图像包装器）时，将触发此事件。

执行方法后的`event`参数对象详细介绍

- event.detail.originalEvent：

  - 类型： `Event`
  - 事件类型：`wheel`，`touchmove`。

- event.detail.oldRatio：

> 画布缩放前的旧（当前）比率
  - 类型： `Number`

- event.detail.ratio：

>画布缩放后的新（下一个）比例（canvasData.width / canvasData.naturalWidth）
  - 类型： `Number`

![image](zoom.jpg)
