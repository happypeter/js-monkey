---
title: 什么是字面值（ Literals ）？
---

字面值是由语法表达式定义的常量；或，通过由一定字辞组成的语词表达式定义的常量。

在JavaScript中，你可以使用各种字面值。这些字面值是脚本中按字面意思给出的固定的值，而不是变量。（译注：字面值是常量，其值是固定的，而且在程序脚本运行中不可更改，比如false，3.1415，thisIsStringOfHelloworld ，invokedFunction: myFunction("myArgument")。本节将介绍以下类型的字面值：

- 数组字面值(Array literals)
- 布尔字面值(Boolean literals)
- 浮点数字面值(Floating-point literals)
- 整数(Intergers)
- 对象字面值(Object literals)
- RegExp literals
- 字符串字面值(String literals)

### 数组字面值( Array literals )

数组字面值是一个封闭在方括号对([])中的包含有零个或多个表达式的列表，其中每个表达式代表数组的一个元素。当你使用数组字面值创建一个数组时，该数组将会以指定的值作为它的元素进行初始化，而其长度被设定为元素的个数。

下面的示例用3个元素生成数组coffees，它的长度是3。

```
var coffees = ["French Roast", "Colombian", "Kona"];
```

> 注意 这里的数组字面值也是一种对象初始化器

若在顶层（全局）脚本里用字面值创建数组，JavaScript语言会在每次对包含该数组字面值的表达式求值时解释该数组。另一方面，在函数中使用的数组，将在每次调用函数时被创建一次。

数组字面值同时也是数组对象。

##### 数组中额外的逗号

（译注：声明时）你不必列举数组字面值中的所有元素。若你在同一行中连写两个逗号（,），数组中就会产生一个没被指定的元素，其初始值是undefined。以下示例创建了一个名为fish的数组：

```
var fish = ["Lion", , "Angel"];
```

这个数组中，有两个已被赋值的元素，和一个空元素（fish[0]是"Lion"，fish[1]是undefined，而fish[2]是"Angel"；译注：此时数组的长度属性fish.length是3)。

如果在元素列表的结尾处包含一个尾随逗号，则忽略逗号。在下面的例子中，数组的长度是3。没有`mylist[3]`。列表中的所有其他逗号表示一个新的元素。

> 注意：尾部的逗号在早期版本的浏览器中会产生错误，因而编程时的最佳实践就是移除它们。

```
var myList = ['home', , 'school', ];
```

在下面的例子中，数组的长度是4，`myList[0]`和`myList[2]`缺失。

```
var myList = [ , 'home', , 'school'];
```

在下面的例子中，数组的长度是4，`myList[1]`和`myList[3]`被漏掉了，最后的逗号被忽略。

```
var myList = ['home', , 'school', , ];
```

理解多余的逗号（在脚本运行时会被如何处理）的含义，对于从语言层面理解JavaScript是十分重要的。但是，你自己写代码时：显式地将缺失的元素声明为undefined，将大大增加你的代码的清晰度和可维护性。

### 布尔字面值(Boolean literals)

（译注：即逻辑字面值）

布尔类型有两种字面值，`true` 和 `false` 。

不要混淆作为布尔对象的真和假与布尔类型的原始值true和false。布尔对象是原始布尔数据类型的一个包装器。

### 整数(Intergers)

整数可以表示为十进制（基数为10），十六进制（基数为16）、八进制（基数为8）和二进制（基数为2）。

- 十进制整数字组成的数字序列，不带前导0。
- 带前导0、0O、0o 的整数字面值表明它是八进制。八进制整数只能包括数字0-7。
- 前缀0x或0X表示十六进制。十六进制整数，可以包含数字（0-9）和字母a~f或A~F。
- 前导为`0B`或`0B`的表示二进制。二进制整数可以包括数字只有0和1。

下面是一些整数的例子：

```
0, 117 and -345 (十进制)
015, 0001 and -0o77 (八进制)
0x1123, 0x00111 and -0xF1A7 (十六进制)
0b11, 0b0011 and -0b11 (二进制)
```

