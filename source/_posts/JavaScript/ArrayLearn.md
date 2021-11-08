---
title: arrayLearn
summary:
  - '数组用于在单个变量中存储多个值。数组是一个特殊变量，一次可以包含多个值，并且还可以通过引用索引号来访问这些值'
  - 数组是一种类列表对象，它的原型中提供了遍历和修改元素的相关操作。JavaScript 数组的长度和元素类型都是非固定的。因为数组的长度可随时改变，并且其数据在内存中也可以不连续，所以 JavaScript 数组不一定是密集型的，这取决于它的使用方式。
drafts: false
p: Javascript/ArrayLearn
date: 2021-11-08 08:32:47
categories:
tags:
poster:
---

## 创建数组的方法

### 使用字面量形式创建

```javascript
  var array_1 = ['apple', 'banner', 'orange', 'pear', 'Mongo'];
```
### 使用关键字创建

```javascript
  // 当关键字括号内有多个已逗号分开的项的话，代表创建数组的项
  var array_1 = new Array('apple', 'banner', 'orange', 'pear', 'Mongo');
  // 当关键字括号内只有一个值，并且是正数的话，表示创建一个有n个为空的数组
  var array_2 = new Array(10);
  // 这里创建了一个有10个空项的数组
```
###
