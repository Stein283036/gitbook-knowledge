# 变量提升和函数提升

### 变量提升

```javascript
console.log(far) // undefined
var far = 'far'
```

上面的例子中，使用 `var` 定义的变量存在显示的变量提升，即将变量的定义提升到了当前作用域（在我这里是全局作用域）的顶层，前面两行的代码等价于：

```javascript
var far;
console.log(far);
far = 'far';
```

因此结果输出 undefined。

#### 暂时性死区

```javascript
console.log(bar);
let bar = 'bar'; // ReferenceError: Cannot access 'bar' before initialization
```

与使用 `var` 声明一个变量相比，`let` 声明的变量不会显示的存在变量提升，因为它是对客户端即编程人员而言的，在 JS 引擎内部，依然可以看到当前作用域已经声明了 bar 变量，不过不允许对它进行访问，如果访问了，那么 JS 殷勤会抛出 `ReferenceError: Cannot access 'bar' before initialization`，而不是 `ReferenceError: bar is not defined`，例如直接输出 `far` 变量而没有直接声明它：

```javascript
console.log(far); // ReferenceError: bar is not defined
```

由此可见，`let` 声明的变量存在暂时性死区，即没有明显的变量提升，但 JS 引擎确实识别了当前作用域使用 `let` 声明的变量。

### 函数提升

对于函数提升来说，JS 引擎会在当前的作用域中识别所有的函数定义（而不是函数表达式）并将它们提升到该作用域的开始处。

{% embed url="https://gist.github.com/maxogden/4bed247d9852de93c94c" %}
