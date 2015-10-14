### this

* **global context 全局上下文**

	在全局上下文中（在任何函数体外部），this指代全局对象（window），无论是否在严格模式下。
	
	```
	console.log(this === window)
	//输出： true
	```
	
* **Function context函数上下文**

	在函数内部，this的值取决于函数是谁调用的。
	
	```
	function fn(){
	  console.log(this);
	}
	fn();  //window
	```
	> 在这个例子中，this的值不是由函数调用设定。因为代码不运行在严格模式下，this的值始终是一个对象且默认为全局对象。
	
	```
	function fn(){
	  "use strict";
	  console.log(this);
	}
	fn();
	```
	> 在严格模式下，this的值根据执行时的上下文，this所保存的值决定。若为定义，this仍是undefined, 它可能被设置为任何的值，比如null，42或者是 " I'am not this "。
	
* **As an object methord 作为对象的方法**

	```
	var o = {};
	o.prop = 37;
	console.log(o);  //{prop:37}
	o.f = function(){
	  return this.prop;
	};
	console.log(o.f());  //37
	```
	
* **As a Constructor 作为构造器**

	当函数作为构造器（使用new关键词），它的this绑定为新构造的对象。
	
	```
	var o = {
	  a: 12,
	  f: function(){
    	return this.a;
	  }
	};
	var p = {
	  a: 21,
	  f: function(){
	    return o.f();
	  }
	};
	console.log(p.f());
	```
	> 注意：当然默认的构造器返回的this对象为当前调用对象，它能被当前对象中return的新对象所取代（如果对象的返回值不是对象，那么this仍指向当前对象）。
	
	```
	function C2(){
	    this.a = 38;
    	return {a:39};
	}
	o = new C2();
	console.log(o.a);   //39
	console.log(o);   //{a:39}  看一下这个才知道是怎么回事，里面根本就没有第一个a
	```
	
	> 在上面的例子中，因为有一个对象在构建中返回，所以this对象绑定到了返回的对象上。
	
* **call和apply**	

	在function内部使用this关键词时，它的值可以在使用call或apply（所有的function对象都继承自Function.prototype）调用时绑定为该函数中传入的对象。


	```
	function add(c,d){
		return this.a + this.b + c + d;
	}
	var o = {
		a: 2,
		b: 2
	};
	console.log(add.call(o,2,2));
	console.log(add.apply(o,[2,4]));
	```
	
* **As a DOM evnet handler 作为一个DOM事件处理程序**

	> 当一个function被用作为一个事件处理程序，它的this被设置为当前的元素（一些浏览器并不遵循这个规则而是动态的添加方法比如使用addEventListener）。


	```
	function fn(e){
	  console.log(this === e.target);
	  console.log(this === e.currentTarget);
	  this.style.backgroundColor = "#f90";
	}
	var eles = document.getElementsByTagName("*");
	for(var i=0; i< eles.length; i++){
	  eles[i].addEventListener('click',fn,false);
	}
	```

	

