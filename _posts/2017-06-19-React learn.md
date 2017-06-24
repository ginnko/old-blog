---
layout: post
title: React学习
date: 2017-06-19
tag: React
---
这篇是React入门的学习总结，主要参考阮一峰大神的教程（如下）和官方文档，用codepen完成了教程里的[demo](https://codepen.io/ginnko/pen/EXWaaw)。
## 基础学习

### 1. 资料
- [阮大角虫的教程](http://www.ruanyifeng.com/blog/2015/03/react.html)
- [官网](https://facebook.github.io/react/docs/installation.html)
- [Dan Abramov大神的实例](https://codepen.io/gaearon/#)

### 2. 问题
- 不太清楚React具体能做什么
> 在下面的想法中，有模糊的描述，感觉还需要做更多的练习才能体会。

- 教程里有个使用Promise的例子，虽然明白Promise最主要的有点就是将执行过程和结果分开，但是并没有觉得这有什么特别好处，只是看起来更清晰了？关于Promise的部分参考了[廖大角虫的教程](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345008539155e93fc16046d4bb7854943814c4f9dc2000)。
- 当使用setInterval()和Ajax的同时使用了bind（）函数，不太理解这个地方。
> bind(this)是将当前作用域传入相应的函数，在ES6中被要求要明确的表示，因为不再自动匹配，在下面的[“是否使用ES6的方法对比”](https://facebook.github.io/react/docs/react-component.html)中有说明。


### 3. 注意
- 组件类的变量名的首字母要**大写**！！！
- rent中的顶级标签只能有一个，所以示例中的全部用<div>标签包裹

## 应用
### 1. Leaderboard
这个[demo](https://codepen.io/ginnko/full/bRqXaN/)是[FreeCodeCamp](https://www.freecodecamp.com/challenges/build-a-camper-leaderboard)的一个练习，使用React实现（2017.6.23完成）。
#### 一个方法：componentDidUpdate()
第一版使用如下代码，但现在看来是自己对componentDidUpdate()这个方法理解有问题，虽然能够实现下述的功能，但这个方法的真正使用方法应该不是这样。
>这个方法用来实现当属性或状态发生变化时，对页面中的相应内容进行变更。[demo](https://codepen.io/ginnko/full/bRqXaN/)中点击30天内的分数排名和总分数排名的切换就是通过这个方法实现的。实现的代码如下：  


	
	componentDidUpdate(){
	  this.props.promise.then(
	    value => this.setState({loading: false, data: value}),
	    error => this.setState({loading: false, error: error})
	  );
	},
	handleClick: function(event){
	  if(flag === 0){
	    flag = 1;
	    this.props.promise = $.getJSON(alltime);
	  }else{
	    flag = 0;
	    this.props.promise = $.getJSON(recent);
	  }
	}

>handleClick属性传给标题中的30天内排名和总分数排名两个标题，当点击时，会相应的改变ajax请求的api并把返回结果传递给promise属性，发生的改变会被componentDidUpdate()方法捕捉，然后使用新的数据重新渲染模板。

#### 一个属性handleClick
这个[demo](https://codepen.io/ginnko/full/bRqXaN/)最终是通过handleClick属性完成切换是根据30天分数排名还是根据总分数排名，还可以选择是正序显示还是倒序显示，不再使用componentDidUpdate()方法。具体代码如下。

	handleClick: function(event){
	  var id = event.target.parentElement.getAttribute('id');
	  if(id === "alltime"){
	    this.props.promise = $.getJSON(alltime);
	    if(flag2 === 1){
	      flag1 = 1;
	      flag2 = 0;
	      this.props.promise.then(
	        value => this.setState({loading: false, data: value, mark2 :"↓", mark1 :""}),
	        error => this.setState({loading: false, error: error})
	      );
	    }else{
	      flag1 = 1;
	      flag2 = 1;
	      this.props.promise.then(
	        value => this.setState({loading: false, data: value.reverse(), mark2 :"↑", mark1 :""}),
	        error => this.setState({loading: false, error: error})
	      );
	    }
	  }
	  if(id === "recent"){
	    this.props.promise = $.getJSON(recent);
	    if(flag1 === 1){
	      flag2 = 1;
	      flag1 = 0;
	      this.props.promise.then(
	        value => this.setState({loading: false, data: value, mark1 :"↓", mark2 :""}),
	        error => this.setState({loading: false, error: error})
	      );
	    }else{
	      flag2 = 1;
	      flag1 = 1;
	      this.props.promise.then(
	        value => this.setState({loading: false, data: value.reverse(), mark1 :"↑", mark2 :""}),
	        error => this.setState({loading: false, error: error})
	      );
	    }
	  }
	}

有两处引用了handleClick，使用**event.target.parentElement.getAttribute('id')**来判断是哪个发生了点击，并据此显示是根据哪类分数显示。  
这条代码的使用参考[此处](https://stackoverflow.com/questions/39559222/react-onclick-event-on-link)。event.target可以获得发生点击事件的DOM node本身。然后使用操纵DOM node的方法[parentElement](https://developer.mozilla.org/en/docs/Web/API/Node/parentElement)以及[getAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute)进行判断。event.target真是方便啊！
#### 一些想法
1. 第一次加载时，由于需要渲染，页面是完全白色的，渲染完成后加载相应的内容。但是在初始加载完成后，后面更新数据重新渲染不会再重新加载页面而只是渲染页面变更的部分，之前一直不太明白React的用途，只是听过适合开发UI，或许上面的描述就是一个证据。
2. 本例中，使用componentDidMount方法来处理ajax请求，根据现在掌握的资料，推断这个方法只能使用一次，也就是在组件加载完成后，之后属性或状态再发生变化要通过componentDidUpdate()方法（有待研究）或handleEvent系列属性来实现。另一个handleEvent属性的实例：[阮大角虫的教程](http://www.ruanyifeng.com/blog/2015/03/react.html)中第9个demo是一个实时显示的应用，使用的是handleChange属性，属性函数里用event.target.value来获取实时改变的值并显示。

#### 一些问题  
1. 最初的代码是，关于图标和表格标题的部分都写在html文档中，页面一加载就能看到这两项内容，表格的数据部分用json获取后通过React返回。当React使用render返回一个被DOM元素包裹的数组时，React会自动将其展开一条一条列出。但是，render函数中要求只能有一个顶级标签，导致返回的表格数组和已经写好的表格标题不一样大小，只占其第一列的宽度。没有查到解决办法，参考别人的项目，也没有这样写的，最后只能让所有的部分都由React来实现。希望能找到解决上述问题的方法。 
2. colspan 属性名在JSX中要写成colSpan才会被识别。
3. ES6发布后，React的一些方法有了改变，阮一峰大神的教程使用的是ES6发布前的方法。这个demo也没有使用ES6，但是在之后的练习中都要使用最新的方法。下面两个链接是React官方文档和是否使用ES6的一些方法的改变对比：  

 - [常用方法](https://facebook.github.io/react/docs/react-component.html)
 - [是否使用ES6的方法对比](https://facebook.github.io/react/docs/react-without-es6.html)  
 



未完。。。




