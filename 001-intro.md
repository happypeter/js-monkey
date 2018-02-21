### Object Oriented Programming 面向对象编程

参考：http://haoqicat.com/o-o-js

基本概念：面向对象编程，是一种基于 **对象** 这个概念的编程方法论。对象中可以包含数据，一般被成为**属性** ，也可以包含函数，一般被成为**方法**。

### OOP: 类和对象

类（ class ）是多个对象（ object ）的抽象，对象是类的实例。人，就可以是一个类，比如人可以有名字，身高这些属性，但是没有具体值，所以说类可以理解为一个空的木桶。对象是类的实例，具体的一个人，就可以叫做

> 人这个类的一个对象

例如，Peter 就可以是人这个类的一个对象。对象的特点是有具体数据的，例如，给定一个人 Peter ，那我们可以得到他的具体的姓名，身高的具体值。所以对象可以理解为木桶中装的水。

下面用代码的形式来表述一下类和对象的关系。在面向对象编程的过程中，我们都是先定义类

```
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

上面 name 就是一个**属性** ，constructor() 是一个方法。

有了类之后，我们就可以实例化出，无穷多个对象了

```
let peter = new Person('happypeter');

console.log(peter.name);
```

上面 `new` 是一个关键字，意思是“新建一个该类的实例” 。得到的 `peter` 就是一个对象，我们可以得到 peter 中的 name 的具体值。

下面我们对一些不太好理解的点，再详细解释一下：

### constructor 构造函数

一个类里面可以定义多个方法，如下

```
class Person {
  constructor() {
    console.log('hello1');
  }
  sayHello2() {
    console.log('hello2');
  }
}
let peter = new Person;
```

上面 `constructor` 是一个特殊的方法（拼写是严格的），它的特点是在对象被创建的时候，也就 `let peter = new Person` 这一句执行的时候，自动被呼叫的一个方法。而其他的方法，都不会被自动执行。

同时，constructor 也可以接受参数，如下

```
class Person {
  constructor(name) {
    console.log('My Name is ' + name);
  }
}
let peter = new Person('peter');
```

如上，给 constructor 传递参数的方式，就是在 new 一个新对象的时候，在类名之后直接加括号来传递，例如 `Person('peter')` 。

### 定义自己的方法

constructor 是一个特殊的方法，它的拼写就是 constructor ，拼错了，就不会被自动执行了。或者说，就成了一个普通方法了。通常我们的类里面都会定义很多普通方法的。

```
class Person {
  sayHello(name) {
    console.log('hello ' + name);
  }
}
let peter = new Person;
```

那么创建新对象的时候，sayHello 是不会被自动执行的，那么如何来调用呢？

```
peter.sayHello('lily');
```

### this 关键字

this 指的就是当然对象

```
class Person {
  constructor(name) {

  }
  sayName() {
    console.log('my name is' + name);
  }
}
let peter = new Person('peter');
peter.sayName();
```

此时如果直接看 peter.sayName() 会发现 `name` 的值为空。

解决这个问题就可以使用 this 关键字。

```
class Person {
  constructor(name) {
    this.name = name;
  }
  sayName() {
    console.log('my name is' + this.name);
  }
}
let peter = new Person('peter');
peter.sayName();
```

这样 sayName() 函数中就可以拿到 this.name 的值了。
