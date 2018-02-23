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


另外，babel 也可以转译 react 的 jsx 语法。

### 集成环境

很多脚手架程序都内置集成了 babel ，所以不需要我们来安装配置，默认就可以支持 es6 和 jsx 。例如，create-react-app 和 gatsby 。
