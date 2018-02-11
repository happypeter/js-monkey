---
title: Babel 到底是用来干啥的？
---


Babel 的官网在：http://babeljs.io/ 。官网上对它的描述是：

> 一个 Javascript 的编译器( compiler )

Babel 编译过程，输入格式 ES6 ，输出格式是 ES5 （ ES5 就是浏览器可以直接支持的 JS 版本)。

到 Babel 官网，点击 try it out ，可以进入 Babel 的在线试用环境，左侧如果我们输入 ES6 语句，例如

```
let i = 1;
```

那么右侧会自动输出 ES5 语法的编译结果。

```
var i = 1;
```
