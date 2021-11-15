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

## 数组的属性

### length

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

## 数组的静态方法

> 数组的静态方法是直接定义在`Array`上，并且通过`Array.`的方式进行调用

### Array.from()

> 从一个可迭代的元素对象中创建一个新数组，并且他是浅拷贝的

#### 语法：

```javascript
  Array.from(arrayLike[, mapFn[, thisArg]]);
```
#### 参数：
  - `arrayLike` 需要转行数组的可迭代的元素
  - `mapFun` 转换成数组后为数组每一项执行该函数并返回最新
  - `thisArg` 执行mapFn 的时候mapFn函数内部的`this`指向

#### 示例：

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

### Array.isArray()

  > 用于检测传递的参数是否是数组，它也是Array上的一个静态方法

#### 语法

```javascript
Array.isArray(obj)
```
`obj`：需要检测的对象

如果是数组返回 `true` 否则返回 `false`

#### 示例
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

#### 兼容写法

```javascript
// 判断Array类上有没有isArray静态方法
if(!Array.isArray){
  Array.isArray = function(arg){
    // 通过是用Object.prototype.toString.call的方式可以得到对象的具体是什么类型
    return Object.prototype.toString.call(arg) === '[object Array]';
  }
}
```


### Array.of()

> 该方法是用来创建一个给定参数的新数组，和`new Array()`类似，唯一的区别是解决了传递一个整正数参数的时候创建非想要的结果的问题

#### 语法

```javascript
Array.of(element0[, element1[, ...[, elementN]]])
```

#### 示例

```javascript
var newArr_1 = new Array(7);
console.log(newArr_1);
//(7) [空属性 × 7]
var newArr_2 = Array.of(7);
console.log(newArr_2);
// [7]
```

#### 兼容写法

```javascript
if(!Array.of){
  Array.of = function(){
    return Array.prototype.slice.call(arguments);
  }
}
```


## 数组原型上的方法

### array.at()

> 数组的`at()`方法是用来访问数组中的元素，和我们正常访问数组元素使用的`array[index]`效果一样，唯一的区别是at可以传递一个负数，表示从数组最后边向前查找

#### 语法示例：
```javascript
let array_1 = [10, 5, 'apple', 'banner', 'orange', 'pear'];
console.log(array_1.at(2));
// apple
console.log(array_1.at(-6));
// orange
```

#### 兼容写法

```javascript
// 兼容写法
if(!Array.prototype.at){
  Array.prototype.at = function(index) {
    // 通过判断传过来的索引是否小于0，如果小于0，就用数组当前的length 加上索引值，就能得到从后向前的查找效果
    index = index < 0 ? this.length + index : index;
    return this[index];
  }
  console.log(array_1.at(-7));
}
```

### array.concat()

> `concat`方法，合并两个数组或多个数组，生成一个新数组, 该方法并不会改变任何一个原数组

#### 语法

```javascript
array.concat(array_2, array_3, array_4,...,array_n);

// array，可以是一个空数组，或者是要合并的数组的其中一个
// 参数：为一个或多个数组，或者是任意类型的值
```

#### 示例

```javascript
var number_arr = [10, 20, 5, 8, 12, 30];
var fruit_arr = ['apple', 'banner', 'orange', 'pear'];
var animal_arr = ['dog', 'cat', 'sheep', 'chicken', 'horse', 'cow'];

let concat_arr = number_arr.concat(fruit_arr, animal_arr);
//合并后的数组: (16) [10, 20, 5, 8, 12, 30, 'apple', 'banner', 'orange', 'pear', 'dog', 'cat', 'sheep', 'chicken', 'horse', 'cow']
let concat_str_arr = [].concat('new_val', 100, undefined, null, NaN, {a:10}, fruit_arr);
// (10) ['new_val', 100, undefined, null, NaN, {…}, 'apple', 'banner', 'orange', 'pear']
```

### array.copyWithin

> 复制数组中的某部分内的数据到另外某个部分，此方法不会改变原数组的长度,但是会改变原数组

#### 语法
```javascript
array.copyWithin(target, start, end)
```

#### 参数说明：

- `target`: 必填要传递的参数，表示目标位置，取值范围：必须是整数。如果取值为0的话，如果不传不执行任何操作
- `start`：要拷贝的数据的开始索引值，可以是负数，如果为负数那么就从数组末尾开始计算，可以用length + start，如果不传默认从数组第一个值开始到目标位置
- `end`: 要拷贝的数组的结束索引，并不包括该索引下的值；
#### 示例

