---
title: ES6 的 let 和 ES5 的 var 有啥区别？
---

ES6新增了 let 命令，用来声明变量。它的用法类似于 var ，但是所声明的变量，只在 let 命令所在的代码块内有效。

```
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

上面代码在代码块之中，分别用 let 和 var 声明了两个变量。然后在代码块之外调用这两个变量，结果 let 声明的变量报错，var 声明的变量返回了正确的值。这表明，let 声明的变量只在它所在的代码块有效。ReferenceError: a is not defined. 的中文意思是：引用错误：a 没有定义。

总之，使用 let 更加安全，直观，而如果使用 var 就需要提防“变量提升”等各种恶心问题。所以最后的建议是，只要有 ES6 环境，尽量使用 let 。

更多细节请参考：http://es6.ruanyifeng.com/#docs/let
