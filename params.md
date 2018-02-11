---
title: 拓展参数
---


拓展参数的案例

```js
var people=['zf','John','Sherlock'];

function sayHello(people1,people2,people3){
    console.log(`Hello ${people1},${people2},${people3}`);
}
//但是我们将一个数组以拓展参数的形式传递，它能很好地映射到每个单独的参数
sayHello(...people);//输出：Hello zf,John,Sherlock

//而在以前，如果需要传递数组当参数，我们需要使用函数的apply方法
// sayHello.apply(null,people);//输出：Hello zf,John,Sherlock
```
