在任何的编程语言中，代码需要依靠不同的输入作出决定并且采取行动。例如，在游戏中，如果玩家的生命值变成了 0，那么游戏就结束了。在天气应用中，如果在早晨运行，就显示一张日出的图片；如果在晚上，就显示星星和月亮的图片。在这篇文章中，我们将探索在 JavaScript 中所谓的条件语句是怎样工作的。

## if ... else 语句

伪代码如下

```
if (condition) {
  code to run if condition is true
} else {
  run some other code instead
}
```

一个真实的例子

```js
var shoppingDone = false

if (shoppingDone === true) {
  var childsAllowance = 10
} else {
  var childsAllowance = 5
}
```

## 逻辑运算符：AND，OR 和 NOT

如果要测试多个条件，而不需要编写嵌套 if ... else 语句，逻辑运算符可以帮助您。当在条件下使用时，前两个执行以下操作：

* && — 逻辑与; 使得并列两个或者更多的表达式成为可能，只有当这些表达式每一个都返回 true 时，整个表达式才会返回 true.
* || — 逻辑或; 当两个或者更多表达式当中的任何一个返回 true 则整个表达式将会返回 true.

## switch

区别于 if ，如果判断条件简单，但是种类众多的时候，就比较适合用 switch 语句，伪代码如下

```
switch (expression) {
  case choice1:
    run this code
    break;

  case choice2:
    run this code instead
    break;

  // include as many cases as you like

  default:
    actually, just run this code
}
```

## 三目运算符

伪代码

```
( condition ) ? run this code : run this code instead
```

实例

```js
var greeting = isBirthday
  ? 'Happy birthday Mrs. Smith — we hope you have a great day!'
  : 'Good morning Mrs. Smith.'
```

如果 isBirthday 为 true 那变量 greeting 的值就是 `Happy birthday...` ，否则就是 `Good morning...` 。

## 参考

* https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/conditionals
