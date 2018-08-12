---
layout: post
title: javascript查漏补缺之十八 ——《相等判断》
date: 2018-08-06
tag: javascript
---

[链接地址](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

### loose equality

![==转换](/images/js/7.png)

1. `Number`，`String`，`Boolean`类型在和`Number`，`String`，`Boolean`类型比较的时候，如果两个不是相同类型，会将两个比较的值都转成数字后再进行比较。转换时，相当于使用`+`。

2. `Number`，`String`，`Boolean`类型在和`Object`类型比较的时候，会把`Object`类型转换成基础类型。转换过程会调用`A.toString`和`A.valueOf`这两个方法，不同类型进行转换时，这两个方法调用的顺序不同。

[koko](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#Same-value_equality)