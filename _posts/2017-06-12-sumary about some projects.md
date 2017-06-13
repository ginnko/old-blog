---
layout: post
title: Tic Tac Toe 游戏项目总结
date: 2017-06-12
tag: jQuery on off push 变量作用域
---

####1. 变量作用域  
在计算器、番茄闹钟和这个项目中，都遇到了在for循环中用var定义一个循环变量后，即便出了for循环的范围依然可以使用的情况，现在返回头，从廖大角虫的[教程](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014344993159773a464f34e1724700a6d5dd9e235ceb7c000)里在明确一下变量作用域。

- 今后在第一行都写上'use strict'，强制要求通过var申明变量。
- 若两个不同的函数各自中声明了相同名字的变量，该变量只在各自的函数体内起作用。
- JavaScript的变量作用域是函数内部，**在for循环等语句块中无法定义具有局部作用域的变量**。比如： 

		function foo() {
			for(var i=0; i<100; i++){
			//
			}
			i += 100; //在for循环外仍然可以使用i！！！
		}

		在语句块中使用let声明局部变量：
		function foo() {
			for(**let** i=0; i<100; i++){
			//
			}
			i += 100; //在for循环外仍然可以使用i！！！
		}

- 名字空间：

		//唯一的全局变量
		var MYAPP = {};
		//其他变量
		MYAPP.name = 'myapp';
		MYAPP.version = 1.0;
		//其它函数
		MYAPP.foo = function(){
			return "foo";
		};

####2. 布尔值
false不能用具体某个数字表示：-1 ！== false

####3. 	遇到的具体问题
- Tag div 没有disable这个属性
- 当使用jQuery时，开关click事件可以使用on， off函数，需要一个callback函数。当依次执行关闭、自动开启、手动开启操作时，为避免多次开启，采用下面的方法。[实例](https://codepen.io/ginnko/pen/dRPXGv)：place函数、another函数以及reset函数。

		$(".pit").off("click");//prevent from being disturbed by the same execution in another function
 		$(".pit").on("click", place);

- 数组的push（）函数，如果参数是一个数组，那么结果将是一个二维数组，如果改动这个二维数组中的元素，则原来那个作为参数传入的数组中的相应元素也会被改动，push（）函数执行的是浅复制操作。









