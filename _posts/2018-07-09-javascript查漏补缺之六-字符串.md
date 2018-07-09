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

    6. `String.prototype.startsWith()`: 用来判断当前字符串是否以另外一个给定的子字符串开头，返回true或false。

        ```
        var str = 'To be, or not to be, that is a question.';

        alert(str.startsWith('To be'))//true
        alert(str.startsWith('not to be'))//false
        alert(str.startsWith('not to be', 10))//true
        ```

    7. `String.prototype.endWith()`: endsWith()方法用来判断当前字符串是否是以另外一个给定的子字符串“结尾”的，根据判断结果返回 true 或 false。

        ```
        var str = "To be, or not to be, that is the question.";

        alert( str.endsWith("question.") );  // true
        alert( str.endsWith("to be") );      // false
        alert( str.endsWith("to be", 19) );  // true

        注意最后一个alert，结束位置是19而不是18,19表示的是be后面的那个逗号。
        ```

    8. `String.prototype.includes()`: 判断一个字符串中是否包含另一个字符串，返回true或false。

        ```
        var str = 'To be, or not to be, that is the question.';

        console.log(str.includes('To be'));       // true
        console.log(str.includes('question'));    // true
        console.log(str.includes('nonexistent')); // false
        console.log(str.includes('To be', 1));    // false
        console.log(str.includes('TO BE'));       // false
        ```
    9. `String.prototype.concat()`:字符串拼接函数，由于性能问题，mdn建议使用`+`代替这个函数拼接字符串。自己写代码好像还真没用过这个函数。

    10. `String.fromCharCode()`：这个函数是String类的静态方法，必须这样使用。返回**字符串**。

        ```
        String.fromCharCode(65,66,67)//'ABC'
        ```
    11. `String.fromCodePoint()`: 这个函数同样是String类的静态方法。参数是高位码点。

    12. `String.prototype.split(seperator[,limit])`: 使用指定的分隔符字符串将一个String对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。separator 可以是一个字符串或正则表达式。

        - 例1：使用空格作为Seperator
        ```
        "Webkit Moz O ms Khtml".split( " " )   // ["Webkit", "Moz", "O", "ms", "Khtml"]
        ```

        - 例2：使用正则表达式作为Seperator,正则表达式不需要加`g`标识符。

        ```
        var myString = "Hello 1 word. Sentence number 2.";
        var splits = myString.split(/(\d)/);

        console.log(splits);

        //[ "Hello ", "1", " word. Sentence number ", "2", "." ]
        ```

        - 例3：设置第二个参数

        ```
        var myString = "Hello World. How are you doing?";
        var splits = myString.split(" ", 3);

        console.log(splits);

        //["Hello", "World.", "How"]

        ```
    13. `String.prototype.slice(begin[, end])`:返回一个子字符串，提取范围是[begin, end),其中end为可选参数，如果begin或end为负值，则实际为length+begin/length+end。

    14. `String.prototype.substring(begin[, end]`: 返回一个子字符串。类似上面的slice方法。当begin>end时，会交换begin和end的位置执行。

    15. `String.prototype.substr(start[, length])`：返回一个字符串中从指定位置开始到指定字符数的字符。

    ---

    **下面是字符串的正则表达式用法**

    ---

    16. 