```javascript

let arr_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'].copyWithin(2);
// (7) ['a', 'b', 'a', 'b', 'c', 'd', 'e']
let arr_2 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'].copyWithin(3, 4);
// (7) ['a', 'b', 'c', 'e', 'f', 'g', 'g']
let arr_3 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'].copyWithin(1, 4, 6);
// (7) ['a', 'e', 'f', 'd', 'e', 'f', 'g']
let arr_4 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'].copyWithin(-5, -2, -1);
// (7) ['a', 'b', 'f', 'd', 'e', 'f', 'g']
let arr_5 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'].copyWithin(-5, -1, 2);
// (7) ['a', 'b', 'c', 'd', 'e', 'f', 'g']
```

### array.entries()

> 生成一个新的Array Iterator对象迭代器，该对象里已键值对的形式保存了数组的所有项

#### 语法
```javascript
array.entries()
```

#### 示例

```javascript
let arr_1 = ['a', 'b', 'c'];
let en_array = arr_1.entries();
/*Array Iterator {}
  __proto__:Array Iterator
  next:ƒ next()
  Symbol(Symbol.toStringTag):"Array Iterator"
  __proto__:Object
*/
// 我们这里可以调用next方法来输出数组中的每一项
en_array.next();
/*{value: Array(2), done: false}
          done:false
          value:(2) [0, "a"]
           __proto__: Object
*/
// iterator.next()返回一个对象，对于有元素的数组，
// 是next{ value: Array(2), done: false }；
// next.done 用于指示迭代器是否完成：在每次迭代时进行更新而且都是false，
// 直到迭代器结束done才是true。
// next.value是一个["key","value"]的数组，是返回的迭代器中的元素值。

// 使用for of 形式输出
for(i of en_array){
  console.log(i);
}
// (2) [1, 'b']
// (2) [2, 'c']
// 由于上边调用过一次next方法，所以这个时候在执行for of 就会从next的下一个开始循环
// 其中i是每一项的数组
```


### array.every()

> 迭代数组中的每一个元素，并且为数组中的每一个元素执行以下回调方法判断是否符合给定的条件，只有数组的所有元素都满足条件`every`方法返回`true`，如果有一个不满足就返回`false`，ie9以上支持

#### 语法

```javascript
array.every(callBack(element, index, array), this)
```

#### 参数

- `callBack`：为数组项中的每一项执行的回调函数
  - `element`: 循环数组中的每一项
  - `index`: 当前数组项的下标
  - `array`: 当前的循环你数组
- `this`: 回调函数内部的this指向,如果是箭头函数的情况下这里传入的this并不会改变，callBack中的this执行的是window

#### 示例
```javascript
let array_1 = [20, 3, 15, 40, 2, 50, 70];
array_1.every(function(v, i, arr){
  return v > 10;
});
// false
let mark_2 = array_1.every(function(v, i, arr){
  return v > 1;
});
// true

// 这里需要说明
let mark_3 = array_1.every(function(v, i, arr){
  console.log(i, v);
  if(i === 0){
    // 当我们在遍历的时候动态给数组增加元素的时候，every的回调函数并不会执行新增加的元素
    arr.push(100);
    // 当我们修改已经存在的元素的时候，或者删除某个元素的时候，every的回调函数会拿到新修改的值
    arr.splice(1, 1, 60)
  }
  return v > 1;
});
console.log(mark_3);
// true
```

#### 兼容写法

```javascript
Array.prototype.every = function(callBack, thisArg){
  let arr = this;
  let leg = arr.length;
  for(let i = 0; i < leg; i++){
    if(!callBack.call(thisArg, arr[i], i, arr)){
      return false;
    }
  }
  return true;
}
```

### array.fill

> 用某个值填充数组从开始到结束的所有项，会更改原数组，但是不会更改数组的长度，IE浏览器暂不支持

#### 语法

```javascript
array.fill(value, start, end);
```
#### 参数

- `value`：需要填充的值，可以是任意值，如果不传入，那么取值是undefined
- `start`：开始填充的位置必须是整数, 可选参数，如果不传默认从第一个值开始, 如果是负数的话，将要从后往前查找相当于`array.length + start`
- `end`：结束填充的位置必须是整数，可选参数如果不传表示到数组的最后一个值, 规则同start相同


#### 示例

