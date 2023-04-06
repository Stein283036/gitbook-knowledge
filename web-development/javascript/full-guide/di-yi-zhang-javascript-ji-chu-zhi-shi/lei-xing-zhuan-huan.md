# 类型转换

大多数情况下，运算符和函数会将数据值转换成合适的数据类型，比如 1 + 1 会被转换成 Number 类型，alert 函数会自动将所有的值转换成字符串。这些转换称之为隐式或自动转换。然而，在某些情况下，我们需要将值显式地转换为我们期望的类型。比如将一个 Number 类型的时间戳转换成一个用来表示某一个日期时间格式的对象类型。

### 字符串转换

字符串类型的值与任何其它数据类型的值进行 + 运算时，结果都会返回一个 String 类型的值。此外可以通过 String(value) 来将任何一个类型值转换成字符串值的表示。

```javascript
let str1 = "str" + 1; // "str1"
let str2 = "str" + true; // "strtrue"
let str3 = String(123456) // "123456"
let str4 = 1 + Math; // "1[object Math]"
```

### 数字类型转换

在算术函数和表达式中，会自动进行 `Number`类型转换。

当对非数字类型使用算数运算符进行计算时，会先尝试将这些变量进行数据类型的转变，比如字符串 "123" 会被转换成 `Number` 类型的 123，而如果一个字符串不是合法的数字，那么它将被转换成 `NaN`，例外是 **'Infinity' 和 '-Infinity' 以及 'NaN' 会被转换成它们对应的特殊的数字值**。

对应字符串而言，还可以通过在字符串的开头拼接 + 运算符，来将该字符串转换为 Number 类型。

```javascript
alert("6" / "2"); // 3
// String 类型的 "6" 和 "2" 会先被转换成 Number 的 6 和 2，在进行计算
alert(+"123" / 2); // 61.5
```

也可以使用 `Number(value)` 显式地将这个 `value` 转换为 number 类型。

```javascript
Number('123'); // 123
Number(''); // 0
Number('abc'); // NaN
Number('    123        '); // 123，会先将字符串的空白字符去除，在尝试转换
Number('              '); // 0
Number('Infinity'); // Infinity
Number('-Infinity'); // -Infinity
Number('012345') // 12345
Number(0xF) // 15
Number(010) // 8
```

`Boolean` 类型的 `true` 会被转换为 1，`false` 会被转换成 0。

```javascript
Number(true); // 1
Number(false); // 0
```

number 类型转换规则：

|        值       |                                                    结果                                                   |
| :------------: | :-----------------------------------------------------------------------------------------------------: |
|   `undefined`  |                                                  `NaN`                                                  |
|     `null`     |                                                   `0`                                                   |
| `true 和 false` |                                               `1` and `0`                                               |
|    `string`    | 去掉首尾空白字符（空格、换行符 、制表符  等）后的纯数字字符串中含有的数字。如果剩余字符串为空，则转换结果为 `0`。否则，将会从剩余字符串中“读取”数字。当类型转换出现 error 时返回 `NaN`。 |

### 布尔类型转换

在逻辑运算的表达式中，会将计算结果的值转换成 true 或者是 fasle，这种逻辑运算通常是比较运算符如 `>`、`<`、`==`、`!=` 等，且通常与逻辑运算符结合使用，如 `&&`、`||`、`!` 。

除了上述的逻辑运算以外，还可以通过调用全局对象 Boolean 来将其它的值转换成 Boolean 类型的值，转换规则如下：

* 空值全被转换成 `false`，这些空值有 `0`、空字符串、`null`、`undefined`、`NaN`。
* 其它值被转换成 `true`

```javascript
alert(Boolean(1)); // true
alert(Boolean(0)); // false
alert(Boolean("0")); // true
alert(Boolean("")); // false
alert(Boolean("   ")); // true
alert(Boolean(null)); // false
alert(Boolean(undefined)); // false
alert(Boolean(NaN)); // false
```

{% hint style="info" %}
对 undefined 进行数字型转换时，输出结果为 NaN，而非 0。

对 `"0"` 和只有空格的字符串（比如：`" "`）进行布尔型转换时，输出结果为 `true。`
{% endhint %}
