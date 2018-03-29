事件（ Events ）是程序运行环境中发生的一些动作或者状况。环境通过事件通知我们，一般我们采取相应的处理策略。举个例子，如果用户点一个按钮，我们可能就会相应的展示一个对话框给用户。

## 事件举例

Web 开发中，事件就是浏览器发出的。并且事件一般都绑定在一个特定的东西上，例如一个元素，多个元素，整个 html 文档，或者整个浏览器窗口。事件可能有很多种类

* 用户点击一个元素，或者鼠标滑过一个元素
* 用户按下键盘上的一个键
* 用户调整了浏览器窗口的大小
* 网页加载完毕
* 出现错误

[这里](https://developer.mozilla.org/en-US/docs/Web/Events) 有完整的事件列表。

每个事件都会有一个事件处理器（event handler)，通常都是一个用户定义的函数。当事件发生时，这个函数就会执行。

## 使用网页事件的方式

可以使用下面的事件处理器属性（ event handler properties ），例如下面的 onClick 来添加事件处理代码。

```js
var btn = document.querySelector('button')

btn.onclick = function() {
  var rndCol =
    'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')'
  document.body.style.backgroundColor = rndCol
}
```

`onClick` 跟 btn.style 和 btn.textContent 一样，都是按钮属性。但是它是一个比较特殊的，当你让它等于某些代码的时候，这些代码就会在事件被触发后被执行。

也不一定非要用无名函数，下面的形式也是可以的

```js
var btn = document.querySelector('button')

function bgChange() {
  var rndCol =
    'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')'
  document.body.style.backgroundColor = rndCol
}

btn.onclick = bgChange
```

其他的事件处理器属性还有很多，例如 btn.onfocus ，window.onkeydown ，btn.onmouseover 等等。

## addEventListener() and removeEventListener()

浏览器还有另外一个函数叫 addEventListener ，这个函数跟事件处理器属性的功能类似，但是语法显然不一样。

```js
var btn = document.querySelector('button')

function bgChange() {
  var rndCol =
    'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')'
  document.body.style.backgroundColor = rndCol
}

btn.addEventListener('click', bgChange)
```

addEventListener 有两个参数，一个是我们要注册的事件处理器的名字，另一个是响应这个事件处理器的处理器函数。当然，采用无名函数的形式把处理器函数代码直接传进来也是完全可以的。

```js
btn.addEventListener('click', function() {
  var rndCol =
    'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')'
  document.body.style.backgroundColor = rndCol
})
```

addEventListener 这种方式有不少优点。

第一，它有一个对应函数叫 removeEventListener ，可以用来删除之前添加的监听器（ listener ）。使用方式如下

```js
btn.removeEventListener('click', bgChange)
```

对于小程序这个就无所谓了，但是对于大型程序清除事件处理器还是非常能提高代码执行效率的。再有，这样也可以让我们的按钮在不同条件下执行不同的处理代码，我们只需要在适当的时候添加和删除事件处理器即可。

第二，现在我们可以向相同的监听器（listener）传递多个处理器（handler)了。

比如如果这样写

```js
myElement.onclick = functionA
myElement.onclick = functionB
```

那么第二行代码就会覆盖第一行，而下面的写法就可以达到目的

```js
myElement.addEventListener('click', functionA)
myElement.addEventListener('click', functionB)
```

元素被点击时，两个函数都会被执行。

第三，addEventListener 还可以实现其他一些功能，具体可以参考它的官方文档。

## 老方式-内联处理器

就是类似这种

```js
<button onclick="alert('Hello, this is my old-fashioned event handler!');">
  Press me
</button>
```

现在已经不推荐使用了。

## 到底该采用哪种机制呢？

除了内联方式，其他两种方式都可以用：

* 事件处理器属性，虽然不是那么灵活，但是浏览器支持好，甚至 IE8 都可以，所以开始学习的时候使用这种方式是非常棒的
* addEventListener ，更强，但是也更复杂，浏览器支持到 IE9 。

## 事件对象

有时候事件处理函数中会有 event，evt 或者 e 这样的参数，这个就是事件对象（ event object ）。它是被自动传递给处理函数的，用来提供丰富的信息。

```js
function bgChange(e) {
  var rndCol =
    'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')'
  e.target.style.backgroundColor = rndCol
  console.log(e)
}

btn.addEventListener('click', bgChange)
```

这样就能打印出事件对象中包含的信息了。

当我们要对很多个元素执行相同的操作时，`e.target` 就显得非常有用了。 比如下面的代码

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Useful event target example</title>
    <style>
      div {
        background-color: red;
        height: 100px;
        width: 25%;
        float: left;
      }
    </style>
  </head>
  <body>
    <script>
      for(var i = 1; i <= 16; i++) {
        var myDiv = document.createElement('div');
        document.body.appendChild(myDiv);
      }
      function random(number) {
        return Math.floor(Math.random()*number);
      }
      function bgChange() {
        var rndCol = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')';
        return rndCol;
      }
      var divs = document.querySelectorAll('div');
      for(var i = 0; i < divs.length; i++) {
        divs[i].onclick = function(e) {
          e.target.style.backgroundColor = bgChange();
        }
      }
    </script>
  </body>
</html>
```

有很多个 div ，每一个点击的时候都会设置一个背景色，有了 e.target ，我们就不用一个个的去选择这些 div 了。

## 阻止默认行为

有时候我们不希望事件执行自己的默认行为。常见的一个例子是一个注册表单，当用户添加信息完毕点提交按钮的时候，默认行为是数据就会马上提交到服务器了。但是实际中，开发者经常希望组织这种默认行为，而是先进行一下表单验证，如果用户提交信息有误，可以显示报错信息。

看下面这个表单

```html
<form>
  <div>
    <label for="fname">First name: </label>
    <input id="fname" type="text">
  </div>
  <div>
    <label for="lname">Last name: </label>
    <input id="lname" type="text">
  </div>
  <div>
     <input id="submit" type="submit">
  </div>
</form>
<p></p>
```

如果想组织提交按钮的默认行为，就要使用 `preventDefault()` 函数。

```js
var form = document.querySelector('form')
var fname = document.getElementById('fname')
var lname = document.getElementById('lname')
var submit = document.getElementById('submit')
var para = document.querySelector('p')

form.onsubmit = function(e) {
  if (fname.value === '' || lname.value === '') {
    e.preventDefault()
    para.textContent = 'You need to fill in both names!'
  }
}
```

添加的 JS 代码会检查用户填写信息是否为空，如果是就用 `e.preventDefault` 阻止提交，然后显示报错。

## 参考

* https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events
