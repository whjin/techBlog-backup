---
title: JavaScript知多少
date: 2018-11-13 07:57:49
category: ["前端"]
tags: ["javascript"]
---

# `this`与对象原型`prototype` #

# `hoisting`状态提升 #

在程序执行前，编译器先由上到下逐行将代码转为机器可读的命令，然后再执行编译后的指令。

> 实现一个函数，可以返回输入参数是否为质数？

<!--more-->

```javascript
function isPrimeNumber(m) {
    if (m <= 1 || m % 1 !== 0) {
        return false;
    }
    var n = 2;
    while (n < m) {
        if (m % n === 0) {
            return false;
        } else {
            n++;
            continue;
        }
    }
    return true;
}
```

> 实现一个函数，如果传入的参数是字符串，则将该字符串按照字母出现的次数由大到小重新排列并输出；如果传入的参数不是字符串，则将参数输出。

**分析：**

1. 首先，使用`for`循环找出相同的字母，此时需要知道字母出现的次数；
2. 然后，给它们进行排序`sort()`，但是`sort()`是数组方法；
3. 考虑把字符串先转换为数组，处理完毕之后再转换回字符串；
4. 使用`split()`（字符串方法，输出为数组），如果内容为空，则返回的是整个字符串作为数组的第一个元素且数组只包含这一个元素。如果`split`传入内容为`''`，即`split('')`，则字符串里的每个字符分别作为输出数组的元素；
5. 处理完毕需要再转换为字符串，使用`join()`（数组方法，输出位字符串），传入内容`join('')`；
6. 使用正则表达式查找重复字符。

> `classList.toggle(class,true/false)`

<p class="codepen" data-height="365" data-theme-id="0" data-default-tab="html,result" data-user="whjin" data-slug-hash="MRdePN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="js-toggleMenu">
  <span>See the Pen <a href="https://codepen.io/whjin/pen/MRdePN/">
  js-toggleMenu</a> by whjin (<a href="https://codepen.io/whjin">@whjin</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

# 事件处理 #

```html
<span onmouseover="over(this)" onmouseout="out(this)">Test</span>
<div onmouseover="over(this)" onmouseout="out(this)">Line</div>
```

```javascript
function over(element) {
  element.style.color = 'red'
}

function out(element) {
  element.style.color = 'blue'
}
```

