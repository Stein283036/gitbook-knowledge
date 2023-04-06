# 变量

### 什么是变量

互联网的背后实则是无穷无尽的信息和数据，比如各种各样的文本资源、图片资源、视频、音乐、你的微信聊条记录、你的游戏进度等等这些都是需要通过存储介质（硬盘、U盘、光驱等）保存在电脑上的，那么当我们编写的应用程序（进程）需要这些数据时就需要将它们从外部的静态存储介质通过操作系统执行 IO 通信的操作来将这些数据加载到内存中，这时候就需要变量来存储它们了，否则内存中的这些数据无法访问到，自然也就没有存在的价值了，这个变量也就是内存中数据的地址。

### 定义变量的三种方式

**var**

在 ES5 及以前，JS 中只有一种定义变量的方式，即使用关键字 `var` 。通过 var 定义的变量会存在显示地变量提升，即会提升到当前作用域的最顶层，值为 `undefined` 。并且 var 定义的变量不存在块作用域，因此很容易造成变量污染，具体关于 var、let、const 的区别在后面的文章中详细讲解。

**let**

```javascript
let username; // 声明了一个 username 变量，但是没有赋值，因此值默认为 undefined
console.log(username); // undefined
username = "stein" // 将字符串 "stein" 赋值给 username 变量
```

```javascript
let username = "stein"; // 使用一行来完成变量的声明和赋值
```

因为 JS 是一门动态语言，变量的数据类型没有严格的限制，因此在对一个变量赋值之后，可以将另一个不同类型的值赋给它。

```javascript
let far = "far"; // "far" 是 String 类型
far = 1024; // 1024 是 Number 类型
```

{% hint style="info" %}
在同一个作用域下，let 声明的变量名称不能重复，这是 let 与 var 的区别之一，否则会导致语法错误。
{% endhint %}

```javascript
let same = "same variable";
let same = "same variable";
// SyntaxError: Identifier 'same' has already been declared
```

**const**

用 `const` 声明的变量表示常量，简单来说，`const` 和 let 很像，不过唯一的区别就是 const 声明的变量必须在声明时赋值，且一旦赋值后值不能发生改变。

const 声明的常量名称通常都是以大写字母和下划线命名，这是一个好的编码规范。不过对于一些需要计算得到的值应该使用 camelCase 的命名风格。

```javascript
const PI; // 没有对 PI 常量进行赋值会导致 SyntaxError 错误
SyntaxError: Missing initializer in const declaration
```

```javascript
const PI = 3.14;
PI = 3.1415926; // 修改常量 PI 的值会导致 TypeError 错误
TypeError: Assignment to constant variable
```

### 变量命名规范

JS 的变量命名规范有一些限制：

* 变量名称只能由 字符（包括除了英文以外的其它字符）、数字、`_` 和 `$` 组成
* 变量名不能以 `_` 开头
* 无法使用 JS 的 [保留字列表](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical\_grammar#Keywords) 作为变量名称

如果命名包括多个单词，通常采用驼峰式命名法（[camelCase](https://en.wikipedia.org/wiki/CamelCase)）。也就是，单词一个接一个，除了第一个单词，其他的每个单词都以大写字母开头：`myVeryLongName`。

{% hint style="info" %}
JS 如同很多编程语言一样，是区分大小写的，因此变量名称 UPPER 和 upper 是两个不同的变量。

JS 虽然允许使用除了英文字母（a-z、A-Z）之外的其它字符作为变量名称的一部分，不过不推荐使用，事实上，很少有开发人员这样使用。
{% endhint %}