### 浮点数字面值(Floating-point literals)

浮点数字面值可以有以下的组成部分：

- 一个十进制整数，它可以带符号（即前面的“+”或“ - ”号），
- 一个小数点（“.”），
- 一个小数部分（由一串十进制数表示），
- 一个指数部分。

指数部分是以“e”或“E”开头后面跟着一个整数，可以有正负号（即前面写“+”或“-”）。一个浮点数字面值必须至少有一位数字，后接小数点或者“e”（大写“E”也可）组成。

简言之，其语法是：

```
[(+|-)][digits][.digits][(E|e)[(+|-)]digits]
```

例如：

```
3.1415926
-.123456789 // -0.23456789
-3.1E+12 // -3.12*1012
.1e-23 // 0.1*10-23=10-24=1e-24
```

### 对象字面值(Object literals)

对象字面值是封闭在花括号对({})中的一个对象的零个或多个"属性名-值"对的（元素）列表。你不能在一条语句的开头就使用对象字面值，这将导致错误或非你所预想的行为，因为此时左花括号（{）会被认为是一个语句块的起始符号。

以下是一个对象字面值的例子。对象car的第一个元素（译注：即一个属性双值对）定义了属性myCar；第二个元素，属性getCar，引用了一个函数（即CarTypes("Honda")）；第三个元素，属性special，使用了一个已有的变量（即Sales）。

```
var sales = "Toyota";

function carTypes(name) {
  if (name === "Honda") {
    return name;
  } else {
    return "Sorry, we don't sell " + name + ".";
  }
}

var car = { myCar: "Saturn", getCar: carTypes("Honda"), special: sales };

console.log(car.myCar);   // Saturn
console.log(car.getCar);  // Honda
console.log(car.special); // Toyota
```

 更进一步的，你可以使用数字或字符串字面值作为属性的名字，或者在另一个字面值内嵌套上一个字面值。如下的示例中使用了这些可选项。

```
var car = { manyCars: {a: "Saab", "b": "Jeep"}, 7: "Mazda" };

console.log(car.manyCars.b); // Jeep
console.log(car[7]); // Mazda
```

对象属性名字可以是任意字符串，包括空串。如果对象属性名字不是合法的javascript标识符，它必须用""包裹。属性的名字不合法，那么便不能用“.”访问属性值，而是通过类数组标记("[]")访问和赋值。

```
var unusualPropertyNames = {
  "": "An empty string",
  "!": "Bang!"
}
console.log(unusualPropertyNames."");   // SyntaxError: Unexpected string
console.log(unusualPropertyNames[""]);  // An empty string
console.log(unusualPropertyNames.!);    // SyntaxError: Unexpected token !
console.log(unusualPropertyNames["!"]); // Bang!
```

在 ES2015 中，对象文本扩展到支持在原型设置建造，简写为`foo: foo`分配，定义方法，回调，计算属性名和表达式。另外，这些也使对象和类声明更紧密的结合在一起，让基于对象的设计得益于一些同样的便利。

```
var obj = {
    // __proto__
    __proto__: theProtoObj,
    // Shorthand for ‘handler: handler’
    handler,
    // Methods
    toString() {
     // Super calls
     return "d " + super.toString();
    },
    // Computed (dynamic) property names
    [ 'prop_' + (() => 42)() ]: 42
};
```

请注意：

```
var foo = {a: "alpha", 2: "two"};
console.log(foo.a);    // alpha
console.log(foo[2]);   // two
//console.log(foo.2);  // Error: missing ) after argument list
//console.log(foo[a]); // Error: a is not defined
console.log(foo["a"]); // alpha
console.log(foo["2"]); // two
```

### 正则表达式（RegExp literals）

一个正则表达式是字符被斜线围成的表达式。下面是一个正则表达式文字的一个例子。

```
var re = /ab+c/;
```

### 字符串字面值(String literals)

字符串字面值可以包含有零个或多个字符，由双引号（"）对或单引号（‘）对包围。字符串被限定在同种引号之间；也即，必须是成对单引号或成对双引号。下面的例子都是字符串字面值：

```
"foo"
'bar'
"1234"
"one line \n another line"
"John's cat"
```

你可以在字符串字面值上使用字符串对象的所有方法——JavaScript会自动将字符串字面值转换为一个临时字符串对象，调用该方法，然后废弃掉那个临时的字符串变量。你也能用对字符串字面值使用类似String.length的属性：

```
console.log("John's cat".length)
// 将打印字符串的长度，包括空格
// 输出结果为10.
```

在 ES2015 中，模板文字也可以使用。模板字符串为构造字符串提供语法糖。这是类似于在`Perl`和`Python`等其他语言的字符串插值功能。可选的，在字符串内容中可以添加一个标记，以允许字符串结构来进行定制，避免注入攻击或构造更高级别的数据结构。

```
// Basic literal string creation
`In JavaScript '\n' is a line-feed.`

// Multiline strings
`In JavaScript this is
 not legal.`

// String interpolation
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`

// Construct an HTTP request prefix is used to interpret the replacements and construction
POST`http://foo.org/bar?a=${a}&b=${b}
     Content-Type: application/json
     X-Credentials: ${credentials}
     { "foo": ${foo},
       "bar": ${bar}}`(myOnReadyStateChangeHandler);
```

##### 在字符串中使用特殊字符

作为一般字符的扩展，你可以在字符串中使用特殊字符，如下例所示。

```
"one line \n another line"
```

下表列出了您可以使用JavaScript字符串中的特殊字符。

| 转义字符      | 含义
| ------------- |:-------------:
| \0      | Null 字符
| \b      | 退格符      
| \f | 换页符
| \n | 换行符
| \r | 回车符
| \t | 水平制表符
| \v | 垂直制表符
| \' | 撇号或单引号
| \" | 双引号
| \\ | 反斜线
| \XXX | 通过最多三个八进制位数×377。例如在0和指定的Latin-1编码的字符，\251是版权符号八进制序列。
| \xXX | 由00和FF之间的两个十六进制数字XX指定的Latin-1编码的字符。例如，版权所有\ xA9为版权符号十六进制序列。
| \uXXXX | 由四个十六进制数字XXXX规定的Unicode字符。例如，\ u00A9为版权符号的Unicode序列。见Unicode转义序列。
| \u{XXXXX} | Unicode code point escapes. For example, \u{2F804} is the same as the simple Unicode escapes \uD87E\uDC04.

##### 转义字符

对于那些未出现在表中的字符，其所带的前导反斜线'\'将被忽略。但是，这一用法已被废弃，应当避免使用。

通过在引号前加上反斜线'\'，可以在字符串中插入引号，这就是`引号转义`。例如:

```
var quote = "He read \"The Cremation of Sam McGee\" by R.W. Service.";
console.log(quote);
```

上边代码输出的结果是：

```
He read "The Cremation of Sam McGee" by R.W. Service.
```

要在字符串中插入'\'字面值，必须转义反斜线。例如，要把文件路径` c:\temp` 赋值给一个字符串，可以采用如下方式:

```
var home = "c:\\temp";
```

也可以在换行之前加上反斜线以转义换行（译注：实际上就是一条语句拆成多行书写），这样反斜线和换行都不会出现在字符串的值中。

```
var str = "this string \
is broken \
across multiple\
lines."
console.log(str);   // this string is broken across multiplelines.
```

尽管 JavaScript 没有“`heredoc`”的语法，但可以用行末的换行符转义和转义的换行来近似实现

```
var poem =
"Roses are red,\n\
Violets are blue.\n\
I'm schizophrenic,\n\
And so am I."
```

### 参考文档

- [MDN Javascript Guide#Grammar and types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types) 本文内容是这里内容的中文版，略有删改。
- 上面的译文大量参考了 [MDN 上的中文翻译](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types)
