### 闭包

## 闭包、this
**闭包**：当一个方法在运行的时候，就会形成一个私有作用域，在这个作用域里，里面定义的变量不会受到上一级作用域或其它作用域的影响，不会和全局或其它作用域里的变量产生冲突。这个由方法运行而产生的私有作用域，就叫闭包。但是通常我们讲的闭包：是在函数内部定义返回一个函数，来读取内部变量。

**闭包的作用**：

1. 读取函数内部的变量
2. 让这些变量的值始终保存在内存中。(会使得内存过大)
> ```
> var n = 1;
> function fn(){
> 	var n = 99;
> 	nAdd = function(){
> 		n++;
> 	}
> 	return function inner(){
> 		alert(n);
> 	}
> }
> var result = fn;
> result();   //99
> nAdd();
> result();    //100
> alert(n);    //1
> ```

3. 如果我们想在闭包中用到我们的全局变量：
>1. window
>2. 传参数
>3. 我们在私有作用域里面别声明同名的变量
> 
```
;(function(){
	var a = 12;
	var b = 13;
	function fn(){
		alert(a+b);
	}
	window.fn = fn;
})(window);
window.fn();
```
4. 例子：
> 
```
var name = "The Window";
var object = {
  name : "My Object",
  getNameFunc : function(){
    return function(){
      return this.name;
    };
  }
};
alert(object.getNameFunc()());
```
> * **输出：The Window** 当this存在于function当中，它表示的是谁，和定义在哪没有关系 ，只和运行在哪有关。
> * **变量：**变量的值用哪个，和运行在哪没关系，只和定义在哪儿有关系。

* **例**
 
	```
var point = {
	x:10,
	y:20,
	moveTo:function(x,y){
		var moveX = function(x){this.x=x;}
		var moveY = function(y){this.y=y;}
		moveX(x);   //主体是window
		moveY(y);
	}	
}
point.moveTo(100,200);  //this是指point
console.log(point.x);
console.log(point.y);
console.log(x);
console.log(y);
```
>如何区分方法执行主体，看方法执行时候前面有没有“.”，有的话就是“.”前面的，没有就是window。


* **面试题**

	```
var number  = 2;
var obj = {
	number:4,
	fn1:(function(){
		this.number *= 2;
		number = number * 2;
		var number = 3;
		return function(){
			this.number *= 2;
			number *=3;
			console.log(number);
		}
	})(),
	db2:function(){
		this.number *= 2;
	}
};
var fn1 = obj.fn1;      
console.log(number);    //  4
fn1();       //
obj.fn1();   //
console.log(window.number);     //
console.log(obj.number);        //
```
**分析：**

	* 预解释：number、obj、fn1；
	
	* 执行代码：其中要注意的是，obj.fn1函数要自动执行，调用的主体是window，执行的结果是return的函数，但是需要注意，前面几行也要运行：

		```
this.number *=2;       //   **window.number = 4**;
number = number * 2;   //undefined*2 = NaN;
var number = 3;        //重新定义一个number = 3;
ruturn function(){};   //返回一个函数
```

	* fn1();

		```
		fn1=function(){
			this.number *= 2;
			number *=3;
			console.log(number);
		}
		```

		执行，里面出现的this都是指向window：window.number = ***8***;
number向上查找到var number = 3;运行结果**number = 9**；

	* obj.fn1(); 此时的this指向obj。则obj.number = 4 * 2 = ***8***;
number向上查找到，在fn1()执行时，number的值变为9，刚此时为 ***27****；



* **闭包的this是window**

	```
;(function(){
	if(this==window){
		alert("true");
	}
})();
```



## 重定向this???????