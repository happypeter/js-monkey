## 事件冒泡和捕捉

英文： Event bubbling and capture

事件冒泡和捕捉的问题不是天天都会遇到，但是万一遇到了，要是不理解，还是真要命的。冒泡和捕捉是事件扩散的两种方式。当一个事件发生在套在另外一个元素中的元素之上，并且这两个元素都注册了相同的事件处理器。那事件扩散就有一个顺序问题了。

首先说，冒泡是向上的，而捕捉是向下的。

冒泡，最里面的元素的事件处理函数先执行，然后向父辈祖辈元素扩展。

捕捉，最外面的元素的事件处理函数先执行，让后一直向内部各级元素传递。

> 之所以会有这两种方式，是因为最早 netscape 浏览器是捕捉，而 IE 是冒泡，而当代浏览器是两个方式都支持。

默认情况下，浏览器都是冒泡的，不会捕捉，除非我们使用 `addEventListener(type, listener, useCapture)` 注册事件的时候专门把第三个参数传递 true 。

## 案例

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Show video box example</title>
    <style>
      div {
        position: absolute;
        top: 50%;
        transform: translate(-50%,-50%);
        width: 480px;
        height: 380px;
        border-radius: 10px;
        background-color: #eee;
        background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.1));
      }

      .hidden {
        left: -50%;
      }

      .showing {
        left: 50%;
      }

      div video {
        display: block;
        width: 400px;
        margin: 40px auto;
      }

    </style>
  </head>
  <body>
    <button>Display video</button>

    <div class="hidden">
      <video>
        <source src="rabbit320.mp4" type="video/mp4">
        <source src="rabbit320.webm" type="video/webm">
        <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
      </video>
    </div>

    <script>

      var btn = document.querySelector('button');
      var videoBox = document.querySelector('div');
      var video = document.querySelector('video');

      btn.onclick = function() {
        videoBox.setAttribute('class','showing');
      }

      videoBox.onclick = function() {
        videoBox.setAttribute('class','hidden');
      };

      video.onclick = function() {
        video.play();
      };

    </script>
  </body>
</html>
```

上面的例子中，一个 div 包裹了一个 video 标签。当点按钮的时候，video 标签会出现。但是，当我们点播放器试图执行 `video.play()` 的时候，由于冒泡原理，video 和 div 的 onClick 事件都会触发。于是视频虽然开始播放了，但是用户也看不到，因为 div 已经被隐藏了。

![](001-bubble.png)

要解决这个问题，就要用 `stopPropagation` 方法来阻止事件扩散。

```js
video.onclick = function(e) {
  e.stopPropagation()
  video.play()
}
```

把 video 的事件处理函数写成这样，事件就不会冒泡到 div 了，当然 div 也就不会被隐藏了。

## 事件代理

英文：Event delegation ，也翻译做事件委托。

冒泡机制下，我们还可以巧妙利用它来实现一种叫**事件代理**的效果。有时候我们希望在点击任何一个子元素的时候都执行特定的代码，此时就可以把事件监听器设置到父元素之上。这样就不用给每一个子元素都设置事件监听了。

一个非常好的例子就是，有一个列表，如果希望点击任一条目的时候都弹出一条信息，就可以把事件监听直接设置到 ul 元素上。

## 参考

* https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events

* https://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing
