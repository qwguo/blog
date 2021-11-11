---
title: arrayLearn
summary:
  - '数组用于在单个变量中存储多个值。数组是一个特殊变量，一次可以包含多个值，并且还可以通过引用索引号来访问这些值'
  - 数组是一种类列表对象，它的原型中提供了遍历和修改元素的相关操作。JavaScript 数组的长度和元素类型都是非固定的。因为数组的长度可随时改变，并且其数据在内存中也可以不连续，所以 JavaScript 数组不一定是密集型的，这取决于它的使用方式。
drafts: false
p: Javascript/ArrayLearn
date: 2021-11-08 08:32:47
categories: [JavaScript]
tags: [JavaScript, Array]
poster:
---

## 创建数组的方式

### 使用字面量形式创建

```javascript
  var array_1 = ['apple', 'banner', 'orange', 'pear', 'Mongo'];
```
### 使用关键字创建

```javascript
  // 当关键字括号内有多个已逗号分开的项的话，代表创建数组的项
  var array_1 = new Array('apple', 'banner', 'orange', 'pear', 'Mongo');
  // 当关键字括号内只有一个值，并且是正数的话，表示创建一个有n个为空的数组项
  var array_2 = new Array(10);
  // 上边的代码创建了一个有10个空项的数组

  var array_3 = new Array(-10);
  var array_4 = new Array(4294967296);
  // Uncaught RangeError: Invalid array length
  // 上边的两种定义数组都会无效的数组长度错误，
  // 如果使用 new 关键字创建数组的话，并且括号中只有一个值，且值为数值类型的情况下，取值范围是：
  // 0 到4294967295 也就是2的32次方 = 4294967296 -1的正数

```
一般建议使用字面量形式创建数组，原因是字面量形式创建数组简单，并且不会出现`array_2`的那种情况
### 访问数组元素, 给数组项赋值

```javascript
  // 访问数组元素
  var firstItem = array_1[0]; // apple
  // 给数组的元素赋值
  array_1[0] = 20;
```

### 数组的属性

#### length

`length`是Array实力中的一个属性，用来返回或者设置一个数组的元素个数，改值是一个`32-bit`位的整正数。并且此值总是数组最高位的下标+1

```javascript
var array_1 = ['apple', 'banner', 'orange', 'pear', 'Mongo'];
var sum = array_1.length; // 5
```

我们也可以通过设置该属性值得方式来截断或者增加数组的项

```javascript
var array_1 = ['apple', 'banner', 'orange', 'pear', 'Mongo'];
// 当我们把数组的length属性设置成小于数组个数的值时，会把下标大于该值的所有元素截取掉，直接改变当前数组
array_1.length = 3; // (3) ['apple', 'banner', 'orange']
// 当我们把数组的length属性设置成大于数组个数的值时，会自动往数组后边追加n个空项。
array_1.length = 10; // (10) ['apple', 'banner', 'orange', 空属性 × 7]

// 如果把length 设置成大于 2的32方，小于0，并且是非正整数的值都会报错
lengthArray_1.length = 4294967296;
lengthArray_1.length = -1
```

### 数组的静态方法

数组的静态方法是直接定义在`Array`上，并且通过`Array.`的方式进行调用

#### Array.from()

> 从一个可迭代的元素对象中创建一个新数组，并且他是浅拷贝的

**语法：**

```javascript
  Array.from(arrayLike[, mapFn[, thisArg]]);
```
**参数：**
  - `arrayLike` 需要转行数组的可迭代的元素
  - `mapFun` 转换成数组后为数组每一项执行该函数并返回最新
  - `thisArg` 执行mapFn 的时候mapFn函数内部的`this`指向

**示例：**

