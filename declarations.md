---
title: JS 中怎么声明变量？
---

在 JavaScript 中有三种声明方式。

`var` 声明一个变量，可以初始化它的值。

`let` 声明一个块级作用域的局部变量，可以初始化它的值。

`const` 声明一个只读常量。

### 变量

在应用程序中，你可以使用变量给一个值起一个好记的名字。变量名，也称为标识符，的使用要遵循一定的规则。

一个 JavaScript 变量名必须以字母，下划线（_），或一个美元符号（$）开始，随后的字符可以是数字（0-9）。因为 JavaScript 是区分大小写的，字母包括字符“A”到“Z”（大写）和字符“a”到“z”（小写）。

一些合法的变量名如：Number_hits、temp99、 _name。

### 声明变量

你可以通过三种方式声明一个变量：

* 通过关键字 `var` 。比如 `var x = 42` 。这种语法可用于声明局部和全局变量。
* 通过直接赋值。比如 `x = 42` 。这样会声明一个全局变量，不推荐这种形式，会产生警告信息。
* 使用关键字 `let` 。比如 `let y = 13`。这个语法可以用来声明一个块级作用域的局部变量。

### 变量求值

通过 `var` 或 `let` 声明的变量如果没有赋值，那么它们的值就是未定义（`undefined`）

访问一个未定义的变量会导致抛出 `ReferenceError` 的错误。

```
var a;
console.log("The value of a is " + a); // log 中会打印出 "The value of a is undefined"
console.log("The value of b is " + b); // 抛出 ReferenceError 异常
```

您可以使用 `undefined` 来确定一个变量是否已经被赋值。在下面的代码中，没有为变量赋值，`if` 语句判断为真。

```
var input;
if(input === undefined){
  doThis();
} else {
  doThat();
}
```

如果被用在布尔条件下，那么 `undefined` 等同于 `false` 。例如，下面的代码将执行函数 MyFunction 因为指定的那个 MyArray 元素是未定义的：

```
var myArray = [];
if (!myArray[0]) myFunction();
```

在数字条件中使用时，`undefined` 的值转换为 `NaN`。

```
var a;
a + 2;  // 求值结果为 NaN
```

当你对一个空变量 `null` 求值时，在数字环境中它的值为0，在布尔环境中是 `false` 。例如：

```
var n = null;
console.log(n * 32); // 终端 log 中会打印 0
```

### 变量作用域

当你在函数外部声明一个变量时，它被称为一个全局变量，因为它可以在当前文档中的任何其他代码中使用。当你在一个函数中声明一个变量时，它被称为局部变量，因为它只能在该函数中使用。

JavaScript 在 ECMAScript 6 之前没有的块级作用域的概念；一个在块内声明的变量的作用域是它所在的函数（或者是全局）。例如下面的代码将输出5，因为在变量 `x`声明在 `if` 语句块中，是一个全局变量。

```
if (true) {
  var x = 5;
}
console.log(x);  // 5
```

ECMAScript6 引入了 `let` ，用它声明变量时，行为就不同了。

```
if (true) {
  let y = 5;
}
console.log(y);  // ReferenceError: y 没有被定义
```

### 变量提前

在 JavaScript 中，另一个关于变量的怪异的事是你可以使用一个在当前位置之后声明的变量，而且不会导致异常，这个被称为声明提前。JavaScript 中的变量在某种意义上是被提升或提前到函数或语句的顶部。然而，被提前的变量的值是 `undefined`，因此，即使在使用或引用该变量之后对它进行声明和初始化，它仍将返回 `undefined` 。

```
/**
 * Example 1
 */
console.log(x === undefined); // 打印 "true"
var x = 3;

/**
 * Example 2
 */
// 返回 undefined
var myvar = "my value";

(function() {
  console.log(myvar); // undefined
  var myvar = "local value";
})();
```

上面的例子等同：

```
/**
 * Example 1
 */
var x;
console.log(x === undefined); // 打印 "true"
x = 3;

/**
 * Example 2
 */
var myvar = "my value";

(function() {
  var myvar;
  console.log(myvar); // undefined
  myvar = "local value";
})();
```

由于声明提前，在函数中所有 `var` 声明应该尽可能的放在函数体的顶部，这种最佳实践提高了代码的清晰度。

在 ECMAScript2015 中，`let` （ `const` ）将会把变量提升到块的顶部。然而，在声明变量之前引用变量将会导致 `ReferenceError` 。从作用域开始直到声明位置，变量处于一个“暂时的死亡区域”。

```
function do_something() {
  console.log(foo); // ReferenceError
  let foo = 2;
}
```

### 全局变量

全局变量实际上是全局对象的属性。Web 页面中的全局对象是窗口（ window ），所以你可以通过使用 window.variable 语法来设置和调用全局变量。

因此，你可以通过指定 window 或 frame 名称，来从另一个 window 或 frame 中访问一个 window 或 frame 中声明的全局变量。例如，如果文件中声明了一个 `phoneNumber` 的变量，你可以从一个 iframe 中用 `parent.phonenumber` 引用这个变量。

### 定义常量

你可以使用 `const` 关键字来创建一个只读的，带有名字的常量。一个常量标识符语法和一个变量标识符相同的：它必须以字母、下划线或美元符号开始，可以包含字母、数字或下划线。

```
const prefix = '212';
```

当脚本正在运行时，一个常量不能通过赋值或被重新声明来改变它的值。它必须被初始化为一个值。

常量的作用域的规则和 `let` 变量块级作用域变量是相同的。如果 `const` 关键字被省略，标识符会被默认为代表一个变量。

在同一作用域范围内，你不能声明与函数或变量同名的常量。例如：

```
// 这样会导致 ERROR
function f() {};
const f = 5;

// 也是 ERROR
function f() {
  const g = 5;
  var g;

  //更多语句
}
```

然而，对象的属性没有被保护，所以下面的语句是没有问题的：

```
const MY_OBJECT = {"key": "value"};
MY_OBJECT.key = "otherValue";
```
