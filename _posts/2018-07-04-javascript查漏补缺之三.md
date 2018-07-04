---
layout: post
title: javascript查缺补漏之三 —— 未完
date: 2018-07-04
tag: javascript
---

1. break

    1. 当在循环中执行break时，会立即终止当前所在的循环。比如下面这几行代码：

        ```
        for (i = 0; i < 3; i++) {
            for ( j = 0; j < 3; j++) {
                if (i === 0) {
                    console.log('最里面:', i);
                    break;
                }
                console.log('里面：', i);
            }
            console.log('外面：', i);
        }
        console.log('最外面');

        //输出顺序：
            最里面: 0
            外面： 0
            里面： 1
            外面： 1
            里面： 2
            外面： 2
            最外面
        ```

        说明break只跳出了内层循环（所在循环），并没有跳出外面包裹的循环。

    2. break label 语法

        自己从来没有使用过这种语法，但通过下面这个列子感觉这个语法还是蛮方便的：

        ```
        var x = 0;
        var z = 0
        labelCancelLoops: while (true) {
        console.log("外部循环: " + x);
        x += 1;
        z = 1;
        while (true) {
            console.log("内部循环: " + z);
            z += 1;
            if (z === 10 && x === 10) {
            break labelCancelLoops;
            } else if (z === 10) {
            break;
            }
        }
        }

        //如果满足 z === 10 && x === 10 的条件，整个循环就会结束，就是使用了break labelCancelLoops 这条语法。
        ```
2. `for in` vs `for of` vs `for`

    1. for...in 语句循环一个指定的变量来循环一个对象**所有可枚举**的属性。

    2. for...of语句在可迭代的对象上创建了一个循环(包括Array, Map, Set, 参数对象（ arguments） 等等)

    3. 数组适合用传统for循环来操作

    ```
    let arr = [3, 5, 7];
    arr.foo = "hello";

    for (let i in arr) {
    console.log(i); // logs "0", "1", "2", "foo"
    }

    for (let i of arr) {
    console.log(i); // logs "3", "5", "7" // 注意这里没有 hello
    }

    for (let i = 0; i < arr.length; i++) {
    console.log(i); //logs "0", "1", "2"// 注意这里没有 foo
    }
    ```

    上面代码中，传统for循环和for of循环的结果相似。
