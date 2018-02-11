---
title: 如何用 Webpack+Babel 来编译 ES6 ?
---

基本的 ES6 的转换其实有 Babel 自己就够了，但是涉及到 ES6 模块，就需要 Webpack 这个打包工具的参与了。Webpack 使用的更多技巧可以参考 [好奇猫#Webpack-React 环境搭建技巧](http://haoqicat.com/webpack-react-tricks) 课程。我们这一集里面做一个最简单的版本，达成：

- 能编译 ES6
- 能打包 ES6 模块

这两个目标即可。这个环境实际开发中用显得简陋了，但是在学习 ES6 基础的时候用是正好合适的。


### 新建 node 项目

新建项目文件夹

```
mkdir es6-compile
cd es6-compile
```

初始化 node 项目

```
npm init // 生成 `package.json`
```

### 安装需要的包

安装 webpack，babel 的 npm 包


```
npm install --save-dev webpack babel-loader babel-core babel-preset-env
```

`--save-dev` 的作用就是把包的版本信息保存的 package.json 中的恰当位置。

更多信息参考：

- [preset-env 的说明](http://babeljs.io/docs/plugins/preset-env/) 。

### 书写 Webpack 和 Babel 的配置文件

首先要保证 Babel 的正常运行，需要在项目根目录下创建 .babelrc 配置文件，内容如下：

```
{
  "presets": ["env"]
}
```


然后，webpack 使用时，也需要增加它的配置文件，在配置文件里，记录 webpack 各项配置，它的配置文件名默认 `webpack.config.js`

```js
var path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'src/index.js'),
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    module: {
      loaders: [
        {
          test: /\.js$/,
          exclude: /node_modules/,
          loader: "babel-loader"
        }
      ]
    }
};

```

上面的配置文件中，有三大要素需要知道，具体语法可以不用死记：

- 输入文件 index.js ，里面是我们手写的 ES6 代码
- 输出文件 bundle.js ，里面的代码浏览器是可以原生支持的
- 指定的编译器 babel ，babel 使用方式是作为一个 webpack 的 loader


### 添加 npm 脚本

为了每次运行命令方便，到 package.json 文件中，把 script 一项改为

```
"scripts": {
  "build": "webpack"
},
```

这样，以后每次编译项目就

```
npm run build
```

即可。

### 实际操作一下

先来添加源码，创建

src/index.js 内容如下：

```js
import hello from './my-module'

console.log(hello)
```

src/my-module.js 内容如下：

```js
let name = 'Peter';

export default name;
```

命令行中运行

```
npm run build
```

就可以得到 `dist/bunle.js` 这个问题了，运行命令

```
$ node dist/build.js
Peter
```

输出 `Peter` ，表示我们的环境已经运转正常了。
