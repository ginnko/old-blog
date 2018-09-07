---
layout: post
title: css查漏补缺之十-floats
date: 2018-09-07
tag: css
---

[链接](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Floats)

### 浮动的结果

`float`本来是用来在一块文本中浮动图片的,多行布局交给了`flex`和`grid`，链接中的文章就是从这个角度来介绍float的。

浮动元素会脱离正常流。

浮动只会在元素所在的原始行开始浮动，并不会像`position: absolute`“浮的”那么彻底。

>the element with the float set on it is taken out of the normal layout flow of the document and stuck to the left and side of its parent container. Any content that comes below the floated element in the normal layout flow will now wrap around it, filling up the space to the right-hand side of it as far up as the top of the floated element. There it will stop.

只能通过给`浮动元素`的一侧添加外边距来调整浮动元素和环绕它的文本的间距。

### 清除浮动

使用`clear`属性，可以取得值有：

- left

- right

- both

### 