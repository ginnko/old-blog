---
layout: post
title: javascript查漏补缺之十九 ——《闭包》
date: 2018-08-14
tag: javascript
---

[链接地址](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

1. 关于`lexical`的解释

> The word "lexical" refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. Nested functions have access to variables declared in their outer scope.

2. 关于闭包

> A closure is the combination of a function andn the lexical environment within which that function was declared.

**闭包具有封装和隐藏数据的优点。**

比如下面这个例子

```js
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

`add5`和`add10`都是闭包，它们共享相同的函数体定义，但是存储了不同的词法环境。在`add5`的词法环境中，`x`是5；在`add10`的词法环境中，`x`是10。

再比如下面这个例子：

```js
var counter = (function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  };   
})();

console.log(counter.value()); // logs 0
counter.increment();
counter.increment();
console.log(counter.value()); // logs 2
counter.decrement();
console.log(counter.value()); // logs 1
```

在前面的例子中，每一个闭包都有它自己的词法环境。然而，这里我们创建了一个单一的词法环境，这个环境被三个函数共享。这个共享的词法环境是在一个匿名函数的函数体中创建的，这个匿名函数创建完就执行了。这个词法环境包含两个私有条目：一个叫做`privateCounter`的变量以及一个叫做`changeBy`的函数。这两个私有条目都不可以从匿名函数外访问到。相反，它们只能被匿名函数返回的三个公共函数访问。