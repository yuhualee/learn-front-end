# 变量作用域、闭包、this

## 变量

* **1. 变量的类型**

	**基本数据类型：**基本数据类型里面存储的是具体的值，是可以直接访问的，可以直接进行操作。

	* number 数字类型
	* string 字符串
	* undefined  未定义
	* boolean  布尔值
	* null

		```
		var a = b = c = 10;
		a = 11;
		alert(a);   //11
		alert(b);   //10
		```

	**引用数据类型：**存储的是一个地址，是对空间的引用。访问的时候可以按照引用地址来访问，不可以直接操作对象的数据。
		
		```
		var a = [1,2,3];
		function aaa(a){
   			 a = [1,2,3,4,]
		}
		aaa(a);
		alert(a);   //[1,2,3]
		```

		* object  对象
		* function

			```
			var a = b = {name:lyh,ege:18};
			a.name = "lee";
			alert(a.name);
			alert(b.name);
		```

* **2.变量的声明**

	变量的声明有两种方式：

	```
	var a;
	a = i;
	```

	* **局部变量：**在函数中使用var关键字进行显式申明的变量是做为局部变量。而函数体中的局部变量只在函数执行时生成的调用对象中存在，函数执行完毕时局部变量即刻销毁。
	
	* **全局变量：**而没有用var关键字，使用直接赋值方式声明的是全局变量。

		> 在js中，当我们使用一个没有定义的变量时，js会报错；而当我们直接给一个没有声明的变量赋值时，js会认为你在隐式声明一个全局变量。
	
		```
		function aaa(){
    		var a = b = 10;
		}
		aaa();
		//alert(a);   //报错，a没有定义
		alert(b);   //10，	
		```
		> 因为b前面没有直接var b = 10，它当作全局变量来处理了。

* **3. 变量的预解析**

	在js代码运行前，js会进行预解析，但是它只对var声明的变量进行预解析，也就是局部变量。对没有通过var声明的全局变量是不会进行预解析的。

	```
	var a = 10;
	functon aaa(){
		alert(a);
		var a = 20;
	}
	aaa();  //undefined
	```
	> 变量的就近原则，没找到的话，再向外层找。

* **4. 变量的作用域**
 
	函数中的变量在整个函数都中有效，外部函数无法读取函数内部定义的变量。

	```
function outPut(){
	alert(i);
}
var i=0;  //全局变量
function outer(){ 
	outPut(i); // 0  
	function inner(){ 
		outPut(i); //undefiend ,内部定义了变量，进行预解析
		var i=1; 
		outPut(i); //1 
	} 
	inner(); 
	outPut(i); //0 
} 
	outer(); 
```
> 在函数体里面声明的变量，在整个函数中都有效。在函数执行之前，会进行预解析，因此函数outer里面定义的var i = 1;，在函数inner里第一个outPut运行之前已经进行预解释，被赋值为undefined，而没有进行实际变量的赋值，所以输出undefined。

	例2：内部定义的变量，外部的函数是无法访问到的。

	```
var a = 10;
function aaa(){
    alert(a);
}
function bbb(){
    var a = 20;
    aaa();
}
bbb();   //弹出10
```
> 函数是要先进行预解析的，要看它在哪定义的，而不是在哪调用的。相对函数aaa()来说，bbb函数里面定义的a是局部变量，外部的aaa函数是无法调用到的。

* **5. 检测变量的类型**

	* **typeof** 返回一个表达js基本数据类型的字符串，可以是number,string,boolean,undefined,object,function。语法为：typeof a或者typeof(1);
	
		1. typeof是一个一元运算符，放在一个运算数之前，运算符可以是做任意类型的。
		
		2. 判断一个变量是否存在，要使用if(typeof a != "undefined")，而不能全用if(a)，因为如果a不存在，程序会报错。
		
		```
		if(typeof a != "undefined"){
			alert("变量a存在！");
		} 
		```

	* **instanceof** 用来检测某个变量是否是某一数据类型，或者一个变量是否是另外一个对象的实例，返回的是boolean类型。a instanceof b，其中的b可以是构造函数String，Object, Function。
		* 如下a即是Array的实例，也是Object的实例，但它的类型是object。
	
			```
			var a = [];
			alert(a instanceof Array);  //true
			alert(a instanceof Object); //true
			alert(typeof a);  //object
			```
		
			```
			function test(){};
			var a=new test();
			alert(a instanceof test);  //true
			```
			
		* 更重的一点是 instanceof 可以在继承关系中用来判断一个实例是否属于它的父类型。
			
			```
		function Foo(){} 
		Foo.prototype = new Aoo();//JavaScript 原型继承 
		var foo = new Foo(); 
		console.log(foo instanceof Foo)//true 
		console.log(foo instanceof Aoo)//true
		```
		
		* 判断arguments的类型：
		
			```
			alert(arguments instanceof Array);  //false
			alert(arguments instanceof Object);  //true
			```

	* **Object.prototype.toString**

		判断某个对象属于某中内置类型，最靠谱的方法就是Object.prototype.toString。

		```
		console.log(Object.prototype.toString.call([]));
		console.log(Object.prototype.toString.call({}));
		console.log(Object.prototype.toString.call(null));
		console.log(Object.prototype.toString.call(1));
		console.log(Object.prototype.toString.call("lee"));
		console.log(Object.prototype.toString.call(undefined));
		```

		* 输入结果 ：[object Array]、[object Object]、[object Null]、[object Number]、[object String]、[object Undefined]
		* 可能值："Array", "Boolean", "Date", "Error", "Function", "Math", "Number", "Object", "RegExp", "String".

	* **constructor**

		```
		var obj = "jeff wong"; 
		alert(obj.constructor == String); //true 
		function Cat(){};
		obj = new Cat(); 
		alert(obj.constructor == Cat); //true 
		```
		
		> 注意：null和undefined没有构造函数：如下，会报错。
		
		> ```
		var a = null;
		console.log(a.constructor);
		var b = undefined;
		console.log(b.constructor);
		> ```

