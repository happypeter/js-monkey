看看 JavaScript 中可用的循环结构。

## 基本形式

一段循环通常需要一个或多个条件：

* 一个计数变量（ counter ），它被初始化为一个特定的值
* 一个结束条件（ exit condition ），这是循环停止的标准
* 一个迭代器（ iterator ），迭代器会在每次循环中修改计数变量的值，直到达到退出条件。

代码如下

```js
for (var i = 0; i < 100; i++) {
  doSth()
}
```

i 就是计数变量。`i < 100` 是结束条件，`i++` 就是迭代器。

## 使用 break 退出循环

如果要在所有迭代完成之前退出循环，可以使用 break 语句。

## 使用 continue 跳过迭代

continue 跟 break 有点类似，但不是完全跳出循环，而是跳过一次迭代。

## while 语句和 do ... while 语句

for 不是 js 中唯一的循环类型，其他的还有很多。while 是常见的一个。

伪代码

```
initializer
while (exit-condition) {
  // code to run

  final-expression
}
```

一个实际例子

```
var i = 0;

while (i < cats.length) {
  if (i === cats.length - 1) {
    info += 'and ' + cats[i] + '.';
  } else {
    info += cats[i] + ', ';
  }

  i++;
}
```

do...while 用法非常类型，伪代码

```
initializer
do {
  // code to run

  final-expression
} while (exit-condition)
```

跟 while 的主要区别就是 do 后面的代码块至少会执行一次，因为检查退出条件是在后面，而 for 和普通 while 的循环可能一次都执行不到，因为是先检查条件后循环。

## 参考

* https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Looping_code
