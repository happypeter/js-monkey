在 JavaScript 中另一个基本概念是函数, 它允许你在一个代码块中存储一段用于处理一个任务的代码，然后在任何你需要的时候用一个简短的命令来调用，而不是把相同的代码写很多次。在本文中，我们将探索函数的基本概念，如基本语法、如何定义和调用、作用域以及参数。

## 浏览器内置函数

当我们操作一个字符串的时候，就会用到很多浏览器内置函数

```js
var myText = 'I am a string'
var newString = myText.replace('string', 'sausage')
console.log(newString)
```

JavaScript 有许多内置的函数，可以做很多有用的事情，而无需自己编写所有的代码。事实上, 许多浏览器内置函数并不是用 JavaScript 来编写——大多数是使用像 C++ 这样更低级的系统语言编写的，而不是像 JavaScript 这样的 web 编程语言。

请记住，这些内置浏览器函数不是 JavaScript 语言的一部分——而是浏览器 API 的一部分。

## 函数与方法

英文：function 和 method 。

需要澄清一件事——严格说来，浏览器函数并不是函数——它们是方法。函数和方法，其实  很多场合都是可以互换的概念。

区别是方法是定义在对象内部的函数。浏览器内置的函数（也就是方法）和变量（也就是属性）都是存放在对象（object）中的。

## 自定义函数

自定义函数就是代码中自己定义的函数，而不是那些浏览器自带的。一个自定义的名字后面如果紧跟一个括号，那这就是一个自定义函数。例如

```js
function draw() {
  ctx.clearRect(0, 0, WIDTH, HEIGHT)
  for (var i = 0; i < 100; i++) {
    ctx.beginPath()
    ctx.fillStyle = 'rgba(255,0,0,0.5)'
    ctx.arc(random(WIDTH), random(HEIGHT), random(50), 0, 2 * Math.PI)
    ctx.fill()
  }
}
```

执行这个函数就用

```js
draw()
```

## 无名函数

您也可以创建一个没有名称的函数：

```js
function() {
  alert('hello');
}
```

这个函数就叫做无名函数，因为它没有函数名。可以用这样的形式来使用

```js
var myButton = document.querySelector('button')

myButton.onclick = function() {
  alert('hello')
}
```

也可以把无名函数赋值给一个变量

```js
var myGreeting = function() {
  alert('hello')
}
```

这样就可以这样来执行它了

```js
myGreeting()
```

## 函数的参数

英文：Function parameters 。

有些函数在执行的时候需要传入参数。参数就是包裹在函数括号中的一些值。

> 参数（Parameters）有时候也被叫做 arguments （中文翻译也是：参数） 或者 properties （属性）。

来看看例子。浏览器自带的 Math.random 函数不需要任何参数。

```js
var myNumber = Math.random()
```

而浏览器自带的 replace 函数需要两个参数。

```js
var myText = 'I am a string'
var newString = myText.replace('string', 'sausage')
```

> 多个参数用逗号隔开

也有些函数的参数是可选项--意思是可以有也可以没有。不给参数的情况下，这些函数都会有一些默认行为。例如 join 函数

```js
var myArray = ['I', 'love', 'chocolate', 'frogs']
var madeAString = myArray.join(' ')
// returns 'I love chocolate frogs'
var madeAString = myArray.join()
// returns 'I,love,chocolate,frogs'
```

没有给 join 传任何参数，那 join 就会默认使用逗号。

## 函数作用域

来聊一下作用域，一个处理函数的时候非常重要的概念。

当一个函数创建好之后，里面的变量和其他东西都处于它自己的作用域范围内，意味着外部世界是访问不到它们的。那这些变量就有着**局部作用域** 。

所有函数之外的顶级区域叫做**全局作用域**（ global scope ）。定义在这个作用域的值可以在代码的任意位置访问到。

## 函数内的函数

可以从任何地方调用函数，甚至可以在另一个函数中调用函数。如果您有一个复杂的函数，如果将其分解成几个子函数，会更容易理解：

```js
function myBigFunction() {
  var myValue

  subFunction1()
  subFunction2()
  subFunction3()
}

function subFunction1() {
  console.log(myValue)
}

function subFunction2() {
  console.log(myValue)
}

function subFunction3() {
  console.log(myValue)
}
```

上面的例子会抛出一个错误`ReferenceError：MyValue 没有被定义`。解决方法就是必须将值作为参数传递给函数，如下所示：

```js
function myBigFunction() {
  var myValue = 1

  subFunction1(myValue)
  subFunction2(myValue)
  subFunction3(myValue)
}

function subFunction1(value) {
  console.log(value)
}

function subFunction2(value) {
  console.log(value)
}

function subFunction3(value) {
  console.log(value)
}
```

## 什么是返回值?

有些函数执行完毕后不会有返回值，但是有些会。返回值就是函数执行后返回的值。

例如：

```js
var myText = 'I am a string'
var newString = myText.replace('string', 'sausage')
console.log(newString)
```

上面，当 replace 函数执行完毕之后，就返回一个值，然后我们把这个值赋值给了变量 newString 。

## 在自己的函数中使用返回值

关键就是学会使用 `return` 关键字。

```js
function random(number) {
  return Math.floor(Math.random() * number)
}
```

上面的形式也等价于

```js
function random(number) {
  var result = Math.floor(Math.random() * number)
  return result
}
```

## 参考

* https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions
