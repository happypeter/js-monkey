---
title: ES6 模块的两种导出方式是什么？
---

简单来说一句话：一个是**命名导出**，一个是**默认导出** 。

前面在 [ES6 模块的最基本的使用方式是什么？](http://haoduoshipin.com/v/209.html) 这一集里面讲了模块的基础知识，这集把这两种导出方式具体演示一下。没啥？很简单的。

### 命名导出

命名导出（ Named Exports ）的具体使用方式，看个例子就明白了。


my-module.js 内容如下：

```
function cube(x) {
  return x * x * x;
}
const foo = Math.PI;
export { cube, foo };
```

index.js 这样写：

```
import { cube, foo } from './my-module';
console.log(cube(3)); // 27
console.log(foo);    // 3.1415...
```

命名导出的特点就是一次可以方便的导出多个变量。注意，上面 `./my-module` 中的 `./` 是必须要有的，因为 my-module 是一个自制模块，所以必须要写路径。

### 默认导出

默认导出（ Default Export )


my-module.js 内容如下：

```
export default function cube(x) {
  return x * x * x;
}
```

index.js 的导入的方式有些差别，不用花括号了：

```
import cube from './my-module';
console.log(cube(3)); // 27
```

需要注意的是， `export default` 后面直接不能跟 var ，let 和 const 。也就是下面的几种写法是不对的：

```
export default let name = 'Peter';
export default var name = 'Peter';
export default const name = 'Peter';
```

但是可以写成下面这样：

```
let name = 'Peter';
export default name;
```

### 参考资料

- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
