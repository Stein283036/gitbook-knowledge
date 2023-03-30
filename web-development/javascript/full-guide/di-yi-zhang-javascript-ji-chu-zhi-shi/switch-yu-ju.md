# "switch" 语句

`switch` 语句可以替代多个 `if` 判断。

`switch` 语句为多分支选择的情况提供了一个更具描述性的方式。

### 语法

`switch` 语句有至少一个 `case` 代码块和一个可选的 `default` 代码块。

```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

* 比较 `x` 值与第一个 `case`（也就是 `value1`）是否**严格相等**，然后比较第二个 `case`（`value2`）以此类推。
* 如果相等，`switch` 语句就执行相应 `case` 下的代码块，直到遇到最靠近的 `break` 语句（或者直到 `switch` 语句末尾）。
* 如果没有符合的 case，则执行 `default` 代码块（如果 `default` 存在）。

**如果没有 `break`，程序将不经过任何检查就会继续执行下一个 `case`。**

{% hint style="info" %}
任何表达式都可以成为 `switch/case` 的参数

`switch` 和 `case` 都允许任意表达式。

比如：

```javascript
let a = "1";
let b = 0;

switch (+a) {
  case b + 1:
    alert("this runs, because +a is 1, exactly equals b+1");
    break;

  default:
    alert("this doesn't run");
}
```

这里 `+a` 返回 `1`，这个值跟 `case` 中 `b + 1` 相比较，然后执行对应的代码。
{% endhint %}

### “case” 分组

```javascript
let a = 3;

switch (a) {
  case 4:
    alert('Right!');
    break;

  case 3: // (*) 下面这两个 case 被分在一组
  case 5:
    alert('Wrong!');
    alert("Why don't you take a math class?");
    break;

  default:
    alert('The result is strange. Really.');
}
```

### 类型很关键

强调一下，这里的相等是严格相等。被比较的值必须是相同的类型才能进行匹配。

```javascript
let arg = prompt("Enter a value?")
switch (arg) {
  case '0':
  case '1':
    alert( 'One or zero' );
    break;

  case '2':
    alert( 'Two' );
    break;

  case 3:
    alert( 'Never executes!' );
    break;
  default:
    alert( 'An unknown value' )
}
```

1. 在 `prompt` 对话框输入 `0`、`1`，第一个 `alert` 弹出。
2. 输入 `2`，第二个 `alert` 弹出。
3. 但是输入 `3`，因为 `prompt` 的结果是字符串类型的 `"3"`，不严格相等 `===` 于数字类型的 `3`，所以 `case 3` 不会执行！因此 `case 3` 部分是一段无效代码。所以会执行 `default` 分支。
