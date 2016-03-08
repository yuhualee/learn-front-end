* **对象写法：**

	把模块写成一个对象，而且模块成员都放到这个对象里面。
	
	```
	var modal = new Object({
		_count: 0,
		m1: function(){
			alert('modal m1');
		},
		m2: function(){
			alert('modal m2');
		}
	});
	modal.m1();    //modal m1  调用modal对象里面的属性	
	```
	
	但是，内部状态可以在外部改写
	
	```
	modal._count = 5;
	alert(modal._count);   //5
	```
	
* **立即执行函数写法**

	```
	var modal = (function(){
		var _count = 0;
		var m1 = function(){
			alert('modal m1');
		};
		var m2 = function(){
			alert('modal m2');
		};
		return{
			m1: m1,
			m2: m2
		}
	})();
	alert(modal._count);   //undefined   外部无法读取内部变量
	modal.m1();
	```
	
* **放大模式**

	如果一个模块很大，必须分成几个部分，或者一个模块需要继承另一个模块
	
	```
	
	```

### AMD

#### AMD原理

AMD：异步模块定义。它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成后，这个回调函数才会运行。

```
	require([modal],callback);	
```

第一个参数[module]，是一个数组，里面的成员就是要加载的模块；第二个参数callback，则是加载成功之后的回调函数。

```
	require(['math'],function(math){
		math.add(2,3);
	});
```
#### AMD模块的写法

reuqire.js加载的模块，采用AMD规范，也就是说模块必须按照AMD的规定来写。

模块必须采用特定的define()函数来定义。如果不依赖其它模块，写法如下：

```
define(function(){
	var add = function(x,y){
		return x + y;
	};
	return {
		add: add
	}
});
```
加载方法：

```
require(['math'],function(math){
	alert(math.add(1,1));
});
```

### require.js
	