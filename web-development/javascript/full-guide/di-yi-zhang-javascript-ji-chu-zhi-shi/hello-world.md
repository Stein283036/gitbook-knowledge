# Hello World

### 使用 script 元素在网页中加入 JS

{% embed url="https://codepen.io/Stein283036/pen/qByRXPR" %}

其中使用了 `script` 标签在 HTML 文件中引入了 JS 代码，浏览器在遇到这部分代码时，就会执行。通常我们可以把该标签放在页面中的任意位置，不过要注意，如果你需要通过 DOM API 来与页面上的 DOM 元素进行交互时，那么需要出现在 DOM 元素之后，否则 script 标签中的 JS 代码在执行前无法获取到制定的 DOM 元素。

### script 标签的 src 属性

前面提到了可以将 JS 代码直接写在 script 标签体内，不过一旦 JS 代码复杂度增加，那么这种方式就不方便维护和开发了，此外使用这种方式编写的 JS 代码只在当前页面生效，无法达到复用的目的。

因此另一种引入 JS 代码的方式就出现了，通过 script 的属性 src 指明 一个 js 文件的路径，这个路径即可以是相对路径，也可以是一个绝对路径。

{% code lineNumbers="true" %}
```javascript
<script src="./hello.js"></script> // 相对于当前目录路径引入 hello.js 文件 文件
```
{% endcode %}

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
// 通过 CDN（Content Delivery Network）内容交付网络的绝对路径引入 js 文件
```

要引入多个 JS 文件，则使用多个 script 标签。通常来说，将 JS 代码写在独立的 .js 文件中可以获得代码复用、可维护性等好处，只有少量的 JS 代码放在 script 标签中也是合适的。

{% hint style="info" %}
如果设置了 `src` 特性，`script` 标签内容将会被忽略。

一个单独的 `<script>` 标签不能同时有 `src` 特性和内部包裹的代码。
{% endhint %}

```javascript
<script src="file.js">
  alert("I'am ignored"); // 此内容会被忽略，因为设定了 src
</script>
```

