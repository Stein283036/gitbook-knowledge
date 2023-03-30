# 条件分支：if 和 '?'

### “if” 语句

`if(...)` 语句计算括号里的条件表达式，如果计算结果是 `true`，就会执行对应的代码块。

```javascript
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) alert( 'You are right!' );
```

建议每次使用 if 语句都用大括号 `{}` 来包装代码块，即使只有一条语句。这样可以提高代码可读性。

### 布尔转换

`if (…)` 语句会计算圆括号内的表达式，并将计算结果转换为布尔型。

前文提到的 Boolean 类型转换规则：

* 数字 `0`、空字符串 `""`、`null`、`undefined` 和 `NaN` 都会被转换成 `false`。因为它们被称为“假值（falsy）”。
* 其他值被转换为 true，所以它们被称为“真值（truthy）”。

### “else” 语句

`if` 语句有时会包含一个可选的 “else” 块。如果判断条件不成立，就会执行它内部的代码。

```javascript
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) {
  alert( 'You guessed it right!' );
} else {
  alert( 'How can you be so wrong?' ); // 2015 以外的任何值
}
```

### 多个条件：“else if”

```javascript
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

可以有更多的 `else if` 块。结尾的 `else` 是可选的。

### 条件运算符 ‘?’

根据一个条件去赋值一个变量。

```javascript
let accessAllowed;
let age = prompt('How old are you?', '');

if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}

alert(accessAllowed);
```

这个运算符通过问号 `?` 表示。有时它被称为三元运算符，被称为“三元”是因为该运算符中有三个操作数。实际上它是 JavaScript 中唯一一个有三个操作数的运算符。

语法：

```javascript
let result = condition ? value1 : value2;
```

### 多个 ‘?’

```javascript
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

**不建议这样使用问号运算符。**

这种写法比 `if` 语句更短，但它的可读性差。

因为我们的眼睛垂直扫描代码。所以，跨越几行的代码块比长而水平的代码更易于理解。

问号 `?` 的作用是根据条件返回其中一个值。请正确使用它。当需要执行不同的代码分支时，请使用 `if`。