##### 基本用法：
```javascript
function fn(){
  // 使用Array.from将参数(arguments)类数组转换成真正的数组
  return Array.from(arguments);
}
let newArr = fn('apple', 'banner', 'orange', 'pear', 'Mongo');
// (5) ['apple', 'banner', 'orange', 'pear', 'Mongo']

// 把获取dom节点的集合类数组改成数组，由于获取dom得到的是一个nodeList的类数组的dom集合
let domNodeList = document.querySelectorAll('span');
// 原始数据： NodeList(10) [span, span, span, span, span, span, span, span, span, span]
let domArr = Array.from(domArr);
// 转换后的数据： (10) [span, span, span, span, span, span, span, span, span, span]

// 由于字符串页带有length属性，也是可以进行迭代的，所以from可以把字符串的每个个字符单独分开转换成数组
let str = Array.from('hello world');
// (11) ['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']

// 我们还可以把带length属性的对象转换成数组
let parson = {name: 'qwguo', sex: '男', age: 30, length: 3};
Array.from(parson)
// (3) [undefined, undefined, undefined]
// 这里转换后的值是三个undefined项的数组，是因为上边的person对象length值为3，但是他并没有0-2的键值的数据
let parson2 = {0: 'qwguo', 1: '男', 2: 30, length: 3};
Array.from(parson2);
// (3) ['qwguo', '男', 30]
// parson2对象设置了length键值，并且把每一项以数组为键值存储，这样就可以通过from方法转换成数组类型


// ES6新增的数据类型，Set数据类型，Map数据类型，本身就是可以迭代的，所以可以调用from方法将其转换成数组
// Set数据类型转换成数组
var newSet = new Set(['foo', 'bar', 'baz', 'foo'])
console.log('原set数据：', newSet);
// 原set数据：Set(3) {'foo', 'bar', 'baz'}
// 因为本身ES6的Set类型的数据项具有唯一性，所以会把重复的数据剔除掉
console.log('把set数据转换成数组：', Array.from(newSet));
// (3) ['foo', 'bar', 'baz']

// Map数据类型转换成数组
const mapper = new Map([['1', 'a'], ['2', 'b']]);
console.log('map元数据:', mapper);
 // map元数据: Map(2) {'1' => 'a', '2' => 'b'}
console.log('map数据转换成数组', Array.from(mapper));
// (2) [Array(2), Array(2)]

// 可以通过Map的values 、keys方法分别得到键和值的数组集合
console.log('map.values方法只转换值为数组：', Array.from(mapper.values()));
// (2) ['a', 'b']
console.log('map.values方法只转换键为数组：', Array.from(mapper.keys()));
// (2) ['1', '2']
```

##### mapFun方法使用：

```javascript
function fn2(){
  // 把函数接收的参数转换数组
  return Array.from(arguments, (v, i)=>{
    return v = v + '_++';
  });
}
let newArr2 = fn2('apple', 'banner', 'orange', 'pear', 'Mongo');
console.log('把函数参数转换成数组：', newArr2);
// (5) ['apple_++', 'banner_++', 'orange_++', 'pear_++', 'Mongo_++']

// 我们可以利用对象有length转换成数组的特性，在运行map方法生成一个0-n的数值序列数组
let numArr = Array.from({length: 5}, (v, i) => i);
    //(5) [0, 1, 2, 3, 4]
```
mapFun类似于数组的map方法，相当于把转换后的数组调用一遍map方法

通过上边的知识我们可写一个生成数字数组的生成器

```javascript
function numRange(start, end, step){
  return Array.from({length: (end - start) / step + 1}, (v, i) => start + i * step);
}
console.log(numRange(1, 10, 1));
// (10) [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(numRange(1, 10, 4));
// (3) [1, 5, 9]

// 生成A-Z的字母数组，先通过上边的方法获取A-Z之间的charCodeAt码数组，然后在使用数组的map进行处理成对象的字母返回
numRange('A'.charCodeAt(), 'Z'.charCodeAt(), 1).map(function(v, i){return String.fromCharCode(v)})
```

##### 第三个参数是用来改变第二个参数的map方法调用时候的内部this执行的参数
```javascript
function fn3(){
  // 把函数接收的参数转换数组
  let y = {z: 20};
  return Array.from(arguments, function(v, i){
    console.log(this);
    return v = v + '_++';
  });
}
// 这种情况调用fn3的话，map内部的this指向的是window，因为是在window下调用的该
let newArr3 = fn3('apple', 'banner', 'orange', 'pear', 'Mongo');
//如果通过这种方式调用this指向的还是window，虽然这调用fn3方法时改变了this，但是map方法的执行并没有改变this
let x = {a: 10, b: 20};
fn3.call(x, 'apple', 'banner', 'orange', 'pear', 'Mongo');

// 把上边的方法改成如下代码
function fn4(){
  // 把函数接收的参数转换数组
  let y = {z: 20};
  return Array.from(arguments, function(v, i){
    console.log(this);
    return v = v + '_++';
  }, this);
}
let x = {a: 10, b: 20};
fn4.call(x, 'apple', 'banner', 'orange', 'pear', 'Mongo');
// 这个时候调用map内部的this就指向了调用该方法的this了，我们也可以传入上边的y把this指向改变为y对象

// 这里还需要注意的是，如果把map方法换成箭头函数的话，由于箭头函数没有this,所以内部的this执行调用该方法的this，就相当于上边第三个参数传this值
```

#### Array.isArray()

> 用于检测传递的参数是否是数组，它也是Array上的一个静态方法

##### 语法

```javascript
Array.isArray(obj)
```
`obj`：需要检测的对象

如果是数组返回 `true` 否则返回 `false`


```javascript
let objArr = {0: 'qwguo', 1: '30', 2: '男', length: 3}
console.log(Array.isArray(objArr));
// false
console.log(Array.isArray(Array.from(objArr)));
// true
let spanDom = document.querySelectorAll('span');
console.log(Array.isArray(spanDom));
// false
let arr = [10, 20, 30];
console.log(Array.isArray(arr));
// true
```


#### Array.of()

> 该方法是用来创建一个给定参数的新数组，和new Array()类似，唯一的区别是解决了传递一个整正数参数的时候创建非想要的结果的问题
