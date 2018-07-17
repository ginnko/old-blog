---
layout: post
title: javascript查漏补缺之九 ——《带键的集合》
date: 2018-07-16
tag: javascript
---

[Map](http://es6.ruanyifeng.com/#docs/set-map#Map)


1. 创建Map

  1. 使用`set`方法添加

    ```
    const m = new Map();
    const o = {p: 'Hello World'};

    m.set(o, 'content')
    ```

    *set方法返回的是当前的Map对象，因此可以采用链式写法。*

    ```
    let map = new Map()
      .set(1, 'a')
      .set(2, 'b')
      .set(3, 'c');
    ```

  2. 调用构造函数的时候传入一个二维数组

    ```
    const map = new Map([
      ['name', '张三'],
      ['title', 'Author']
    ]);
    ```

2. 判断Map结构中是否包含某个键值，使用`has`方法

  `map.has('name') // true`

3. 获取Map结构某个键对应的值，使用`get`方法

  `map.get('name') // "张三"`

4. 删除某个键值对，使用`delete`方法

  `m.delete(o) // true`

5. 清除所有成员，使用`clear`方法
  ```
  let map = new Map();
  map.set('foo', true);
  map.set('bar', false);

  map.size // 2
  map.clear()
  map.size // 0
  ```
6. 对同一个键多次赋值，后面的值将覆盖前面的值。

7. 读取一个未知的键返回undefined。

8. 只有对同一个对象的引用，Map 结构才将其视为同一个键。**陷阱！大陷阱！！！**墙裂注意下面的代码。原因：**Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞（clash）的问题.**

  ```
  const map = new Map();

  map.set(['a'], 555);
  map.get(['a']) // undefined
  ```
9. 如果 Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键。虽然NaN不严格相等于自身，但 Map 将其视为同一个键。

10. 三个遍历器生成函数

  1. 遍历的顺序就是插入的顺序。

  2. 使用这三个函数返回的是这种形式的结果：`MapIterator {"F", "T"}`。这就是传说中的遍历器？！**感觉可以将这个遍历器视为一个数组？下面第11项感觉可以佐证这个猜想。**

    然后利用这个遍历器的方法如下：

    ```
    for (let key of map.keys()) {
      console.log(key);
    }
    ```
    用`for of`循环来利用这个遍历器。

  3. Map结构的默认遍历器接口就是entries方法。

  ```
  for (let [key, value] of map.entries()) {
      console.log(key, value);
    }
    // "F" "no"
    // "T" "yes"

    // 等同于使用map.entries()
    for (let [key, value] of map) {
      console.log(key, value);
    }
  ```

11. Map结构转数组

  ```
  const map = new Map([
    [1, 'one'],
    [2, 'two'],
    [3, 'three'],
  ]);

  [...map.keys()]
  // [1, 2, 3]

  [...map.values()]
  // ['one', 'two', 'three']

  [...map.entries()]
  // [[1,'one'], [2, 'two'], [3, 'three']]

  [...map]
  // [[1,'one'], [2, 'two'], [3, 'three']]
  ```

12. Map结构的遍历函数`forEach`

  1. 使用方法类似数组的`forEach`

    ```
    map.forEach(function(value, key, map) {
      console.log("Key: %s, Value: %s", key, value);
    });
    ```

  2. forEach方法还可以接受第二个参数，用来绑定this

    ```
    const reporter = {
      report: function(key, value) {
        console.log("Key: %s, Value: %s", key, value);
      }
    };

    map.forEach(function(value, key, map) {
      this.report(key, value);
    }, reporter);
    ```
