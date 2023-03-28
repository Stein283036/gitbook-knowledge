---
description: 本章的 JS 代码运行在浏览器环境中，在 Node.js 环境中没有这些 BOM API。
---

# 交互：alert、prompt 和 confirm

在浏览器环境中，对于动态网页来说，通常要与用户进行一些交互行为，比如用户触发了类似删除的危险操作，又或是提示用户输入用户名、密码等信息。因此 浏览器内置的 BOM API，提供了与用户进行交互的函数。

### alert

alert 会在当前窗口下弹出一个警告信息弹框，用户需要点击确认后才能进行其它的交互操作。

```javascript
alert("alert info");
```

弹出的这个带有信息的小窗口被称为 **模态窗**。“modal” 意味着用户不能与页面的其他部分（例如点击其他按钮等）进行交互，直到他们处理完窗口。在上面示例这种情况下 —— 直到用户点击“确定”按钮。

### prompt

`prompt` 函数接收两个参数，第一个参数 title 表示提示框的标题，第二个可选参数表示提示框的初始值。

```javascript
result = prompt(title, [default]);
// 上述语法中 default 周围的方括号表示该参数是可选的，不是必需的。
```

浏览器会显示一个带有文本消息的模态窗口，还有 input 框和确定/取消按钮。

`prompt` 将返回用户在 `input` 框内输入的文本，如果用户取消了输入，则返回 `null`。

```javascript
let age = prompt('How old are you?', 23);

alert(`You are ${age} years old!`);
```

### confirm

`confirm` 函数显示一个带有 `question` 以及确定和取消两个按钮的模态窗口。

语法：

```javascript
result = confirm(question);
```

当用户点击确认后，返回 true；点击取消后返回 false。

{% hint style="info" %}
上述所有方法共有两个限制：

1. 模态窗口的确切位置由浏览器决定。通常在页面中心。
2. 窗口的确切外观也取决于浏览器。我们不能修改它。
{% endhint %}
