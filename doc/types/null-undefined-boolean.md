# null， undefined 和布尔值

## null、undefined

### 概述

`null`与`undefined`都可以表示“没有”，含义非常相似。将一个变量赋值为`undefined`和`null`，语法效果几乎没区别

```javascript
var a = undefined;
// 或者
var a = null
```

写法效果几乎等价：在`if`语句中，都会自动转为`false`，`==`两者相等

```javascript
if (!undefined) {
  console.log('undefined is false');
}
// undefined is false

if (!null) {
  console.log('null is false');
}
// null is false

undefined == null
// true
```

困扰的原因：历史原因

最初设计的时候，像java一样，只设置了`null`表示“无”。根据 C 语言传统，`null`可以自动转为`0`

```javascript
Number(null) // 0 可以自动转为0
5 + null // 5
```

第一版的 JavaScript 里面，`null`就像在 Java 里一样，被当成一个对象，Brendan Eich 觉得表示“无”的值最好不是对象。其次，那时的 JavaScript 不包括错误处理机制，Brendan Eich 觉得，如果`null`自动转为0，很不容易发现错误。

因此，又设计了一个`undefined`。区别是这样的：`null`是一个表示“空”的对象。转为数值为`0`；`undefined`是一个表示“此处无定义的”原始值，转为数值时为`NaN`

```javascript
Number(undefined) // NaN
5 + undefined // NaN
```

### 用法和含义

`null`表示空值，即该处的值为空。调用函数时，某个参数未设置任何值，这时可以传入`null`，表示该参数为空。比如，某个函数接受引擎抛出的错误作为参数，如果运行过程中未出错，那么这个参数就会传入`null`，表示未发生错误。

`undefined`表示“未定义”，下面是返回`undefined`的典型场景。

```javascript
// 变量声明了，但没有赋值
var i;
i // undefined

// 调用函数时，应该提供的参数没有提供，该参数等于 undefined
function f(x) {
  return x;
}
f() // undefined

// 对象没有赋值的属性
var  o = new Object();
o.p // undefined

// 函数没有返回值时，默认返回 undefined
function f() {}
f() // undefined
```

## 布尔值

下列运算符会返回布尔值：

- 前置逻辑运算符： `!` (Not)
- 相等运算符：`===`，`!==`，`==`，`!=`
- 比较运算符：`>`，`>=`，`<`，`<=`


除了下面六个值被转为`false`，其他值都视为`true`。

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- `""`或`''`（空字符串）

应用：流程控制

```javascript
if ('') {
  console.log('true');
}
// 没有任何输出
```

注意，空数组（`[]`）和空对象（`{}`）对应的布尔值，都是`true`。

```javascript
if ([]) {
  console.log('true');
}
// true

if ({}) {
  console.log('true');
}
// true
```
