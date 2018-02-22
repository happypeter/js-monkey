历史上，JavaScript 一直没有模块（module）体系，无法将一个大程序拆分成互相依赖的小文件，再用简单的方法拼装起来。其他语言都有这项功能，比如 Ruby 的 require、Python 的 import，甚至就连 CSS 都有 @import，但是 JavaScript 任何这方面的支持都没有，这对开发大型的、复杂的项目形成了巨大障碍。

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代现有的 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

模块功能主要由两个命令构成：export 和 import 。export 命令用于规定模块的对外接口，import 命令用于输入其他模块提供的功能。来看一个 Hello World 级的例子。

先写一个 user.js

```js
let name = 'Peter'
export { name }
```

上面的文件中有 export 语句，那么这个文件可以被叫做一个 ES6 模块。那么在 index.js 中可以这样来使用这个模块：

```js
import { name } from './user'
console.log(name)
```

比较麻烦的步骤可能就是编译了，需要搭建一下 Webpack-babel 的环境，参考 [好奇猫上的课程视频](http://haoqicat.com/webpack-react-tricks/)

```
npm run build
```

就可以得到 dist/bundle.js 文件了。

```
$ node bundle.js
Peter
```

可以看到正确的输出。粗略的可以认为 bundle.js 就是 index.js 和 user.js 的合体。
