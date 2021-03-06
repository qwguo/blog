---
title: JSON是一种轻量级数据交换格式
summary:
  - JSON全称JavaScript Object Notation，它基于 ECMAScript 的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。
  - 'JSON是一种数据格式，不是一种编程语言。虽然具有相同的语法形式，但 JSON 并不从属于 JavaScript。而且，并不是只有 JavaScript 才使用 `JSON`，毕竟JSON只是一种数据格式。很多编程语言都有针对 JSON 的解析器和序列化器'
drafts: false
p: JavaScript/JSON
date: 2020-06-10 23:09:05
categories:
tags:
poster: poster.png
---

# JSON

## 定义
> `JSON`是一种数据格式，不是一种编程语言。虽然具有相同的语法形式，但 JSON 并不从属于 JavaScript。而且，并不是只有 JavaScript 才使用 `JSON`，毕竟JSON只是一种数据格式。很多编程语言都有针对 JSON 的解析器和序列化器。

## 语法

JSON语法可以包含以下三种类型值：
1. 简单值：`Number`、`String`、`Boolean`、`null`，也就是javascript中的基本数据类型，但是他不支持`undefined`;
2. 对象：是一种复杂数据类型，表示的是一组无序的键值对儿。而每个键值对儿中的值可以是简单值，也可以是复杂数据类型的值
3. 数组：也是一种复杂的数据类型，表示的是一组有序的的值的列表，可以通过数组的索引值(索引从0开始)来访问其中的值，数组中的值可以是：简单值、对象或数组

## 综合案例
```javascript
{
    "title": "JavaScript",
    "authors": ["name1", "name2"],
    edition: 3,
    year: 2011,
    chapter:{
        grammar:['运算符','表达式'],
        ajax: {
            definition: 'ajax定义',
            user: 'ajax使用'
        }
    },
    appendix: null
}
```

## 说明

> JSON 中对象的属性名任何时候都必须加双引号，在书写JSON的时候如果忘了给对象属性名加双引号或者把双引号写成单引号都是常见的错误。同时在同一级中属性名不能重复必须是唯一的，JSON中不能使用注释符来标注
javascript中的json没有这么严格要求，可以不用给属性名添加双号，或者可以是单引号，但是必输要按照javascript命名规范来属性，同时如果同级内出现同样的属性名，后出现的会替换到先出现的


```javascript
{
    "name": '张三',
    'age': 30,  // 错误，键名不能用单引号
    sex: "男" // 错误，键名必须使用双号括起来
    age: 40, // 错误，出现了重复的键名
    "home": "河北", // 错误，JSON最后一个值后面不能有逗号
}
```

上面的代码如果是在JSON文件中是会报错的，只有第一行的定义是正确的，其他三行都错误，如果是javascript定义的对象，上面的写法不会报错。


## javascript中json提供的方法

在早期的javascript中解析JSON基本上只能用`eval()`函数来实现；而ECMAScript5对解析JSON的行为做了规范化，提供了全局的JSON对象可以通过JSON对象提供的方法轻松的解析和格式化JSON对象。

JSON对象包含两个方法: 用于解析 JavaScript Object Notation  (JSON) 的 parse() 方法，以及将对象/值转换为 JSON字符串的 stringify() 方法。除了这两个方法, JSON这个对象本身并没有其他作用，也不能被调用或者作为构造函数调用。

### stringify
> 用于将JSON对象转换成JSON字符串，可以通过额外的参数, 控制仅包含某些属性, 或者以自定义方法来替换某些key对应的属性值。

**语法：**


```javascript
JSON.stringify(value[, replace | [] [, space]])
```

**参数：**

1. `value`：将要序列化成字符串的对象或者数组的对象值。
2. `replace`：可选参数，如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为 null 或者未提供，则对象所有的属性都会被序列化；
3. `space`：可选参数，指定缩进用的空白字符串，用于美化输出；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串（当字符串长度超过10个字母，取其前10个字母），该字符串将被作为空格；如果该参数没有提供（或者为 null），将没有空格。

```javascript
var firstJson = {
  "a": 10,
  "b": 20,
  "c": 30,
  "20": 'aaa'
}
/* 把json转换成字符串 */
JSON.stringify(firstJson);
// {"20":"aaa","a":10,"b":20,"c":30}

/* 第二个参数是数组，根据数组提供的值和对象的键值做==对比返回存在此键值的值 */
JSON.stringify(firstJson, ['a', 20, 'x']);
// {"a":10,"20":"aaa"}  这个对比会进行类型转换

/* 第二个值时方法的时候 */
JSON.stringify(firstJson, function(key, value){
  // 先判断key是否为真因为第一次循环会把整个对象作为参数传入，键值为空，第二次开始遍历每个值
  if(key){
    // 为每个值加10
    value += 10;
  }
  return value;
});
// {"20":"aaa10","a":20,"b":30,"c":40}

/* 第三个参数 */
JSON.stringify(firstJson, null, 2);
/* {
  "20": "aaa",
  "a": 10,
  "b": 20,
  "c": 30
}*/
```

### toJSON
> _此方法并非是JSON中的方法_，如果一个被序列化的对象拥有 toJSON 方法，那么该 toJSON 方法就会覆盖该对象默认的序列化行为：不是该对象被序列化，而是调用 toJSON 方法后的返回值会被序列化

```javascript
/* 对象形式 */
var firstJson = {
  "a": 10,
  "b": 20,
  "c": 30,
  "20": 'aaa',
  toJSON: function(){
    return {'x':1, 'y':10};
  }
}
JSON.stringify(firstJson);
// {"x":1,"y":10}

/* 数组形式 */
var arr = [1, 2, 4, 'abc', true, 4.5, {a:10, b:20}];
// 可以在数组原型上添加toJSON方法。
Array.prototype.toJSON = function(){
    return 'arr';
}
// 可以在实例化对象中添加toJSON方法效果一样
/* arr.toJSON = function(){
    return 'arr';
} */
var getArrStr1 = JSON.stringify(arr);
// "arr"
```

### parse
> 用来解析由字符串描述的JavaScript值或对象。

**基本语法：**
```javascript
JSON.parse(text[, reviver])
```
**参数说明：**

1. `text`：必选，要被解析成 JavaScript 值的字符串，若传入的字符串不符合 JSON 规范，则会抛出 SyntaxError 异常。
2. `reviver`：可选，转换器，如果传入该参数(函数)，可以用来修改解析生成的原始值，调用时机在 parse 函数返回之前。

**示例：**
```javascript
/* 只传入一个要转换的值 */
// 可以使空对象字符串
JSON.parse('{}');              // {}
// 对象字符串
JSON.parse('{a:10, b:20}');   // SyntaxError 这里的键值必须使用单引号或者双引号括起来
// 对象字符串
JSON.parse('{"a":10, "b":20}');   // {a: 10, b:20}
// 可以是字符串正假值
JSON.parse('true');            // true
// 不可以直接使用字符串
JSON.parse('foo');             // SyntaxError错误
// 字符串需要引号括起来
JSON.parse('"foo"');           // "foo"
// 可以是数组
JSON.parse('[1, 5, "false", true]'); // [1, 5, "false", true]
// 可以是null值
JSON.parse('null');            // null
// 不能使用undefined
JSON.parse(undefined)         // SyntaxError错误
// 不能使用function
JSON.parse(function(){})         // SyntaxError错误

/* 传入递归函数 */
var getJSON = JSON.parse('{"a": 1, "b": "2","c": {"d": 4, "e": {"f": 6}},"g":null, "f":"hello"}', function (k, v) {
  console.log(k);  // 这里依次输出的顺序是：a, b, d, f, e, c, g, f ''
  if(typeof v == 'number'){  //这里通过遍历判断值是否为数字类型是进行处理并返回
    return v + 10;
  }
  if(k == "f"){ // 这里判断键值是否是f，如果是返回undefined，也就是删除此值
    return undefined;
  }
  // 默认返回
  return v;
});
console.log(getJSON);  // { a: 11, b: '2', c: { d: 14, e: { f: 16 } }, g: null }
```

1. 通过上边实例可以看出，我们在使用`parse`方法的时候必须传入正确的JSON支持的数据类型：JSON对象、数组、数值、字符串、布尔值和 空(null) 。

2. 当我们提供第二个值的时候，他会为每一个值执行一次这个方法，并且把键当做第一个参数，值当做第二个参数传入该函数，并且在函数内部进行一些处理，当我们想要排除一些指定的键值对的话我们可以返回undefined，就会删除该项。并且它的执行顺序是依次顺序执行，当遇到的是对象形式，先便利里边的值，然后再输出该对象的键值，也就是由内到外执行，最后便利整个对象并且把转换后的整体返回，这个和 `stringify` 中的`replace`方法刚好相反。
这里还需要主要的是在遍历的时候`reviver`函数内的this指向的是当前的对象，如果遇到的键值是一个对象，那么进入该对象遍历时，this会执行该键值的对象。

## 参考网站

1. https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
