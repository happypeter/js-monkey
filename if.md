---
title: 条件判断语句长成啥样？
---

条件判断语句指的是根据指定的条件所返回的结果（真或假或其它预定义的），来执行特定的语句。JavaScript提供了两种条件判断语句：`if...else` 和 `switch`。

### `if...else` 语句

当一个逻辑条件为真，用if语句执行一个语句。当这个条件为假，使用可选择的else从句来执行这个语句。if语句如下所示：

```
if (condition) {
  statement_1;
} else {
  statement_2;
} // else 可选
```

`condition` 可以是任何返回结果是 `true` 或 `false` 的表达式。如果 `condition` 表达式返回的是 `true`，`statement_1` 会被执行；否则，`statement_2` 被执行。`statement_1` 和 `statement_2` 可以是任何语句，甚至你可以将另一个 `if` 语句嵌套其中。

你也可以组合语句通过使用 `else if` 来测试连续的多种条件判断，就像下面这样：

```
if (condition_1) {
  statement_1;
} else if (condition_2) {
  statement_2;
} else if (condition_n) {
  statement_n;
} else {
  statement_last;
}
```

为了防止在多个条件情况下，只有第一个逻辑条件为 `true` 是才会被执行。要执行多个语句，使用语句块 ({ ... }) 来分组这些语句。一般情况下，总是使用语句块是一个好的习惯，特别是在代码涉及比较多的 if 语句时：

```
if (condition) {
  statement_1_runs_if_condition_is_true;
  statement_2_runs_if_condition_is_true;
} else {
  statement_3_runs_if_condition_is_false;
  statement_4_runs_if_condition_is_false;
}
```

在条件表达式中最好不要使用“=”来判断条件是否相等，因为这会产生非预期结果。不要使用下面的代码：

```
if (x = y) {
  /* statements here */
}
```

如果你需要在条件表达式中使用赋值，一个共同的习惯是在赋值语句前后额外的添加一对括号。例如：

```
if ((x = y)) {
  /* statements here */
}
```

##### Falsy values

下面这些值将被计算出 `false` （也被称为 Falsy values）：

```
false
undefined
null
0
NaN
the empty string ("")
```

当传递给条件语句时，所有其他值，包括所有对象会被计算为 `true`。

请不要混淆原始的布尔值 true 和 false 与 布尔对象的值 true 和 false（下例中 b 属于对象，会被计算为true）。例如：

```
var b = new Boolean(false);
if (b) // 返回 true
if (b == true) // 返回 false
```

##### 例如

在下面的例子中，如果一个文本对象中的字符串长度是3，函数 checkData 返回 true；否则，函数显示一个 alert 的弹出框消息并返回 false。

```
function checkData() {
  if (document.form1.threeChar.value.length == 3) {
    return true;
  } else {
    alert("Enter exactly three characters. " +
    document.form1.threeChar.value + " is not valid.");
    return false;
  }
}
```

### switch 语句

switch 语句允许一个程序求一个表达式的值并且尝试去匹配表达式的值到一个 case label。如果匹配成功，这个程序执行相关的语句。swich 语句如下所示：

```
switch (expression) {
  case label_1:
    statements_1
    [break;]
  case label_2:
    statements_2
    [break;]
    ...
  default:
    statements_def
    [break;]
}
```

程序首先查找一个与 `expression` 匹配的 `case` 语句，然后将控制权转移到该子句，执行相关的语句。如果没有匹配值， 程序会去找 `default` 语句，如果找到了，控制权转移到该子句，执行相关的语句。如果没有找到 `default`，程序会继续执行 switch 语句后面的语句。default 语句通常出现在switch语句里的最后面，当然这不是必须的。

可选的 break 语句与每个 case 语句相关联， 保证在匹配匹配的语句被执行后程序可以跳出 switch 并且继续执行 switch 后面的语句。如果不写 break , 程序将继续执行 switch 中的语句。

##### 示例

在如下示例中, 如果 fruittype 等于 "Bananas", 程序匹配到对应 "Bananas" 的case 语句，并执行相关语句。 当执行到 break 时，程序结束了 switch 并执行 switch 后面的语句。 如果不写 break ，那么程序将会执行 case "Cherries" 下的语句。

```
switch (fruittype) {
  case "Oranges":
    console.log("Oranges are $0.59 a pound.");
    break;
  case "Apples":
    console.log("Apples are $0.32 a pound.");
    break;
  case "Bananas":
    console.log("Bananas are $0.48 a pound.");
    break;
  case "Cherries":
    console.log("Cherries are $3.00 a pound.");
    break;
  case "Mangoes":
    console.log("Mangoes are $0.56 a pound.");
    break;
  case "Papayas":
    console.log("Mangoes and papayas are $2.79 a pound.");
    break;
  default:
   console.log("Sorry, we are out of " + fruittype + ".");
}
console.log("Is there anything else you'd like?");
```
