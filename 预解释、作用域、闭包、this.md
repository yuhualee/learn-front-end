# 预解释、作用域、闭包、this

## 内存
在我们js中，存储数据的空间我们可以分为两种：堆内存、zhan内存。

* **堆内存：**我们定义的那些引用数据类型的数据，都会在堆内存中开辟空间。
* **zhan内存：**我们运行的js代码，还有我们定义的基本数据类型，都直接在占内存中存储
>js在运行之前，先会找所有带var和function关键字的，先把他们声明，找完了，然后从上到下执行我们的js代码。

##预解释 
**预解释：**在当前作用域下，js代码运行之前，我们先把带var和function关键字的提前声明（declare），并且在内存里安排好。

```
1. var a;  //声明一个变量，但是并没有赋值，那就是undefined。
2. a = 12;   //先在栈内存中，开辟一个空间存储我们的12。
3. 再将我们的12和a关联。
```


>带var和function的预解释是不一样的

>通过我们的var关键字的都是声明declare

>function不仅声明而且还定义define了，但是他存储数据的那个空间里面存储的都是代码字符串，没有任何的意义。

**预解释是发生在作用域下的，刚开始进来的时候，我们预解释的是全局作用域（*global*），在js中我们的global就是我们的window**

1. 我们运行函数的时候会生成一个**新的私有作用域**（每次执行都是新的，执行完就销毁），这个作用域下（我们可以理解为开辟了一个新的栈内存），在这个内存中我们也要执行我们的预解释机制，***当我们的函数执行完成后，这个内存或者作用域就会销毁***。
>**function的运行周期**：从我们window下的预解释开始就声明和定义了，当我们的function执行的时候，会产生新的作用域，当function执行完成，通常情况下作用域就会自己销毁。
2. 如果在当前作用域下的一个变量没有预解释，就向它的上一级去找，直到找到window，如果window下也没有定义，就会报错。
3. **预解释只发生在var和function身上**，也就是只能对var和function进行提前声明定义，window.a这样的不会进行预解释。
4. **预解释只对当前脚本块中起作用**。
5. 预解释不会在同一个变量上重复的发生，也就是一个变量如果已经在当前作用域下预解释了，那么就出现同样的就不再预解释了。
6. js预解释只对＝左边带var的预解释，＝右边是赋值，不会进行预解释。

比如：

```
alert(a); 
fn(); 
var a = function fn(){};
```
>第一次打印undefined，第二次报错，未定义。


```
alert(a);
if(1==2){
	var a=12;
}
```
>预解释是**不受其它if或者其它判断条件影响**的，也就是说，即使条件不成立，我们里面只要有var或者function也会被预解释。

###面试题
```
if(!("a" in window)){
	var a = "珠峰培训"；
}
alert(a);       //undefined
```
>我们的预解释也不会受到function里面的return影响

```
function fn(){alert("我们是全局的fn");}
function fn2(){
	alert(fn);
	fn = 3;
	return ;
	function fn(){alert("我是fn2里面的");}
}
```
>定义一个function，如果我们只是return； 没有返回任何东西，外面接收的是undefined，如果不加return也是undefined

```
var n = 0;
function a(){
	var n = 10;
	function b(){
		n++;
		alert(n);
	}
	b();
	return b;
}
var c = a();    //a()执行一次，弹出11，并且把返回值赋给c，此时的c为function b(){}
c();            //alert(n),12
alert(n);       // 0
```
>return直接返回的那个，其实是一个结果或者是值，是不需要预解释的。

```
var n = 99;
function outer(){
	var n = 0;
	return function inner(){
		return n++;
	}
}
var c = outer();   //c=function inner(){ return n++; }
var num1 = c();    //0，然后再执行n++  此时n=1;
var num2 = c();    //1,  n++   2;
var d = outer();   //重新开辟新
var num3 = d();    //0
```
>当我们的一个函数返回一个新的function，我们在外面定义一个变量来接收，这样这个函数的内存就不能在执行完成后自动销毁，也就是我们所谓的函数内存被占用了。

## 闭包
**闭包**：当一个方法在运行的时候，就会形成一个私有作用域，在这个作用域里，里面定义的变量不会受到上一级作用域或其它作用域的影响，不会和全局或其它作用域里的变量产生冲突。这个由方法运行而产生的私有作用域，就叫闭包。
>如果我们想在闭包中用到我们的全局变量：

>1. window
>2. 传参数
>3. 我们在私有作用域里面别声明同名的变量

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



##this、变量
**this:**只存在于function当中，它表示的是谁，和定义在哪没有关系，只和运行在哪有关系。

**变量：**变量的值用哪个，和运行在哪没关系，只和定义在哪儿有关系。

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

### 面试题

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