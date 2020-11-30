# 数据类型概述

## 简介

JavaScript 语言中的每一个值，都属于某一种数据类型。 JavaScript 的数据类型，共有六种。

- 数值（number）：整数和小数（比如`1`和`3.14`）
- 字符串（String）：文本（比如`Hello World`）
- 布尔值（Boolean）：表示真伪的两个特殊值，即`true`（真）和`false`（假）
- `undefined`：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何职
- `null`：表示空值，即此处的值为空
- 对象（object）：各种值组成的集合


对象是最复杂的数据类型，又可以分为三个子类型

- 狭义的对象（object）
- 数组（array）
- 函数（function） 函数式编程

## typeof 运算符

JavaScript 有三种方法，可以确定一个值到底是什么类型

- `typeof`运算符
- `instanceof`运算符
- `Object.prototype.toString`方法

`typeof`运算符返回一个值的数据类型

数值、字符串、布尔值分别返回`number`、`string`、`boolean`

```javascript
typeof 123 // "number"
typeof '123' // "string"
typeof false // "boolean"
```

函数返回`function`

```javascript
function f(){}
typeof f  // "function"
```

`undefined`返回`undefined`

```javascript
typeof undefined 
// "undefined"
```

利用这一点，`typeof`可以用来检查一个没有声明的变量，而不报错

```javascript
v
// ReferenceError: v is not defined

typeof v
// "undefined"
```

实际编程中，通常用在判断语句
```javascript
// 错误的写法
if (v) {
  // ...
}
// ReferenceError: v is not defined

// 正确的写法
if (typeof v === "undefined") {
  // ...
}
```

对象返回`object`

```javascript
typeof window // "object"
typeof {} // "object"
typeof [] // "object"  数组本质上是一种特殊的对象
```

`instanceof`运算符可以区分数组和对象。

```javascript
var o = {};
var a = [];

o instanceof Array // false
a instanceof Array // true
```

`null`返回`object`。

```javascript
typeof null // "object"
```

`null`的类型是`object`，这是由于历史原因造成的。1995年的 JavaScript 语言第一版，只设计了五种数据类型（对象、整数、浮点数、字符串和布尔值），没考虑`null`，只把它当作`object`的一种特殊值。后来`null`独立出来，作为一种单独的数据类型，为了兼容以前的代码，`typeof null`返回`object`就没法改变了。
