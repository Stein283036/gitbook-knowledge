# 循环：while 和 for

**循环** 是一种重复运行同一代码的方法。

基础的循环：`while`，`do..while` 和 `for(..; ..; ..)`。

用于遍历对象属性的 for..in 循环请见：for…in。

用于遍历数组和可迭代对象的循环分别请见：for…of 和 iterables。

### “while” 循环

while 循环的语法如下：

```javascript

while (condition) {
  // 代码
  // 所谓的“循环体”
}
```

任何表达式或变量都可以是循环条件，而不仅仅是比较。在 `while` 中的循环条件会被计算，计算结果会被转化为布尔值。

例如，`while (i != 0)` 可简写为 `while (i)`：

```javascript
let i = 3;
while (i) { // 当 i 变成 0 时，条件为假，循环终止
  alert( i );
  i--;
}
```

### “do…while” 循环

语法：

```javascript
do {
  // 循环体
} while (condition);
```

这种形式的语法很少使用，除非你希望不管条件是否为真，循环体 **至少执行一次**。通常我们更倾向于使用另一个形式：`while(…) {…}`。

### “for” 循环

`for` 循环更加复杂，但它是最常使用的循环形式。语法如下：

```javascript
for (begin; condition; step) {
    // 循环体
}
```

### 跳出循环

通常条件为假时，循环会终止。

但我们随时都可以使用 `break` 指令强制退出。

### 继续下一次迭代

`continue` 指令是 `break` 的“轻量版”。它不会停掉整个循环。而是停止当前这一次迭代，并强制启动新一轮循环（如果条件允许的话）。

如果我们完成了当前的迭代，并且希望继续执行下一次迭代，我们就可以使用它。

下面这个循环使用 `continue` 来只输出奇数：

```javascript
for (let i = 0; i < 10; i++) {

  //如果为真，跳过循环体的剩余部分。
  if (i % 2 == 0) continue;

  alert(i); // 1，然后 3，5，7，9
}
```

### break/continue 标签

有时候我们需要一次从多层嵌套的循环中跳出来。

例如，下述代码中我们的循环使用了 `i` 和 `j`，从 `(0,0)` 到 `(3,3)` 提示坐标 `(i, j)`：

```javascript
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // 如果我想从这里退出并直接执行 alert('Done!')
  }
}

alert('Done!');
```

我们需要提供一种方法，以在用户取消输入时来停止这个过程。

在 `input` 之后的普通 `break` 只会打破内部循环。这还不够 —— 标签可以实现这一功能！

**标签** 是在循环之前带有冒号的标识符：

```javascript
labelName: for (...) {
  ...
}
```

`break <labelName>` 语句跳出循环至标签处：

```javascript
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // 如果是空字符串或被取消，则中断并跳出这两个循环。
    if (!input) break outer; // (*)

    // 用得到的值做些事……
  }
}

alert('Done!');
```
