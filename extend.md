---
title: 类的继承是个啥？
---

### 面向对象小案例


```
class Block {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  area() {
    console.log(this.width * this.height);
  }
  addWidthHeight() {
    console.log(this.width + this.height);
  }
}

let block1 = new Block(2,3);
let block2 = new Block(4,7);
block1.area();
block1.addWidthHeight();
block2.area();
block2.addWidthHeight();
```

单纯从这个小例子中不能看出面向对象的强大之处，但是后续我们的逻辑变得越来越复杂，
面向对象思想的优势，例如更好的模块化，更高的代码复用，更加易读的代码，就会体现出来。


### 类的继承

先来看一下基础语法：

```
class Person {
  bodyHeight() {
    console.log('bodyHeight around 1.7m!');
  }
}
```

```
class Men {
  sayGender() {
    console.log('my gender Male');
  }
}
```

```
let peter = new Men;
peter.sayGender();
peter.bodyHeight();
```

在当前条件下 Person 类和 Men 类，没有任何关系，导致 peter.bodyHeight() 是肯定不能用的。
那么，我们要给 Person 和 Men 简历一种什么样的关系，才能让 Men 中，复用 Person 中的方法呢？

答案：就是让 Men 继承 Person 。


具体的语法如下：


```
class Person {
  bodyHeight() {
    console.log('bodyHeight around 1.7');
  }
}

class Men extends Person {
  gender() {
    console.log('my gender Male');
  }
}

class Women extends Person {
  gender() {
    console.log('my gender Female');
  }
}

// 现在我们就有了一个父类，Person ，两个子类，Men 和 Women 。

let peter = new Men;
let billie = new Women;
peter.gender();
billie.gender();
// 以上的两个调用肯定可以实现，因为 gender() 已经在 Men 和 Women 两个类之中直接定义了
// 但是同时，因为 Men/Women 都**继承**自 Person ，所以在 peter/billie 两个对象上
// 也一样可以使用 bodyHeight() 方法
peter.bodyHeight();
billie.bodyHeight();
```

到目前为止，**继承** 这个知识点似乎非常简单，只需要我们记住 extends （ 英文本意是 拓展 )
这个单词而已。但是下面我们来说点复杂的。

### super() 方法在类继承中的作用

我们现在来看，既然方法可以被继承，那么属性当然也应该是可以被继承的。

```
class Person {
  constructor() {
    this.weight = "around 100kg";
    this.height = "around 170cm";
  }
}
class Men extends Person {
  constructor() {
    super();
    this.gender = "Male";
  }
}

let peter = new Men;
console.log(peter.weight);
```

问题是，在上面的代码中，如果没有 super() 调用，那么子类中就不允许使用 this ，报错信息是

```
repl: 'this' is not allowed before super()
   8 |   constructor() {
   9 |     // super();
> 10 |     this.gender = "Male";
     |     ^
  11 |   }
  12 | }
```

那么，super() 到底是什么呢？


答案是这个样子的：子类的 this 是基于父类的 this 的（先创建父类的对象，然后再在上面进行增加）
，也就是说在父类对象没有被创建的时候，子类是没有办法被创建的。而 super() 指的就是父类的
constructor() 所以添加了 super() 在子类中，问题就解决了。

经验就是：子类的 constructor() 中必须先呼叫 super() ，然后才能使用 this 。

class 的一些注意点：

- class 名首字母大写
- class 内部通常写一个个方法
- class 的方法之间不需要符号链接
