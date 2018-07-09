---
layout: post
title: javascript查漏补缺之六-《字符串》
date: 2018-07-09
tag: javascript
---

[译文链接](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide)

1. String对象方法

    1. `String.prototype.charAt()`：从一个字符串中返回指定的字符。

        ```
        var anyString = "Brave new world";

        console.log("The character at index 0   is '" + anyString.charAt(0)   + "'");
        console.log("The character at index 1   is '" + anyString.charAt(1)   + "'");
        console.log("The character at index 2   is '" + anyString.charAt(2)   + "'");
        console.log("The character at index 3   is '" + anyString.charAt(3)   + "'");
        console.log("The character at index 4   is '" + anyString.charAt(4)   + "'");
        console.log("The character at index 999 is '" + anyString.charAt(999) + "'");

        //输出结果：
        The character at index 0 is 'B'
        The character at index 1 is 'r'
        The character at index 2 is 'a'
        The character at index 3 is 'v'
        The character at index 4 is 'e'
        The character at index 999 is ''
        ```
    
    2. `String.prototype.charCodeAt(index)`: 能正确返回一个两个字节组成的字符的码点值。

    3. `String.prototype.pointCodeAt(index)`： 能正确返回一个四个字节组成的字符的码点值。

    4. `String.prototype.indexOf()`: indexOf() 方法返回调用  String 对象中第一次出现的指定值的索引，开始在 fromIndex进行搜索。如果未找到该值，则返回-1。**这个方法区分大小写**。

        ```
        'Blue Whale'.indexOf('lu')
        //1

        //判断某个字符串是否存在于另一个字符串中
        "Blue Whale".indexOf("Blue") !== -1; // true
        "Blue Whale".indexOf("Bloe") !== -1; // false
        ```
    5. `String.prototype.lastIndexOf()`: lastIndexOf() 方法返回指定值在调用该方法的字符串中最后出现的位置，如果没找到则返回 -1。从该字符串的后面向前查找，从 fromIndex 处开始。

    其中， fromIndex从调用该方法字符串的此位置处开始查找。可以是任意整数。默认值为 str.length。如果为负值，则被看作 0。如果 fromIndex > str.length，则 fromIndex 被看作 str.length。