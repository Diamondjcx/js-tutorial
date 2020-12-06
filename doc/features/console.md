# console 对象与控制台

### console.count()

`count`方法用于计数，输出它被调用了多少次。

```javascript
function greet(user) {
  console.count();
  return 'hi ' + user;
}

greet('bob')
//  : 1
// "hi bob"

greet('alice')
//  : 2
// "hi alice"

greet('bob')
//  : 3
// "hi bob"
```

上面代码每次调用`greet`函数，内部的`console.count`方法就输出执行次数。

该方法可以接受一个字符串作为参数，作为标签，对执行次数进行分类。

```javascript
function greet(user) {
  console.count(user);
  return "hi " + user;
}

greet('bob')
// bob: 1
// "hi bob"

greet('alice')
// alice: 1
// "hi alice"

greet('bob')
// bob: 2
// "hi bob"
```

上面代码根据参数的不同，显示`bob`执行了两次，`alice`执行了一次。

### console.time()，console.timeEnd()

这两个方法用于计时，可以算出一个操作所花费的准确时间。

```javascript
console.time('Array initialize');

var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};

console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```

`time`方法表示计时开始，`timeEnd`方法表示计时结束。它们的参数是计时器的名称。调用`timeEnd`方法之后，控制台会显示“计时器名称: 所耗费的时间”。