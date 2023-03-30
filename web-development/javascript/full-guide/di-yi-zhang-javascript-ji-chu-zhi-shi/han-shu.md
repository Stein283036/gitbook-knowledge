# 函数

函数是程序的主要“构建模块”。函数使该段代码可以被调用很多次，而不需要写重复的代码。

### 函数声明

```javascript
function far([可选参数]) {
    // 函数体
}
```

函数可以通过名称调用：`far()`。

### 局部变量

函数中声明的变量的作用域仅在该函数内部有效（可见）。即使它是使用 `var` 声明的。因为 `var` 只有函数作用域，而 `let` 和 `const` 有既有函数作用域也有范围更小的块作用域。

```javascript
function showMessage() {
  var message = "Hello, I'm JavaScript!"; // 局部变量

  alert( message );
}

showMessage(); // Hello, I'm JavaScript!

alert( message ); // <-- 错误！变量是函数的局部变量
```

### 外部变量

虽然无法在一个函数外部访问一个函数内定义的变量，不过可以在函数内部访问函数之外的变量，前提是这些变量是全局变量，因为它们在函数作用域内是可见的。

```javascript
let userName = 'John';

function showMessage() {
  userName = "Bob"; // (1) 改变外部变量

  let message = 'Hello, ' + userName;
  alert(message);
}

alert( userName ); // John 在函数调用之前

showMessage();

alert( userName ); // Bob，值被函数修改了
```

只有在没有局部变量的情况下才会使用外部变量。

如果在函数内部声明了同名变量，那么函数会**覆盖**外部变量。

```javascript
let userName = 'John';

function showMessage() {
  let userName = "Bob"; // 声明一个局部变量

  let message = 'Hello, ' + userName; // Bob
  alert(message);
}

// 函数会创建并使用它自己的 userName
showMessage();

alert( userName ); // John，未被更改，函数没有访问外部变量。
```

{% hint style="info" %}
全局变量

任何函数之外声明的变量，例如上述代码中的外部变量 `userName`，都被称为 **全局** 变量。

全局变量在任意函数中都是可见的（除非被局部变量遮蔽）。

减少全局变量的使用是一种很好的做法。现代的代码有很少甚至没有全局变量。大多数变量存在于它们的函数中。但是有时候，全局变量能够用于存储项目级别的数据。比如一些公共的常量通常作为全局变量来表示，如圆周率 `π`，用户的个人信息等。
{% endhint %}

### 参数

当一个值被作为函数参数（parameter）传递时，它也被称为 **参数（argument）**。

换一种方式，我们把这些术语搞清楚：

* 参数（parameter）是函数声明中括号内列出的变量（它是函数声明时的术语），也叫形参。
* 参数（argument）是调用函数时传递给函数的值（它是函数调用时的术语），也叫实参。

### 参数的默认值

如果一个函数被调用，但有参数（argument）未被提供，那么相应的值就会变成 `undefined`。

可以使用 `=` 为函数声明中的参数指定所谓的“默认”（如果对应参数的值未被传递则使用）值：

```javascript
function greet(from, text="no text") {
    alert(`from ${from}, ${text}`);
}
```

### 返回值

```javascript
function sum(a, b) {
  return a + b;
}

let result = sum(1, 2);
alert( result ); // 3
```

指令 `return` 可以在函数的任意位置。当执行到达时，函数停止，并将值返回给接收者，在上面是 `result` 变量。

只使用 `return` 但没有返回值也是可行的。但这会导致函数立即退出。

{% hint style="info" %}
空值的 `return` 或没有 `return` 的函数返回值为 `undefined`

如果函数无返回值，它就会像返回 `undefined` 一样：

```javascript
function doNothing() { /* 没有代码 */ }

alert( doNothing() === undefined ); // true
```

空值的 `return` 和 `return undefined` 等效：

```javascript
function doNothing() {
  return;
}

alert( doNothing() === undefined ); // true
```
{% endhint %}

### 函数命名

函数就是行为（action）。所以它们的名字通常是**动词**。它应该**简短**且尽可能准确地描述函数的作用。这样读代码的人就能清楚地知道这个函数的功能。

一种普遍的做法是用**动词前缀**来开始一个函数，这个前缀模糊地描述了这个行为。团队内部必须就前缀的含义**达成一致**。

例如，以 `"show"` 开头的函数通常会显示某些内容。

函数以 XX 开始……

* `"get…"` —— 返回一个值，
* `"calc…"` —— 计算某些内容，
* `"create…"` —— 创建某些内容，
* `"check…"` —— 检查某些内容并返回 boolean 值，等。

这类名字的示例：

```javascript
showMessage(..)     // 显示信息
getAge(..)          // 返回 age（gets it somehow）
calcSum(..)         // 计算求和并返回结果
createForm(..)      // 创建表单（通常会返回它）
checkPermission(..) // 检查权限并返回 true/false
```

{% hint style="info" %}
非常短的函数命名

常用的函数有时会有**非常短**的名字。

例如，[jQuery](http://jquery.com/) 框架用 `$` 定义一个函数。[LoDash](http://lodash.com/) 库的核心函数用 `_` 命名。

这些都是例外，一般而言，函数名应简明扼要且具有描述性。
{% endhint %}

### 函数 == 注释

函数应该简短且只有一个功能。如果这个函数功能复杂，那么把该函数拆分成几个小的函数是值得的。有时候遵循这个规则并不是那么容易，但这绝对是件好事。

一个单独的函数不仅更容易测试和调试 —— 它的存在本身就是一个很好的注释！

例如，比较如下两个函数 `showPrimes(n)`。它们的功能都是输出到 `n` 的 [素数](https://en.wikipedia.org/wiki/Prime\_number)。

第一个变体使用了一个标签：

```javascript
function showPrimes(n) {
  nextPrime: for (let i = 2; i < n; i++) {

    for (let j = 2; j < i; j++) {
      if (i % j == 0) continue nextPrime;
    }

    alert( i ); // 一个素数
  }
}
```

第二个变体使用附加函数 `isPrime(n)` 来检验素数：

```javascript
function showPrimes(n) {

  for (let i = 2; i < n; i++) {
    if (!isPrime(i)) continue;

    alert(i);  // 一个素数
  }
}

function isPrime(n) {
  for (let i = 2; i < n; i++) {
    if ( n % i == 0) return false;
  }
  return true;
}
```

第二个变体更容易理解，不是吗？我们通过函数名（`isPrime`）就可以看出函数的行为，而不需要通过代码。人们通常把这样的代码称为 **自描述**。

因此，即使我们不打算重用它们，也可以创建函数。函数可以让代码结构更清晰，可读性更强。
