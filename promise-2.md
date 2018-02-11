---
title: Promise 的底层机制 ?
---

接前面一期，这一集来介绍 Promise 的底层机制。

### 构造函数

基本用法如下：

```
var thing = new Promise(function(){
  alert('hello');
});
```

上面的这个 function() 是会立刻被执行的。如果你理解面向对象编程的话，可以认为这个函数就类似于一个 constructor 构造函数。
所以上面代码执行，我们可以立即看到 alert 的对话框。

### resolve 和 reject

上面的函数中，可以接受两个参数，一个是 resolve 一个是 reject ，如下

```
var thing = new Promise(function(resolve, reject){
  resolve();// 当操作成功之后，我们会呼叫这个函数，这样 thing.then() 就会被执行
  reject();// 如果操作失败，我们呼叫这个函数，来触发 thing.catch()
});
```

### 动手实验一下

试着在 jsbin 中运行下面代码

```
var thing = new Promise(function(resolve, reject){
  console.log('Run!');
  setTimeout(function(){
    resolve()
  }, 3000);
});
thing.then(function(){
  console.log('thing.then()...');
});
thing.catch(function(){
  console.log('thing.catch()...');  
});
```

执行上面代码，可以看到，chrome 终端中会先打印出 Run! ，然后三秒后会打印出 thing.then ... 。如果把上面的 `resolve()` 改成 `reject()` ，
那么得到执行的就是 `thing.catch()` 了。


### 总结

前面205期和本期，我试图用最直观的方式展示一下 Promise 的基本原理，我想分享的内容暂时就是这些，但是 Promise 还有很多知识点没有介绍到，大家可以翻阅下面的参考内容。

### 参考

- https://laracasts.com/series/es6-cliffsnotes/episodes/13
- http://es6.ruanyifeng.com/#docs/promise
