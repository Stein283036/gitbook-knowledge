# 代码结构

### 语句

语句是按照编程语言的规范来编写的执行特定行为的指令，比如前文出现的 `alert("Hello JavaScript");` 这就是一个符合 JavaScript 语法规范的指令，它的行为是在当前浏览器窗口中弹出 Hello JavaScript 警告信息。我们可以编写无数的 JS 语句来实现各种各种的任务，多个语句之间以 `;` 分隔，通常，一条独立的语句占一行，以提高代码的可读性，比如：

```
alert("Hello");
alert("JavaScript");
```

### 分号

上面我们看到 `;` 号是作为 JS 语句之间的分隔符，不过在大多数有换行符的情况下，`;` 可以省略，比如：

```javascript
alert('Hello')
alert('World')
```

在这，JavaScript 将换行符理解成“隐式”的分号。这也被称为 [自动分号插入](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion)。不过关于 JS 语句是否以 `;` 结尾一直是一个具有争议的问题，我的推荐是使用 `;` 作为语句的结尾。

### 注释

注释就是会被 JS 引擎忽略的代码，它的作用就是为了给代码做出解释、说明它们的功能，良好的注释习惯是开发人员必备的技能素养。

单行注释以两个正斜杠字符 // 开始。

```javascript
// 单行注释
```

多行注释

```javascript
/*
多行注释
*/
```

```javascript
/**
多行注释
*/
```
