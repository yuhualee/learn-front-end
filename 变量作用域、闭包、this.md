# 变量作用域、闭包、this

## 变量
#### 1. 变量的类型

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

* object  对象
* function

```
var a = b = {name:lyh,ege:18};
a.name = "lee";
alert(a.name);
alert(b.name);
```

#### 2. 变量的声明

变量的声明有两种方式：

```
var a;
a = i;
```

* **局部变量：**在函数中使用var关键字进行显式申明的变量是做为局部变量。而函数体中的局部变量只在函数执行时生成的调用对象中存在，函数执行完毕时局部变量即刻销毁。
* **全局变量：**而没有用var关键字，使用直接赋值方式声明的是全局变量。

> 在js中，当我们使用一个没有定义的变量时，js会报错；而当我们直接给一个没有声明的变量赋值时，js会认为你在隐式声明一个全局变量。

#### 3. 变量的预解析

在js代码运行前，js会进行预解析，但是它只对var声明的变量进行预解析，也就是局部变量。对没有通过var声明的全局变量是不会进行预解析的。

#### 4. 变量的作用域
 
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

#### 5. 检测变量的类型

1. typeof 返回一个表达js基本数据类型的字符串，可以是number,string,boolean,undefined,object,function。语法为：typeof a或者typeof(1);
> 1. typeof是一个一元运算符，放在一个运算数之前，运算符可以是做任意类型的。
> 2. 判断一个变量是否存在，要使用if(typeof a != "undefined")，而不能全用if(a)，因为如果a不存在，程序会报错。
> > ```
> if(typeof a != "undefined"){
> 	 alert("变量a存在！");
> } 
> ```
> 
> 3. 在
2. **instanceof** 用来检测某个变量是否是某一数据类型，或者一个变量是否是另外一个对象的实例，返回的是boolean类型。a instanceof b，其中的b可以是构造函数String，Object, Function。
> 1. 如下a即是Array的实例，也是Object的实例，但它的类型是object。
> > ```
> var a = [];
> alert(a instanceof Array);  //true
> alert(a instanceof Object); //true
> alert(typeof a);  //object
> ```
> > ```
> function test(){};
> var a=new test();
> alert(a instanceof test);  //true
> ```
> 2. 更重的一点是 instanceof 可以在继承关系中用来判断一个实例是否属于它的父类型。
> > ```
> function Foo(){} 
> Foo.prototype = new Aoo();//JavaScript 原型继承 
> var foo = new Foo(); 
> console.log(foo instanceof Foo)//true 
> console.log(foo instanceof Aoo)//true
> ```
> 3. 判断arguments的类型：
> > ```
> alert(arguments instanceof Array);  //false
alert(arguments instanceof Object);  //true
> ```
3. tostring
4. constructor
> ```
> var obj = "jeff wong"; 
> alert(obj.constructor == String); //true 
> function Cat(){};
> obj = new Cat(); 
> alert(obj.constructor == Cat); //true 
> ```
> 注意：null和undefined没有构造函数：如下，会报错。
> > ```
> var a = null;
console.log(a.constructor);
var b = undefined;
console.log(b.constructor);
> ```

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

5. 例
> 
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


## 面试题

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
#### 分析：
>1. 预解释：number、obj、fn1；
>2. 执行代码：其中要注意的是，obj.fn1函数要自动执行，调用的主体是window，执行的结果是return的函数，但是需要注意，前面几行也要运行：
>
```
this.number *=2;       //   **window.number = 4**;
number = number * 2;   //undefined*2 = NaN;
var number = 3;        //重新定义一个number = 3;
ruturn function(){};   //返回一个函数
```
>3. fn1();
>
```
fn1=function(){
	this.number *= 2;
	number *=3;
	console.log(number);
}
```

>执行，里面出现的this都是指向window：window.number = ***8***;
number向上查找到var number = 3;运行结果**number = 9**；

>4. obj.fn1(); 此时的this指向obj。则obj.number = 4 * 2 = ***8***;
number向上查找到，在fn1()执行时，number的值变为9，刚此时为 ***27****；



**
闭包的this是window
**

```
;(function(){
	if(this==window){
		alert("true");
	}
})();
```



## 重定向this???????