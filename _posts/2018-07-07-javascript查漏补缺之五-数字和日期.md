---
layout: post
title: javascript查漏补缺之五-《数字和日期》
date: 2018-07-07
tag: javascript
---

[译文地址](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Numbers_and_dates)

1. js中数字的范围和类型

  范围： -(2^53 - 1) ~ (2^53 - 1)

  类型： 普通数字， +Infinity， -Infinity， NaN

2. 数字对象属性和方法的引用

  属性包括最大值、最小值、非数、正无穷、负无穷、比较值、最大安全数、最小安全数。

  ![数字对象属性](/images/js/1.png)

  方法调用的时候要使用`Number.`的形式，忘记这个在哪儿看到的了，总之就是有好处就对了。

  ![数字对象的方法](/images/js/2.png)

3. 实现精确四舍五入保留小数位数的方法

    1. `Number.prototype.toFixed()`：这个写在数字对象原型上的方法就可以做到，只不过会返回字符串形式的结果。（负数因为操作符的优先级问题，在不加括号的情况下不会返回字符串形式）

    2. 使用这种方法保留小数后几（3）位：

        ```
        const rounded = Math.round(output * 1000) / 1000;
        ```


