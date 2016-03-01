Date: 2014-09-16  
Title:原型和原型链   
Published: true  
Type: post  
Excerpt:   

## 1.面向对象

* **1.1 手工模式：单例模式**

	```
	var person = new Object();
	person.name = "lyh";
	person.sex = "female";
	```
	> 1. 问题：创建多个对象，代码重复
	> 2. 解决方法---工厂模式

* **1.2 工厂模式:就是对生产对象的流程进行封装**

	```
	function person(name,age){
		var obj = {};
		obj.name = name;
		obj.age = age;
		obj.getName = function(){
			alert(this.name);
		}
		return obj;
	}
	//批量生产对象
	var a = [];
	for(var i=0;i<10;i++){
		a.push(person("lyh"+i,18+i));
	}
	//单独设置
	var lyh = new person("李玉华",18);
	```

	> 1. 解决了我们批量生产的问题
	> 2. 随着发展我们还要区分产品的差异化----构造函数模式

* **1.3 构造函数**
		
	```
	function Person(name,age){
		this.name = name;
		this.age = age;
		this.getName = function(){
			alert(this.name);
		}
	}
	var p1 = new Person("lyh",18);
	var p2 = new Person("李玉华",18);
	alert(p1.getName);
	alert(p2.getName);
	alert(p1.getName==p2.getName);   //false
	```



---
---
---


* **基于构造函数的原型模式** 

	我们发现，不管是哪个实例，我们的writeCss或者writeJs其实都是同样的规范，我们不是每次new函数的时候重新的创建，那么我们如何创建了，又不用重复创建呢？
	
	> * object: 创建一个对象数据类型的数据，我们不仅在内存中开辟了一个空间，将自己私有的键值对存进来，而且还有一个系统自带的属性 _ proto _ 
	
	> * function:创建一个函数，我们不仅在内存中开辟了一个空间，将我们函数里面的js代码当成字符串存进去，而且还有一个系统自带的属性：prototype
	
	> * 
```
function constructFn(name,age){
		this.name = name;
		this.age = age;
}
constructFn.prototype.writeCss = function(){
};
constructFn.prototype.writeJs = function(){
};
var p1 = new constructFn("aaa",1);
var p2 = new constructFn("bbb",2);
p1.name;
p1.age;
p1.writeCss;
p1.writeJs;
alert(p1.writeCss==p2.wirteJs);   //指向同一内存，所以地址相同
```
	>* 如果我们的某个实例想获取类中prototype上定义的方法和属性，我们的原理是：实例中默认的 _ proto _ 属性去获取的.
	>* p1.wirteCss();----先在类中私有空间中找这个方法，如果没有的话，才去类的原型链上找，如果有，则不再去原型链上找



---
---

* **重新认识面向对象：**

	1. 一切事物皆对象
	2. 对象具有**封装和继承**的特性
	3. 对象与对象之间存在信息通信，各自存着信息隐藏
	
	javascript是通过原型（**prototype**）的方式来实现面向对象的。
	
	
---

## Prototype
	
* **Prototype模式**

	Javascript规定，每一个构造函数都有一个prototype属性，指向另一个对象。这个对象的所有属性和方法，都会被构造函数的实例继承。
	
	这就意味着，我们可以把那些*不变的属性和方法*，直接定义在prototype对象上：
	
	```
	function Person(name,age){
		this.name = name;
		this.age = age;
	}
	Person.prototype.type = '人';
	Person.prototype.say = function(){
		alert('Person');
	}
	var p = new Person('liyuhua',28);
	var p2 = new Person('liyuhua',28);
	alert(p.type == p2.type);    //true
	p.say();   //  Person
	```
	
	> 这样所有的实例的type属性和say方法，其实都是同一个内存地址，指向prototype对象，因此提高了运行效率。
	
* **isPrototype模式的验证方法**

	这个方法用来判断，某个prototype对象和某个实例之间的关系

	```
	alert(Person.prototype.isPrototypeOf(p));
	```
	
* **hasOwnProperty()**

	每个实例对象都有一个hasOwnProperty()方法，用来判断某一个属性到底是本地属性，还是继承自prototype对象的属性。

	```
	alert(p.hasOwnProperty('name'));    //true
	alert(p.hasOwnProperty('type'));    //flase
	```
	
* **in运算符**

	in运算符可以用来判断，某个实例是否含有某个属性，不管是不是本地属性。

	```
	p2.sayHello = function(){
		alert(this.name);
	}
	alert('sayHello' in p);     //false
	alert('sayHello' in p2);    //true
	```
	
	in运算符还可以用来遍历某个对象的所有属性。
	
	```
	for(var prop in p){
		alert('p[' + prop + ']=' + p[prop]);
	}
	```

	
