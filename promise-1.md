---
title: 什么是 Promise ?
---


注：有视频，在 <http://haoduoshipin.com/v/205.html> 。

Promise 咱们分两期介绍，本期介绍基本使用，下期介绍底层原理。

### 什么是 Promise ?

Promises 是一种规范，目的是为异步编程提供统一接口。Promise 在 ES5 的时代没有语言层面的原生支持，但是有很多第三方的库可以用。ES6 中 Promise 被固化到了语言中。

简单说，它的思想是，每一个异步任务返回一个 Promise 对象，该对象有一个 then 方法，允许指定回调函数。比如，f1 的回调函数 f2,可以写成：

```
f1().then(f2);
```

要理解 Promise 首先要理解什么是**异步**。

### 异步执行

通常程序执行都是第一句先执行，执行完毕之后，再执行第二句，如果第二句没有执行完毕，例如返回值还没有得到，就不会
执行第三条语句。这样的执行方式叫“同步执行”。但是我们今天要聊的**异步执行**，就完全不同。


来看下面的例子，可以到 http://jsbin.com 执行一下：


html 如下：

```
  <button>click</button>
```

js 如下：


```
var button = document.querySelector('button');


console.log('Before');

button.onclick = function(){
  console.log('button clicked!');
};

console.log('After');
```


我们主要看 button.onclick 的这个 function ，代码执行到这一行的时候，这个函数并不会马上执行，
而是先执行下面的 `log('After')` 语句。而只有当某种条件下（我们这里的情况是，点击按钮的时候），`button clicked!` 那
一行语句才能被执行到。这就是异步执行的一个例子。


### 异步代码通常用于耗时比较长的操作


比如我们写 NodeJS 的时候，遇到[文件系统的读文件操作](https://nodejs.org/api/fs.html#fs_fs_read_fd_buffer_offset_length_position_callback)

```
fs.read(filepath, function(){
   console.log('读到数据');  
});

console.log('After');
```

来看看上面的代码。由于读取硬盘上的文件是个比较耗费时间的操作，所以 Nodejs 的设计者就把 `fs.read` 设计成
一个**异步函数**，也就是当代码执行到 `fs.read` 这一行的时候，并不会在这里停留，而是会先执行后面的打印 `After` 语句。
而只有当数据读取完毕了，才执行 `console.log('读到数据')` 这一行所在的回调函数。


### 异步操作有不同的执行方式

使用回调函数（ callback ）是非常常见的一种实现异步执行的方式，但是[执行异步操作的方式并不唯一](http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html) 。回调函数如果嵌套层级多了，就会引发 callback hell 回调地狱，让代码写得非常难看。

使用 Promise 就可以避免这个问题。Promise 的作用就跟它的名字一样，就是一个“承诺”。Promise 就是个盒子，盒子里面装着一个
还没有被执行到的操作。那”承诺”什么呢？就是承诺这个操作未来一定会被执行。

Promise 其实用的范围听广的，例如我们用 axios/fetch 做 http 请求的时候，总会看到 `.then()` 函数，这个就已经用到了 Promise 了。
不一定非要

```
new Promise
```

才能用 Promise 。


### Axios 为例

Axios 的 github [页面上](https://github.com/mzabriskie/axios) 可以看到 `Promise based HTTP client` 的字样，说它是一个

> 基于 Promise 的 HTTP 客户端


所以如果有这样的代码


```
var promise = axios.get('/path/to/server/api');

promise.then(function(data){

});
promise.catch(function(err){

});
```

此时 axios 的返回值就是一个 promise 。可以用 .then 来获取返回的数据，如果有错误发生，可以用 .catch 来拿到错误信息。
注意，当我们拿到 promise 对象的时候，也就是上面代码执行完了第一行的时候，promise 这个盒子里面装的这个请求 API 的操作，并没有
被执行完毕。但是程序“承诺”这个操作一定会执行的。执行完毕之后，才会自动执行 .then 和 .catch 。

另外

```
promise.then(function(data){

});
promise.catch(function(err){

});
```

有两种等价形式，第一种是**链式函数**，如下

```
promise.then(function(data){

}).catch(function(err){

});
```

另外一种形式是，直接把 catch 中的回调函数作为 .then 的第二个参数，如下

```
promise.then(function(data){

}, function(err){

});
```

所以，上面 .then 中的两个参数函数，第一个是 on success 时候的处理函数，第二个是 on error 的处理函数。

我们其实用 Promise 做异步操作，就是在模拟多线程语言的行为，通常都是来处理**并发任务** 。


### Promise 底层原理

这个下一期介绍。

### 参考资料

- http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html
- https://laracasts.com/series/es6-cliffsnotes/episodes/13
