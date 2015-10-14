Date: 2014-08-24  
Title:   
Published: true  
Type: post  
Excerpt: 


# call和apply


## 定义

1. **定义：** 调用一个对象的一个方法，以另一个对象替换当前对象。

2. **参数：** call(thisObj,arg1,agr2...)

	* thisObj：可选项，将被用作当前对象的对象
	
	* arg1，arg2...可选项，将被传递方法参数序列
	
3. **说明：** call方法可以用来代替另一个对象调用一个方法。call方法可以将一个函数的对象上下文从初始的上下文改变为thisObj指定的新对象。如果没有thisObj，那么Global对象被用作thisObj。

---

## 边走边看

1. 调用方法

	obj1.method1.call(obj2,arg1,arg2):call的作用就是把obj1的方法放到obj2上使用，后面的arg作为参数传入。

	如下：

	```
	function add(a,b){alert(a+b);}
	function sub(a,b){alert(a-b);}
	add.call(sub,3,1);
	```
	
	> 如果把add的对象当作window，那么就是window.add.call(sub,3,1)，也就是sub.add(3,1)。其实就是把add当成sub的一个方法调用。

* 继承

	```
	funciont class1(){
		this.showTxt = function(txt){
			alert(txt);
		}
	}
	function class2(){
		class1.call(this);
	}
	var c2 = new class2();
	c2.showTxt("cc");
	```
	
	 这样class1.call(this)的意思：此时的this指向class2，也就是class2中就是有了class1的属性和方法，c2对象就能直接调用class2的方法和属性了。执行结果就是：alert("cc");注意，是this指向了class2,如果class1里面有不带this的属性，它是不指向class2的，如下：
	
	```
	function f1(){
	  a = 1;
	  this.show = function(txt){
	    alert(txt);
	  }
	}
	function f2(){
	  f1.call(this);
	}
	var f = new f2();
	f;  //输出 f2 { show=function()}
	```
	

	```
	function f1(){
		this.a = 1;
		this.show = function(txt){
		    alert(txt);
		}
	}
	function f2(){
	  f1.call(this);   //仍为function
	}
	var f = new f2();  //构造函数object
	f; //f2 { a=1, show=function()}
	```

*  改变this

	例1：

	```
	var test = 111;
	function _add()  
	{  
	    this.test = 444;  //注释①
	    console.log(this.test);  
	}  
	function _sub()
	{  
	    this.test = 222;
	    console.log(this.test);  
	}  
	_add();//弹出444          
	_sub();//弹出222
	_add.call(_sub);   //执行函数_add()，但是里面的this指向_sub,这里面可以打印this是_sub();
	console.log(_sub.test);  //这里的test是_add()里面的，而_sub()里面的test，因为还没有执行，所以它存在，但如果执行_sub()，则window.test = 222;
	``` 
	> * 执行_add.call(_sub)时，它是在执行_add()，但是里面的this，指向_sub，也就是设置了_sub.test = 444，然后console.log(_sub.test);所以输出是444。相当于：
	
		```
		(_add{
			_sub.test = 444;
			console.log(_sub.test);  //444
		}());
		//多了一个全局变量_sub.test;
		console.log(_sub.test);   //输出444
		console.log(window.test);   //111;第一行定义的变量；
		_sub();  //执行这个 会输出222，那么window.test = 222;
		```
	
	 
	例2：
	
	```
	var test = 111;
	function _add()  
	{  
	    //this.test = 444;  //注释①
	    console.log(this.test);  
	}  
	function _sub()
	{  
	    this.test = 222;
	    console.log(this.test);  
	}  
	_add();//弹出111,_add中this指向window      
	var d=new _sub();//_sub中this指向d
	console.log(test);//弹出111  ！！！！！！！！
	_sub();//弹出222,_sub中的this继续指向window
	console.log(test);//执行_sub()的结果！！！！！！！！
	_add.call(_sub);//_add中this指向_sub,_sub无test属性,undefined
	```
	
	例3：
	
	```
	var test = 111;
	function _add()  
	{  
	    this.test = 444;  //注释①
	    console.log(this.test);  
	}  
	function _sub()
	{  
	    this.test = 222;
    	console.log(this.test);  
	}  
	_add();//弹出444,_add中this指向window,则window.test变成444      
	var d=new _sub();//_sub中this指向d，弹出222
	console.log(test);//弹出444，第一步执行结果
	_sub();//弹出222,_sub中的this继续指向window
	console.log(test);//执行_sub()的结果222
	_add.call(_sub);//_add中this指向_sub,相当于_sub.test = 444;console.log(_sub.test);注意，这里的_sub.test和_sub里面的this.test并不是同一个。
	```
	
	例4：
	
	```
	var test = 111;
	function _add()  
	{  
	    this.test = 444;  //注释①
    	this();   //其实是执行_sub()，所以输出222
	    console.log(this.test);  
	}  
	function _sub()
	{  
    	this.test = 222;
	    console.log(this.test);  
	}  
	_add.call(_sub);
	```
	---


## call和apply的区别

1. call和apply其实是一样的，唯一的区别在于他们调用参数，call是一个一个的调用 ，而apply是是调用一个数组，或者类数组。
	
	```
	foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments) == this.foo(arg1, arg2, arg3)
	```
	> call, apply方法区别是,从第二个参数起, call方法参数将依次传递给借用的方法作参数, 而apply直接将这些参数放到一个数组中再传递, 最后借用方法的参数列表是一样的.