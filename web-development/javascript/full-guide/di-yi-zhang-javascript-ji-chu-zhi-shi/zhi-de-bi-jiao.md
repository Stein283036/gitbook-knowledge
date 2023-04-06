# 值的比较

### 比较结果为 Boolean 类型

所有比较运算符均返回布尔值：

* `true`
* `false`

```javascript
alert( 2 > 1 );  // true（正确）
alert( 2 == 1 ); // false（错误）
alert( 2 != 1 ); // true（正确）
```

### 字符串比较

在比较字符串的大小时，因为 JS 中使用 Unicode-16 存储字符，因此比较字符串的时候是按照字符串的字符一一对应并且比较它们的 Unicode 码。

```javascript
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
alert('apple' < 'Apple'); // false，因为 字符 a 的 Unicode 码 97 大于 字符 A 的 Unicode 码 65
```

字符串的比较算法非常简单：

1. 首先比较两个字符串的**首位字符**大小。
2. 如果一方字符较大（或较小），则该字符串大于（或小于）另一个字符串。算法结束。
3. 否则，如果两个字符串的首位字符相等，则继续取出两个字符串各自的后一位字符进行比较。
4. 重复上述步骤进行比较，直到比较完成某字符串的所有字符为止。
5. 如果两个字符串的字符同时用完，那么则判定它们相等，否则未结束（还有未比较的字符）的字符串更大

### 不同类型间的比较

当对不同类型的值进行比较时，JavaScript 会首先将其转化为数字（number）再判定大小。

```javascript

alert( '2' > 1 ); // true，字符串 '2' 会被转化为数字 2
alert( '01' == 1 ); // true，字符串 '01' 会被转化为数字 1
```

对于布尔类型值，`true` 会被转化为 `1`、`false` 转化为 `0`。

```javascript
alert( true == 1 ); // true
alert( false == 0 ); // true
```

{% hint style="info" %}
一个有趣的现象

有时候，以下两种情况会同时发生：

* 若直接比较两个值，其结果是相等的。
* 若把两个值转为布尔值，它们可能得出完全相反的结果，即一个是 `true`，一个是 `false`。

例如：

```javascript

let a = 0;
alert( Boolean(a) ); // false

let b = "0";
alert( Boolean(b) ); // true

alert(a == b); // true!
```

对于 JavaScript 而言，这种现象其实挺正常的。因为 **JavaScript 会把待比较的值转化为数字后再做比较**（因此 `"0"` 变成了 `0`）。若只是将一个变量转化为 `Boolean` 值，则会使用其他的类型转换规则。== 只比较数据的值，而不比较值的类型。如果要比较值的类型，那么需要使用 ===。
{% endhint %}

#### 严格相等

普通的相等性检查 `==` 存在一个问题，它不能区分出 `0` 和 `false`：

```javascript
alert( 0 == false ); // true
```

也同样无法区分空字符串和 `false`：

```javascript

alert( '' == false ); // true
```

这是因为在比较不同类型的值时，处于相等判断符号 `==` 两侧的值会**先被转化为数字**。空字符串和 `false` 也是如此，转化后它们都为数字 0。

**严格相等运算符 `===` 在进行比较时不会做任何的类型转换。**

换句话说，如果 `a` 和 `b` 属于不同的数据类型，那么 `a === b` 不会做任何的类型转换而立刻返回 `false`。

```javascript
alert( 0 === false ); // false，因为被比较值的数据类型不同
```

同样的，与“不相等”符号 `!=` 类似，“严格不相等”表示为 `!==`。

### 对 null 和 undefined 进行比较

当使用严格相等 `===` 比较二者时

它们不相等，因为它们属于不同的类型。

```javascript
alert( null === undefined ); // false
```

当使用非严格相等 `==` 比较二者时

JavaScript 存在一个特殊的规则，会判定它们相等。

```javascript
alert( null == undefined ); // true
```

当使用数学式或其他比较方法 `< > <= >=` 时：

`null/undefined` 会被转化为数字：**`null` 被转化为 `0`**，**`undefined` 被转化为 `NaN`**。

<details>

<summary>奇怪的结果：null vs 0</summary>

通过比较 `null` 和 0 可得：

```javascript

alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
```

上面的结果完全打破了你对数学的认识。在最后一行代码显示“`null` 大于等于 0”的情况下，前两行代码中一定会有一个是正确的，然而事实表明它们的结果都是 false。

为什么会出现这种反常结果，这是因为相等性检查 `==` 和普通比较符 `> < >= <=` 的代码逻辑是相互独立的。进行值的比较时，`null` 会被转化为数字，因此它被转化为了 `0`。这就是为什么（3）中 `null >= 0` 返回值是 true，（1）中 `null > 0` 返回值是 false。

另一方面，**`undefined` 和 `null` 在相等性检查 `==` 中不会进行任何的类型转换，它们有自己独立的比较规则**，所以**除了它们之间互等外，不会等于任何除自己以外的其它值**。这就解释了为什么（2）中 `null == 0` 会返回 false。

</details>

<details>

<summary>特立独行的 undefined</summary>

`undefined` 不应该被与其他值进行比较：

```javascript
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```

原因如下：

* `(1)` 和 `(2)` 都返回 `false` 是因为 `undefined` 在比较中被转换为了 `NaN`，而 `NaN` 是一个特殊的数值型值，它与任何值进行比较都会返回 `false`。是的，包括与它自己进行比较依然返回 `false`。
* `(3)` 返回 `false` 是因为这是一个相等性检查，而 `undefined` 只与 `null` 相等，不会与其他值相等。

</details>

{% hint style="info" %}
**避免问题**

不不需要时刻记得这些古怪的规则，虽然随着代码写得越来越多，我们对这些规则也都会烂熟于胸，但是我们需要更为可靠的方法来避免潜在的问题：

* 除了严格相等 `===` 外，其他但凡是有 `undefined/null` 参与的比较，我们都需要格外小心。
* 除非你非常清楚自己在做什么，否则永远不要使用 `>= > < <=` 去比较一个可能为 `null/undefined` 的变量。对于取值可能是 `null/undefined` 的变量，请按需要分别检查它的取值情况。
* 在非严格相等 == 下，null 和 undefined 相等且各自不等于除自身任何其他的值。
{% endhint %}

### 练习

```javascript
5 > 4 // true
"apple" > "pineapple" // false
"2" > "12" // false
undefined == null // true
undefined === null // false，undefined 和 null 的数据类型不相同
null == "\n0\n" // false，null 只与 undefined 和其自身相等
null === +"\n0\n" // false
```
