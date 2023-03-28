# 数据类型

### JS 中的八种数据类型

原始数据类型

* String
* Number
* undefined
* null
* Boolean
* BigInt
* Symbol

引用数据类型

* Object

### Number

JS 中的数字类型没有整型和浮点型之分，只有一种表示数字的类型，即 `Number` 。常用的基本数字操作有：+、-、\*、/、\*\*（平方）、% 。数字也可以用来进行位运算，比如：`^`、`|`、`&`。

出来常规的数字字面量表示的数值以外，还有特殊的数字值也属于 Number 类型，这些值是：`Infinity`、`-Infinity` 和 `NaN` 。

Infinity 是数学中表示无穷大的概念，表示无穷大；-Infinity 则表示负无穷大，即无穷小的概念；NaN 即 Not a Number，它是用来表示对一个不正确的数学运算结果的表示。

```javascript
alert(1 / 0); // Infinity
alert(-1 / 0); // -Infinity
alert("not a number" / 0) // NaN
```

### BigInt

在 JavaScript 中，“number” 类型无法安全地表示大于 `(253-1)`（即 `9007199254740991`），或小于 `-(253-1)` 的整数。

更准确的说，“number” 类型可以存储更大的整数（最多 `1.7976931348623157 * 10308`），但超出安全整数范围 `±(253-1)` 会出现精度问题，因为并非所有数字都适合固定的 64 位存储。因此，可能存储的是“近似值”。

```javascript
console.log(9007199254740991 + 1); // 9007199254740992 // 能精确存储大于 9007199254740991 的偶数
console.log(9007199254740991 + 2); // 9007199254740992 // 不能精确存储大于 9007199254740991 的奇数
console.log(9007199254740991 + 3); // 9007199254740994
```

在大多数情况下，`±(253-1)` 范围就足够了，但有时候我们需要整个范围非常大的整数，例如用于密码学或微秒精度的时间戳。

`BigInt` 类型是最近被添加到 JavaScript 语言中的，用于表示任意长度的整数。

可以通过将 `n` 附加到整数字段的末尾来创建 `BigInt` 值。

```javascript
// 尾部的 "n" 表示这是一个 BigInt 类型
const bigInt = 1234567890123456789012345678901234567890n;
```

### String

JS 中没有单独对字符规定一个数据类型，只有一种 `String` 类型用于表示字符串和字符。一个字符串可以包含零个、一个或多个字符。有三种可以将数据值表示成字符串类型的方式：

* 双引号："double quotes"
* 单引号：'single quote'
* 反引号（模板字符串，ES6 新增）：\`template string\`

```javascript
let birthPlace = 'Beijing';
birthPlace = 'China';
let description = `I was born in ${birthPlace}`; // I was born in China
// ${} 中的表达式会被计算，计算结果会成为字符串的一部分，可以在其中
// 嵌入一些其它的表达式计算，最好不要过于复杂
let result = `${(1 + 9) * 10}`; // 100
```

### Boolean

Boolean 类型有且仅有两个布尔值，`true` 和 `false`。布尔值常用于条件判断和循环体中作为一种表示条件是否成立的值，这种值通常由一些比较运算（数字、字符串等）计算得来。如果为 true，则表示条件成立；如果为 false，则表示条件不成立。

```javascript
let flag = 2 > 1; // true
if (flag) {
    // flag 为 true 时执行该作用域下的 JS 代码
    alert("2 > 1");
} else {
    // flag 为 false 时执行该作用域下的 JS 代码
    alert("2 <= 1");
}
```

### null

`null` 数据类型有且仅有一个值，那就是字面量 null。

### undefined

特殊值 undefined 也构成了一种类型，那就是 `undefined` 。

使用 `null` 将一个“空”或者“未知”的值写入变量中，而 `undefined` 则保留作为未进行初始化的事物的默认初始值。

### Symbol

`Symbol` 类型用户创建对象的唯一标识符。

### Object

`Object` 类型是 JS 中唯一一个引用数据类型，它的值由更多更复杂的其它数据类型的值所组成。

### typeof 运算符

那既然 JS 有 8 种数据类型，当我们想要知道某个变量的数据类型时，就需要使用 typeof 运算符了。对 typeof 运算符调用的结果会以 String 类型的值返回，用以表示该变量的数据类型。

```javascript
typeof undefined // "undefined"

typeof 0 // "number"

typeof 10n // "bigint"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

typeof Math // "object"，这是浏览器种内置的全局对象（Global Object）

typeof null // "object"

typeof alert // "function"
```

{% hint style="info" %}
`typeof null` 的结果为 `"object"`。

这是官方承认的 typeof 的错误，这个问题来自于 JavaScript 语言的早期阶段，并为了兼容性而保留了下来。 // null 绝对不是一个 object。null 有自己的类型，它是一个特殊值。typeof 的行为在这里是错误的。

`typeof alert` 的结果是 `"function"，`因为 `alert` 在 JavaScript 语言中是一个函数。在 JavaScript 语言中没有一个特别的 “function” 类型。函数隶属于 `object` 类型。但是 `typeof` 会对函数区分对待，并返回 `"function"`。这也是来自于 JavaScript 语言早期的问题。从技术上讲，这种行为是不正确的，但在实际编程中却非常方便。
{% endhint %}