```javascript
let arr = ['a', 'b', 'c', 'd'];
[].concat(arr).fill();
// (4) [undefined, undefined, undefined, undefined]，不传任何参数，将把数组的所有项替换成undefined
[].concat(arr).fill(10);
// (4) [10, 10, 10, 10]，值传入第一个值将把该值替换到所有的数组项中
[].concat(arr).fill(10, 2);
// (4) ['a', 'b', 10, 10]，只传入两个值，前边的表示替换后的值，然后从start开始到数组末尾
[].concat(arr).fill(10, 0, 2);
//(4) [10, 10, 'c', 'd']，把数值10替换到数组从第一项开始到第二项的项目，不包括第三个
[].concat(arr).fill(3, -2, -1);
//(4) ['a', 'b', 3, 'd']，把数值3替换到从 array.length(4) + -2 = 2，到array.length(4) + -1 = 3的位置,
[].concat(arr).fill([3, 10], 1, 4);
// (4) ['a', Array(2), Array(2), Array(2)] // 替换的值可以是数组
[].concat(arr).fill(NaN, 1, 4);
// (4) ['a', NaN, NaN, NaN]
let j = {a: 10};
[].concat(arr).fill(j, 1, 4);
// (4) ['a', {…}, {…}, {…}]， 这里替换的下标为第1个到下标4个的项，因为这里替换的是对象所以他们都指向一个对象j, 当改变j的内部数据是，替换的项会跟随变化
j.a = 30;
```
#### 兼容写法
```javascript
if(!Array.prototype.fill){
  Array.prototype.fill = function(){
    let arr = this;
    let len = arr.length;
    let val = arguments[0];
    let start = arguments[1];
    let end = arguments[2];
    if(start){
      if(start < 0)
      start = len + start;
    }else{
      start = 0
    }
    if(end){
      if(end < 0){
        end = len + end;
      }
    }else{
      end = len;
    }
    while(start<end){
      arr[start] = val;
      start++;
    }
    return arr;
  }
}
```

### array.filter()

> 数组过滤器，循环数组中的每一项，然后为每一项调用回调函数进行判断，然后返回符合条件的项，生成新数组, IE9以上支持

#### 语法

```javascript
let newArray = array.filter(callBack(element, index, array), thisArg);
```

#### 参数

- `callBack`：为每个元素执行的回调函数，回调函数中进行判断，如果条件成立返回true，保留当前项，如果条件不成立返回false排除当前项，如果没有找到匹配的项返回空数组
  - `element`：循环迭代的每一项
  - `index`：当前项的下标索引值
  - `array`：循环的当前数组
- `thisArg`：用于改变回调函数中的this指向

#### 示例

```javascript
let array = [10, 20, 5, 3, 80, 6, 1, 12];
let newArray_1 = array.filter((element, index, arr)=>{
  return element > 10;
});
// (3) [20, 80, 12]
let newArray_2 = array.filter((element, index, arr)=>{
  return index%2;
});
// (4) [20, 3, 6, 12]

let array_2 = ['apple', 'banana', 'grapes', 'mango', 'orange'];
let fun = function(e, i, arr){
  return e.indexOf('ap') != -1;
};
let newArray_3 = array_2.filter(fun);
// (2) ['apple', 'grapes']
```

#### 兼容写法

```javascript
if(!Array.prototype.filter){
  Array.prototype.filter = function(callBack, thisArg){
    if(typeof(callBack) !== 'function'){
      throw new TypeError(callBack + ' is not a function');
      return;
    }
    let newArr = [];
    let arr = this;
    let len = arr.length;
    let i = 0;
    while(i<len){
      if(callBack.call(thisArg, arr[i], i, arr)){
        newArr.push(arr[i]);
      }
      i++;
    }
    return newArr;
  }
}
```

### array.find()

> 循环迭代数组中的项目，并且提供一个函数作为检测函数，如果数组中有一项满足检测条件就返回`true`并且直接退出循环，如果没找到返回`undefined`

#### 语法

```javascript
array.find(callBack(element, index, arr), thisArg);
```
#### 参数

- `callBack`：循环迭代为每个元素执行的回调函数，回调函数中进行判断，如果条件成立返回当前项并且结束循环，只要循环中找到一个匹配项立马结束循环,如果没有匹配的项返回undefined
  - `element`：循环迭代的每一项
  - `index`：当前项的下标索引值
  - `array`：循环的当前数组
- `thisArg`：用于改变回调函数中的this指向

#### 示例

```javascript
let array = [10, 20, 5, 3, 80, 6, 1, 12];
console.log('原数组：', array);
let newArray_1 = array.find((element, index, arr)=>{
  return element > 60;
});
// 80
let newArray_2 = array.find((element, index, arr)=>{
  return index%2;
});
// 20
let array_2 = ['apple', 'banana', 'grapes', 'mango', 'orange'];
let fun = function(e, i, arr){
  return e.indexOf('ap') != -1;
};
let newArray_3 = array_2.find(fun);
// apple
```
