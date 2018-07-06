---
layout: post
title: javascript查漏补缺之四-《表达式和运算符》
date: 2018-07-06
tag: javascript
---

1. 假值

    `false, null, 0, NaN, "", undefined`
  
2. 逗号操作符

    对两个操作数进行求值并**返回最终操作数的值**。它常常用在 for 循环中，在每次循环时对多个变量进行更新。

    ```
    var x = [0,1,2,3,4,5,6,7,8,9]
    var a = [x, x, x, x, x];

    for (var i = 0, j = 9; i <= j; i++, j--)
      console.log('a[' + i + '][' + j + ']= ' + a[i][j]);
    ```

3. delete操作符

    delete不能删除使用var，let，const声明的变量。

    delete删除数组元素值，这个元素还存在，但是值变成了undefined,
    执行`index in array`返回`false`。

    ```
    let obt1 = {
      test: 'test1',
      test2: 'test2'  
    };

    let arr1 = [
        1, 2, 3
    ];

    let obj1 = {
      test: 'test'  
    };

    console.log(delete obj1);//false
    console.log(obj1);//{test: "test"}

    console.log(delete obt1.test);//true
    console.log(obt1);//{test2: "test2"}

    console.log(delete arr1[1]);//true
    console.log(arr1);//[1, , 3]
    conosle.log(arr1[1]);//undefined
    ```

4. 表达式和语句

    表达式： 用来计算出一个值

    语句： 用来使某个事情发生

5. typeof操作符

    返回值为字符串形式。

    ```
    typeof myFun;     // returns "function"
    typeof shape;     // returns "string"
    typeof size;      // returns "number"
    typeof today;     // returns "object"
    typeof dontExist; // returns "undefined"
    typeof true; // returns "boolean"
    typeof null; // returns "object" 这个要注意下
    ```

6. in操作符

    **检查它（或其原型链）是否包含具有指定名称的属性的对象。**

    `prop in object`

    *prop*: 一个字符串类型或者 symbol 类型的属性名或者数组索引

    *object*: 对象或者数组

7. instance操作符

    **instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。**

    `object instanceof constructor`

8. 基本表达式

    1. this

        下面这两种用法之前没有留意过诶。

        1. 作为一个DOM事件处理函数

            当函数被用作事件处理函数时，它的this指向触发事件的元素。

            ```
            // 被调用时，将关联的元素变成蓝色
            function bluify(e){
            console.log(this === e.currentTarget); // 总是 true

            // 当 currentTarget 和 target 是同一个对象时为 true
            console.log(this === e.target);        
            this.style.backgroundColor = '#A5D9F3';
            }

            // 获取文档中的所有元素的列表
            var elements = document.getElementsByTagName('*');

            // 将bluify作为元素的点击监听函数，当元素被点击时，就会变成蓝色
            for(var i=0 ; i<elements.length ; i++){
            elements[i].addEventListener('click', bluify, false);
            }
            ```

        2. 作为一个内联事件处理函数

            当代码被内联on-event 处理函数调用时，它的this指向监听器所在的DOM元素。

            ```
                <button onclick="alert(this.tagName.toLowerCase());">
                Show this
                </button>

                //alert 会显示button
            ```

            还有下面这种用法...感觉之前完全没有想过。

            ```
            function validate(obj, lowval, hival){
            if ((obj.value < lowval) || (obj.value > hival))
                console.log("Invalid Value!");
            }

            <p>Enter a number between 18 and 99:</p>
            <input type="text" name="age" size=3 onChange="validate(this, 18, 99);">
            ```
9. 扩展语句

    1. 函数调用

        `myFunction(...iterableObj);`

    
    2. 字面量数组构造或字符串

        `[...iterableObj, '4', ...'hello', 6];`

    3. 构造字面量对象时,进行克隆或者属性拷贝

        `let objClone = { ...obj };`

未完，看到[这里](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)。