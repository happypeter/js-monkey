---
title: 异常处理语句怎么写？
---

你可以用 throw 语句抛出一个异常并且用 try...catch 语句捕获处理它。

- throw statement
- try...catch statement

### 异常类型（Exception Types）

JavaScript 可以抛出任意对象。然而，不是所有对象能产生相同的结果。尽管抛出数值或者字母串作为错误信息十分常见，但是通常用下列其中一种异常类型来创建目标更为高效：

- ECMAScript exceptions
- DOMException and DOMError

### 抛出语句（throw Statement）

使用 throw 语句抛出一个异常。当你抛出异常，你规定一个含有值的表达式要被抛出。

```
throw expression;
```

你可以抛出任意表达式而不是特定一种类型的表达式。下面的代码抛出了几个不同类型的表达式：

```
throw "Error2";   // 字符串
throw 42;         // 数字
throw true;       // 布尔值
throw {toString: function() { return "I'm an object!"; } };
```

> 注意：你可以在抛出异常时声明一个对象。那你就可以在捕捉块中查询到对象的属性。下面的例子创建了一个UserException类型的对象myUserException用在抛出语句中。

```
// Create an object type UserException
function UserException(message) {
  this.message = message;
  this.name = "UserException";
}

// Make the exception convert to a pretty string when used as a string
// (e.g. by the error console)
UserException.prototype.toString = function() {
  return this.name + ': "' + this.message + '"';
}

// Create an instance of the object type and throw it
throw new UserException("Value too high");
```

### try...catch 语句

try...catch 语句标记一块待尝试的语句，并规定一个以上的响应应该有一个异常被抛出。如果我们抛出一个异常，try...catch 语句就捕获它。

try...catch 语句有一个包含一条或者多条语句的try代码块，0个或多个的catch代码块，catch代码块中的语句会在try代码块中抛出异常时执行。 换句话说，如果你在try代码块中的代码如果没有执行成功，那么你希望将执行流程转入catch代码块。如果try代码块中的语句（或者try 代码块中调用的方法）一旦抛出了异常，那么执行流程会立即进入catch 代码块。如果try代码块没有抛出异常，catch代码块就会被跳过。finally 代码块总会紧跟在try和catch代码块之后执行，但会在try和catch代码块之后的其他代码之前执行。

下面的例子使用了try...catch语句。示例调用了一个函数用于从一个数组中根据传递值来获取一个月份名称。如果该值与月份数值不相符，会抛出一个带有"InvalidMonthNo"值的异常，然后在捕捉块语句中设monthName变量为unknown。

```
function getMonthName(mo) {
  mo = mo - 1; // Adjust month number for array index (1 = Jan, 12 = Dec)
  var months = ["Jan","Feb","Mar","Apr","May","Jun","Jul",
                "Aug","Sep","Oct","Nov","Dec"];
  if (months[mo]) {
    return months[mo];
  } else {
    throw "InvalidMonthNo"; //throw keyword is used here
  }
}

try { // statements to try
  monthName = getMonthName(myMonth); // function could throw exception
}
catch (e) {
  monthName = "unknown";
  logMyErrors(e); // pass exception object to error handler -> your own function
}
```

##### 捕捉块（The catch Block）

你可以使用捕捉块来处理所有可能在 try 代码块中产生的异常。

```
catch (catchID) {
  statements
}
```

捕捉块指定了一个标识符 (上述语句中的 catchID ）来存放抛出语句指定的值；你可以用这个标识符来获取抛出的异常信息。在插入捕捉块时 JavaScript 创建这个标识符；标识符只存在于捕捉块的存续期间里；当捕捉块执行完成时，标识符不再可用。

举个例子，下面代码抛出了一个异常。当异常出现时跳到捕捉块（the catch block）。

```
try {
  throw "myException"; // 生成异常
}
catch (e) {
  // 处理任何异常语句
  logMyErrors(e); // 通过异常对象错误处理程序
}
```

##### 终结块（The finally Block）

终结块包含了在 try 和 catch 块完成后、下面接着的 try...catch 语句之前执行的语句。终结块无论是否抛出异常都会执行。如果抛出了一个异常，就算没有异常处理，终结块里的语句也会执行。

你可以用终结块来令你的脚本在异常发生时优雅地退出；举个例子，你可能需要在绑定的脚本中释放资源。接下来的例子用文件处理语句打开了一个文件（服务端的 JavaScript 允许你进入文件）。如果在文件打开时一个异常抛出，终结块会在脚本错误之前关闭文件。

```
openMyFile();
try {
  writeMyFile(theData); // 这个过程可能发生异常
} catch(e) {  
  handleError(e); // 处理获取到的异常
} finally {
  closeMyFile(); // 关闭源文件
}
```

如果终结块返回一个值，该值会是整个 try-catch-finally 流程的返回值，不管在 try 和 catch 块中语句返回了什么：

```
function f() {
  try {
    console.log(0);
    throw "bogus";
  } catch(e) {
    console.log(1);
    return true; // 这个 return 语句将被暂停,直到 finally 块已完成
    console.log(2); // 不会执行
  } finally {
    console.log(3);
    return false; // 覆盖之前的 return
    console.log(4); // 不会执行
  }
  // "return false" 现在被执行
  console.log(5); // 不会执行
}
f(); // 输出 0, 1, 3; returns false
```

通过 finally 块覆盖返回值也适用于抛出异常或重复抛出异常的 catch 块:

```
function f() {
  try {
    throw "bogus";
  } catch(e) {
    console.log('caught inner "bogus"');
    throw e; // 这个 return 语句将被暂停,直到 finally 块已完成
  } finally {
    return false; // 覆盖之前的 return
  }
  // "return false" 现在被执行
}

try {
  f();
} catch(e) {
  // 这里永远不会执行因为在 catch 内部的 throw 被 finally 中的 return 覆盖
  console.log('caught outer "bogus"');
}

// 输出
// caught inner "bogus"
```

##### 嵌套 try...catch 语句

你可以嵌套一个或多个 try...catch 语句。如果一个内部的 try...catch 语句没有捕捉块（catch block），将会启动匹配外部的 try...catch 语句的捕捉块（catch block）。

### 错误匹配对象（Utilizing Error objects）

根据错误类型，你也许可以用 'name' 和 'message' 获取更精炼的信息。'name' 提供了常规的错误类(e.g., 'DOMException' or 'Error')，而 'message' 通常提供了一条从错误对象转换成字符串的简明信息。

在抛出你个人所为的异常时，为了充分利用那些属性（比如你的 catch 块不能分辨是你个人所为的异常还是系统的异常时），你可以使用错误构造函数（the Error constructor）。比如：

```
function doSomethingErrorProne () {
  if (ourCodeMakesAMistake()) {
    throw (new Error('The message'));
  } else {
    doSomethingToGetAJavascriptError();
  }
}
....
try {
  doSomethingErrorProne();
}
catch (e) {
  console.log(e.name); // logs 'Error'
  console.log(e.message); // logs 'The message' or a JavaScript error message)
}
```