## 	继承

* **构造函数绑定**

	```
	function Animal(){
		this.species = '动物';
	}
	function Cat(name,color){
		Animal.apply(this,arguments);
		this.name = name;
		this.color = color;
	}
	var cat1 = new Cat('花花','黄色');
	alert(cat1.species);    //动物 
	```

* **prototype模式**

	如果"猫"的prototype对象，指向一个Animal的实例，那么所有"猫"的实例，就能继承Animal了。
	
	```
	function Animal(){
		this.species = '动物';
	}
	function Cat(name,color){
		this.name = name;
		this.color = color;
	}
	Cat.prototype.say = function(){
		alert('cat');
	}
	Cat.prototype = new Animal();   //代码的第一行，我们将Cat的prototype对象指向一个Animal的实例。它相当于完全删除了prototype 对象原先的值，然后赋予一个新值。
	Cat.prototype.constructor = Cat;   //任何一个prototype对象都有一个constructor属性，指向它的构造函数。如果没有"Cat.prototype = new Animal();"这一行，Cat.prototype.constructor是指向Cat的；加了这一行以后，Cat.prototype.constructor指向Animal。
	var cat1 = new Cat('花花','黄色');
	alert(cat1.say());   //不存在
	```
	
	```
	Cat.prototype = new Animal();
	alert(Cat.prototype.constructor == Animal);   //true
	Cat.prototype.constructor = Cat;
	alert(Cat.prototype.constructor == Cat);    //true
	```
	
	每一个实例也有一个constructor属性，默认调用prototype对象的constructor属性。
	
	```
	alert(cat1.constructor == Cat.prototype.constructor);
	```
	
	> **这一点很重要，如果替换了prototype对象，则一定要为新的prototype对象加上constructor属性，并将这个属性指回原来的构造函数**
	
	```
	O.prototype = {};
	O.prototype.constructor = O;
	```
	
		
* **直接继承prototype**

	由于Animal对象中，不变的属性都可以直接写入Animal.prototype。所以，我们也可以让Cat()跳过 Animal()，直接继承Animal.prototype。


	```
	function Animal(){}
	Animal.prototype.species = '动物';
	```
	
	然后，将Cat的prototype对象，然后指向Animal的prototype对象，这样就完成了继承。
	
	```
	Cat.prototype = Animal.prototype;
	Cat.prototype.constructor = Cat;    //这一句实际上把Animal.prototype对象的constructor属性也改掉了！
	var cat1 = new Cat('花花','黄色');
	alert(cat1.species);    //动物
	```

	```
	alert(Animal.prototype.constructor == Cat.prototype.constructor);    //true
	```
	
	```
	var a1 = new Animal();
	alert(a1.constructor == Cat);
	```
	
* **利用空的对象作为中介**

	```
	function Animal(){};
	Animal.prototype.sepices = '动物';
	function Cat(name,color){
		this.name = name;
		this.color = color;
	}
	var F = function(){};
	F.prototype = Animal.prototype;
	Cat.prototype = new F();
	Cat.prototype.constructor = Cat;
	//F是空对象，所以几乎不占内存。这时，修改Cat的prototype对象，就不会影响到Animal的prototype对象。
	alert(Animal.prototype.constructor);
	```
	
	封装：
	
	```
	function Animal(){};
	Animal.prototype.sepices = '动物';
	function Cat(name,color){
		this.name = name;
		this.color = color;
	}
	function extend(Child,Parent){
		var F = function(){};
		F.prototype = Parent.prototype;
		Child.prototype = new F();
		Child.prototype.constructor = Child;
		Child.uber = Parent.prototype;
	}
	```
	
	使用
	
	```
	extend(Cat,Animal);
	var cat1 = new Cat('大典','黄毛');
	alert(cat1.sepices);
	```
	
	> 这个extend函数，就是YUI库如何实现继承的方法。
	
	```
	Child.uber = Parent.prototype;
	```
	> 意思是为子对象设一个uber属性，这个属性直接指向父对象的prototype属性。（uber是一个德语词，意思是"向上"、"上一层"。）这等于在子对象上打开一条通道，可以直接调用父对象的方法。这一行放在这里，只是为了实现继承的完备性，纯属备用性质。
	

## 非构造函数的继承

* **object()方法**

	```
	var Chinese = {
		nation: '中国'
	};
	function object(o){
		function F(){};
		F.prototype = o;
		return new F();
	}
	var Doctor = object(Chinese);
	Doctor.career = '医生';
	alert(Doctor.nation);   //中国
	```
	
	> 这个object()函数，其实只做一件事，就是把子对象的prototype属性，指向父对象，从而使得子对象与父对象连在一起。









