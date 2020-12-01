# 对象

## 属性的操作

### 属性的读取

读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。

```javascript
var obj = {
  p: 'Hello World'
};

obj.p // "Hello World"
obj['p'] // "Hello World"
```

### 属性的赋值

点运算符和方括号运算符，不仅可以用来读取值，还可以用来赋值。

```javascript
var obj = {};

obj.foo = 'Hello';
obj['bar'] = 'World';
```

### 属性的查看

查看一个对象本身的所有属性，可以使用`Object.keys`方法。

```javascript
var obj = {
  key1: 1,
  key2: 2
};

Object.keys(obj);
// ['key1', 'key2']
```

### 属性的删除：delete 命令

`delete`命令用于删除对象的属性，删除成功后返回`true`。不存在的属性，返回`true` 不可删除的属性，返回false

```javascript
var obj = { p: 1 };
Object.keys(obj) // ["p"]

delete obj.p // true
obj.p // undefined
Object.keys(obj) // []
```

注意，删除一个不存在的属性，`delete`不报错，而且返回`true`。

```javascript
var obj = {};
delete obj.p // true
```

`delete`命令会返回`false`，那就是该属性存在，且不得删除。

```javascript
var obj = Object.defineProperty({}, 'p', {
  value: 123,
  configurable: false
});

obj.p // 123
delete obj.p // false
```

`delete`命令只能删除对象本身的属性，无法删除继承的属性

```javascript
var obj = {};
delete obj.toString // true
obj.toString // function toString() { [native code] }
```

### 属性是否存在：in 运算符

`in`运算符用于检查对象是否包含某个属性（注意，检查的是键名，不是键值），如果包含就返回`true`，否则返回`false`。

```javascript
var obj = { p: 1 };
'p' in obj // true
'toString' in obj // true
```

`in`运算符的一个问题是，它不能识别哪些属性是对象自身的，哪些属性是继承的。就像上面代码中，对象`obj`本身并没有`toString`属性，但是`in`运算符会返回`true`，因为这个属性是继承的。

这时，可以使用对象的`hasOwnProperty`方法判断一下，是否为对象自身的属性。

```javascript
var obj = {};
if ('toString' in obj) {
  console.log(obj.hasOwnProperty('toString')) // false
}
```

### 属性的遍历：for...in 循环

`for...in`循环用来遍历一个对象的全部属性。

```javascript
var obj = {a: 1, b: 2, c: 3};

for (var i in obj) {
  console.log('键名：', i);
  console.log('键值：', obj[i]);
}
// 键名： a
// 键值： 1
// 键名： b
// 键值： 2
// 键名： c
// 键值： 3
```

`for...in`循环有两个使用注意点。

- 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
- 它不仅遍历对象自身的属性，还遍历继承的属性。

举例来说，对象都继承了`toString`属性，但是`for...in`循环不会遍历到这个属性。

```javascript
var obj = {};

// toString 属性是存在的
obj.toString // toString() { [native code] }

for (var p in obj) {
  console.log(p);
} // 没有任何输出
```

上面代码中，对象`obj`继承了`toString`属性，该属性不会被`for...in`循环遍历到，因为它默认是“不可遍历”的。关于对象属性的可遍历性，参见《标准库》章节中 Object 一章的介绍。

如果继承的属性是可遍历的，那么就会被`for...in`循环遍历到。但是，一般情况下，都是只想遍历对象自身的属性，所以使用`for...in`的时候，应该结合使用`hasOwnProperty`方法，在循环内部判断一下，某个属性是否为对象自身的属性。

```javascript
var person = { name: '老张' };

for (var key in person) {
  if (person.hasOwnProperty(key)) {
    console.log(key);
  }
}
// name
```