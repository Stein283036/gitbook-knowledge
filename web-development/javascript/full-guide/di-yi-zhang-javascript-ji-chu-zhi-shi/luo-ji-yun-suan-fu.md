# 逻辑运算符

JavaScript 中有四个逻辑运算符：`||`（或），`&&`（与），`!`（非），`??`（空值合并运算符）。本文介绍前三个，在下一篇文章中再详细介绍 `??` 运算符。

### ||（或）&#x20;

```javascript

alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```

除了两个操作数都是 `false` 的情况，结果都是 `true`。

如果操作数不是布尔值，那么它将会被**转化为布尔值**来参与运算。

例如，数字 `1` 被作为 `true` 处理，数字 `0` 则被作为 `false`：

```javascript
if (1 || 0) { // 工作原理相当于 if( true || false )
  alert( 'truthy!' );
}
```

大多数情况下，逻辑或 `||` 会被**用在 `if` 语句中**，用来测试是否有 **任何** 给定的条件为 `true`。

### 或运算寻找第一个真值

给定多个参与或运算的值：

```javascript
result = value1 || value2 || value3;
```

或运算符 `||` 做了如下的事情：

* 从左到右依次计算操作数。
* 处理每一个操作数时，都将其转化为布尔值。如果结果是 `true`，就停止计算，返回这个操作数的初始值。
* 如果所有的操作数都被计算过（也就是，转换结果都是 `false`），则返回最后一个操作数。

**返回的值是操作数的初始形式，不会做布尔转换。**

换句话说，一个或运算 `||` 的链，将返回第一个真值，**如果不存在真值，就返回该链的最后一个值**。

```javascript
alert( 1 || 0 ); // 1（1 是真值）

alert( null || 1 ); // 1（1 是第一个真值）
alert( null || 0 || 1 ); // 1（第一个真值）

alert( undefined || null || 0 ); // 0（都是假值，返回最后一个值）
```

### &&（与）

两个 & 符号表示 `&&` 与运算符：

```javascript
result = a && b;
```

在传统的编程中，当两个操作数都是真值时，与运算返回 `true`，否则返回 `false`：

```javascript
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

### 与运算寻找第一个假值

给出多个参加与运算的值：

```javascript
result = value1 && value2 && value3;
```

与运算 `&&` 做了如下的事：

* 从左到右依次计算操作数。
* 在处理每一个操作数时，都将其转化为布尔值。如果结果是 `false`，就停止计算，并返回这个操作数的初始值。
* **如果所有的操作数都被计算过（例如都是真值），则返回最后一个操作数。**

换句话说，与运算返回第一个假值，如果没有假值就返回最后一个值。

```javascript
// 如果第一个操作数是真值，
// 与运算返回第二个操作数：
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5

// 如果第一个操作数是假值，
// 与运算将直接返回它。第二个操作数会被忽略
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
```

在一行代码上串联多个值。查看第一个假值是如何被返回的：

```javascript
alert( 1 && 2 && null && 3 ); // null
```

如果所有的值都是真值，最后一个值将会被返回：

```javascript
alert( 1 && 2 && 3 ); // 3，最后一个值
```

### !（非）

感叹符号 `!` 表示布尔非运算符。

语法相当简单：

```javascript
result = !value;
```

逻辑非运算符接受一个参数，并按如下运作：

1. 将操作数转化为布尔类型：`true/false`。
2. 返回相反的值。

```javascript
alert( !true ); // false
alert( !0 ); // true
```

**两个非运算 `!!` 有时候用来将某个值转化为布尔类型**：

```javascript
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

也就是，**第一个非运算将该值转化为布尔类型并取反，第二个非运算再次取反**。最后我们就得到了一个任意值到布尔值的转化。

有一个略显冗长的方式也可以实现同样的效果 —— 一个内建的 `Boolean` 函数：

```javascript
alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```

**非运算符 `!` 的优先级在所有逻辑运算符里面最高，所以它总是在 `&&` 和 `||` 之前执行。**
