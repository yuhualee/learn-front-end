### js类型

1. 类型

	* **基本数据类型：**基本数据类型里面存储的是具体的值，是可以直接访问的，可以直接进行操作。

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

	* **引用数据类型：**存储的是一个地址，是对空间的引用。访问的时候可以按照引用地址来访问，不可以直接操作对象的数据。
		
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

		
	---	

2. 检测类型的方法

	* **typeof**
	
		```
		var obj = 1;
		typeof obj; //"number"
		obj = "abc"
		typeof obj; //"string"
		obj = false
		typeof obj; //"boolean"
		obj = undefined;
		typeof obj; //"undefined"
		obj = null;
		typeof obj; //"object"，WTF，其实这是js的一个bug，人艰不拆 T_T
		//
		obj = function(){};
		typeof obj; //"function"
		obj = [];
		typeof obj; //"object"
		obj = {};
		typeof obj; //"object"
		obj = /w/g;
		typeof obj //"object"
		```
		> 从上面我们可以得出type能检测原始类型number,string,boolean,undefined，引用类型的function。
	
	* **instanceof**
	
		```
		var obj = function(){};
		obj instanceof Function; //true
		obj = [];
		obj instanceof Array; //true
		obj = {};
		obj instanceof Object; //true
		obj = new Date()
		obj instanceof Date; //true
		obj = /w/g;
		obj instanceof RegExp; //true
		//....桥豆麻袋, 事情其实还没完呢
		obj = [];
		obj instanceof Object; //true  草草嗒，所有引用类型其实都是继承自Object对象的，所以你懂的。
		```
		
		> incetanceof 操作符能鉴别引用类型，可惜有个缺憾是，如果想鉴别一个变量object类型而不是其他的function，array，date什么的，仍然需要花一番力气。
		
		> * 原始类型的变量直接保存原始值，而不是一个只想对象的指针。如果一个变量赋值给另一个变量，那么每个变量都它自己的一份数据拷贝，并不会相互影响。
		> * 引用类型的变量保存的是一个指向内存中实际对象所在的指针（或者说引用）。因此当你将一个对象赋值给变量时，实际是赋值给这个变量一个指针。意味着将一个变量赋值给另一个变量时，两个变量指向的是内存中同一个对象。
	
	* **Object.prototype.toString.call**
	
		```
		//低版本ie中undefined变量可以被修改，所以使用void 0 获取真实的undefined值，
		var isUndefined = function(obj) {
		    //or: return typeof obj === 'undefined';
		    return obj === void 0;
		};
		//typeof null 的结果是"object"。
		var isNull = function(obj) {
		    return obj === null;
		};
		// boolean值，number值和string值需要考虑两种情况，值为字面量时使用typeof和Object.prototype.toString能检测; 
		// 值为构造函数构建的时候需要使用Object.prototype.toString或者instanceof检测
		var isBoolean = function(obj) {
		    return Object.prototype.toString.call(obj) == '[object Boolean]';
		};
		var isNumber = function(obj) {
		    return Object.prototype.toString.call(obj) == '[object Number]';
		};
		var isString = function(obj) {
		    return Object.prototype.toString.call(obj) == '[object String]';
		};
		var isNaN = function(obj) {
		    return obj !== obj;
		};
		//
		//typeof 操作符在引用类型的变量里能对function有效。
		var isFunction = function(obj) {
		    //or:  return Object.prototype.toString.call(obj) == '[object Function]';
		    return typeof obj === 'function';
		};
		var isDate = function(obj) {
		    return Object.prototype.toString.call(obj) == '[object Date]';
		}
		var isArray = function(obj) {
		    return Object.prototype.toString.call(obj) == '[object Array]';
		}
		var isObject = function(obj) {
		    //or: return obj === Object(obj);
		    return Object.prototype.toString.call(obj) == '[object Object]';
		}
		var isRegExp = function(obj) {
		    //or: return obj === Object(obj);
		    return Object.prototype.toString.call(obj) == '[object RegExp]';
		}
		var has = function(obj, key) {
		    return Object.prototype.hasOwnProperty.call(obj, key);
		};
		//判断数组，字符串，对象是否为空
		var isEmpty = function(obj) {
		    if (obj == null) return true;
		    if (isArray(obj) || isString(obj)) return obj.length === 0;
		    for (var key in obj) if (has(obj, key)) return false;
		    return true;
		};
		```
	