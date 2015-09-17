#前端开发面试题（js篇）

### 认识javascript

1. javascript的数据类型都有什么，它们的区别是什么

	* **基本数据类型：** number,string,boolean,undefined,null
	* **引用数据类型：**object,function 
	* **区别：**基本数据类型存储的是一个值，访问的时候是按照值来访问的，可以直接操作保存在变量中的值。引用数据类型存储的是一个地址，对内在空间的引用，访问的时候可以按照引用地址来访问，不可以直接操作对象的内存空间。
	
* 如何判断一个变量是什么类型的？

	* typeof
	* instanceof
	

* 例举3种强制类型转换和2种隐式类型转换?

	* 强制（parseInt,parseFloat,number）
	* 隐式（== – ===）

* 如何判断某变量是否为数组数据类型

	* **方法一：**判断其是否具有“数组性质”，如slice()方法，可自己给变量定义slice方法，故有时会失效
	
	* **方法二：**obj instanceof Array 在某些ie版本中不正确 
	
	* **方法三：** 方法一，二皆有漏洞，在ECMA Script5中定义了新方法Array.isArray()
	
		```
		if(typeof Array.isArray === 'undefined'){
			Array.isArray = function(arg){
				return Object.prototype.toString.call(arg) === '[object Array]'
			};
		}
		```
* 数据类型转换

	```
	var undefined;
	undefined == null; //true
	1 == true;  //true
	2 == true;  //false
	0 == false;  //true
	0 == '';  //true
	NaN == NaN;   //false
	[] == false;   //true
	[] == ![];    //true	
	```
	> 解释：对于不同类型的 “＝＝”判断，有如下一些规则，顺序自上而下：
	
	* undefined 与null相等
	* 一个是number，一个是string时，会尝试将string转换成number
	* 尝试将boolean转换成number，0或者1
	* 尝试将Object转换成number或string，取决于另外一个对比量的类型
	* 对于0、空字符串的判断，建议使用“===”，它会先判断两边的值类型，类型不匹配是为false。 		
* js表达式

	* 9+9+'abcd', 017 + 0 + 'abcd', 0x17 + 9 + 'abcd', 9- 'abcd'
	
	> * number + number = number		* boolean(转数字) + number = number / null(转数字) + number = number 
		* 如：1+true=1, true+true=2, null+false=0,1+null=1
	* number(转字符串) + string = string
	* object(toString) + string = string / number(toString) + object(toString) = string `5 + [1,2,3,4] -> 51,2,3,4`
	* number/boolean/null + undefined = NaN


* 引用数据类型

	```
	var a = new Object();
	a.value = 1;
	b = a;
	b.value = 2;
	alert(a.value); 
	```
	> 2
	
	```
	function test(obj){
		obj.value = 1;
		obj = new Object();
		obj.value = 3;
	}
	var a = new Object();
	a.value = 2;
	test(a);
	alert(a.value);
	```
	> 1
	
	```
	var a = [1,2];
	var b = a;
	console.log(b);
	a = [4,5];
	console.log(a);
	console.log(b);
	a.pop();
	console.log(a);
	console.log(b);
	```
	> [1,2],  [4,5],  [1,2],  [4],  [1,2]
	
	```
	var a = [0], b = a;
	b[0] = 2;
	console.log(a+b);  //22
	a = [0], b = a, b = [1];
	console.log(a+b);  //01
	```
	
* obj = {atr:1},那么获取atr属性的值，以下哪些做法是可以的：A,C,E

	A. obj.atr
	B. obj('atr')
	C. obj['atr']
	D. obj{'atr'}
	E. obj['a'+'t'+'r']
	F. obj[atr] 
	
* 以下哪个单词是不能被定义成变量: A,B,C,D,E,F

	A. with   B. parent  C. class  D. void  E. document  F. body
	
* 以下哪条语句会产生运行错误： A,E

	A. var obj = ();
	B. var obj = [];
	C. var obj = {};
	D. var obj = /\d/;
	E. var obj = //;
	
* 用for和while循环各自写一套九九乘法表
	
* `alert({})`弹出的结果是什么，为什么？

	弹出的结果是：[object,Object]，第一个指对象的类型是object类型，第二个指对象的constructor是Object类




===

### 字符串

1. 截取字符串bcdefg的efg

	```
	alert('abcdefg'.substring(4));
	```
	
* 统计字符串a出现的次数

	```
	var str = 'gdfafaagafa';
	String.prototype.count = function(){
		return this.split('a')）).length-1;
	}
	str.count();
	```
	```
	var str = 'gdfafaagafa';
	String.prototype.count = function(){
		return this.length - this.replace(/a/g,"").length;
	}
	str.count();
	```

	
* 判断一个字符串中出现次数最多的字符，并统计

	* **方法一：**

		```
		var str = 'abcdffefaaaagsssaeee';
		var json = {};
		for(var i = 0; i < str.length; i++){
			if(!json[str.charAt(i)]){
				json[str.charAt(i)] = 1;
			}else{
				json[str.charAt(i)]++;
			}
		};
		var iMax = 0;
		var iIndex = '';
		for(var i in json){
			if(json[i]>iMax){
				iMax = json[i];
				iIndex = i;
			}
		}
		alert('出现次数最多的是:'+iIndex+'出现'+iMax+'次');
		```
	* **方法二：见正则**
		
			
* JavaScript中如何检测一个变量是一个String类型？请写出函数实现

	```
	typeof(obj) == 'string';
	obj.constructor == String;
	```
	
* 字符串转驼峰写法

	* **方法一：字符串**
	
		```
		var str = 'border-top-color';
		function hump(str){
			var ary = str.split('-');
			for(var i=1;i<ary.length;i++){
				ary[i] = ary[i].charAt(0).toUpperCase()+a[i].substring(1);
			}
			return ary.join('');
		}
		```
		
	* **方法二：见正则**
	

	
===
	
### 数组

1. 把数据转成字符串 var str = ["this", "is" , "a","cat"];

	```
	var str = ["this", "is" , "a","cat"];
	console.log(str.join(" "));
	```
	
* var str = [3,6,2,4,1,5];

	1）实现对数组的倒序排列：
	
	```
	var str = [3,6,2,4,1,5];
	str.reverse();
	```
	2) 实现对该数组的降序排列
	
	```
	var str = [3,6,2,4,1,5];
	str.sort(function(a,b){
		return b-a;
	});
	```


* 编写一个方法 去掉一个数组的重复元素

	**方法一：**

	```
	var arr = [1,2,3,1,43,12,12,1];
	var json = {};
	var arr2 = [];
	for (var i = 0; i < arr.length; i++) {
        if(!json[arr[i]]){
        	json[arr[i]] = true;
        }else{
        	json[arr[i]] = false;
        }
        if(json[arr[i]]){
            arr2.push(arr[i]);
        }
	};
	for (var i = 0; i < arr.length; i++) {
        if(!aa(arr[i], arr2)){
             arr2.push(arr[i])
        }
	};
	function aa(obj, arr){
        for (var i = 0; i < arr.length; i++) {
        	if(arr[i] == obj) return true;
            else return false;
        };
	}
	alert(arr2)
	```
	
	**方法二：**
	
	```
	var a = [23,23,44,5,64,54,45,54,33,23];
	Array.prototype.distinct = function(){
    	for(var i=0; i<a.length-1; i++){
        	var cur = this[i];
	        for(var j=i+1;j<this.length;j++){
    	        if(cur==this[j]){
        	        this.splice(j,1);
            	    j--;
            	}
	        }
    	}
	}
	a.distinct();
	console.log(a);
	```
	
	**方法三：**
	
	```
	var a = [23,23,44,5,64,54,45,54,33,23];
	Array.prototype.distinct = function(){
    	var ary = this.concat();
	    for(var i=0; i<this.length-1; i++){
    	    for(var j=i+1;j<ary.length;j++){
        	    if(cur==ary[j]){
            	    this.splice(j,1);
                	j--;
	            }
    	    }
	    }
    	return ary;
	}
	var b = a.distinct();
	console.log(b);
	```
	
	**方法四：**
	
	```
	var a = [23,23,44,5,64,54,45,54,33,23];
	Array.prototype.distanct = function(){
	    var ary = this.concat();
    	//将我们原来的数组赋值给一个新的对象，这样以后的操作过程中，我们就用新的对象来操作，这样原有的数组就不会改变了。
	    var obj = {};
	    for(var i=0; i<ary.length; i++){
    	    if(obj[ary[i]]==ary[i]){
        	    ary.splice(i,1);
            	i--;
	        }else{
    	        obj[ary[i]]=ary[i];
        	}
	    }
    	return ary;
	}
	var b = a.distanct();
	console.log(b);
	```
	

* 如何深度克隆

	```
	var arr = [1,2,43];
	var json = {a:6,b:4,c:[1,2,3]};
	var str = 'sdfsdf';
	var json2 = clone(json);
	alert(json['c'])
	function clone(obj){
        var oNew = new obj.constructor(obj.valueOf());
        if(obj.constructor == Object){
                for(var i in obj){
                        oNew[i] = obj[i];
                        if(typeof(oNew[i]) == 'object'){
                                clone(oNew[i]);
                        }
                }
        }
        return oNew;
	}
	```

* splice和slice

* 对如下数组排序

	```
	var a = [12,44,6,77,47,9];
	function sortNumber(a,b){
    	return a - b;
	}
	alert(a.sort(sortNumber));
	```
* 字符串反转顺序

	```
	String.prototype.reverse = function(){
		var arry = this.split('');
		var str = arry.reverse().join('');
		return str;
	}
	```
* 数组和对象之间的关系是什么？

* 如何严格的判断一个数据是数组(Array)类的实例function isArray(val){return}

	```
	function isArray(value){
		if(typeof Array.isArray === 'function'){
			return Array.isArray(value);
		}else{
			return Object.prototype.toString.call(value) === '[object Array]';
		}
	}
	```


	
===

### 日期

1. 输出今天的日期，以YYYY-MM-DD的方式

	```
	var d = new Date();
	var year = d.getFullYear();
	var month = d.getMonth()+1;
	month = month < 10 ? '0' + month : month;
	var day = d.getDate();
	day = day < 10 ? '0' + day: day;
	console.log(year + '-' + month + '-' + day);
	```

### 操作符类型转换

===

### DOM

1. 已知ID的Input输入框，希望获取这个输入框的输入值，怎么做？(不使用第三方框架)

	```
	document.getElementById('ID').value;
	```

* 希望获取到页面中所有的checkbox怎么做？(不使用第三方框架)

	```
	var domList = document.getElementsByTagName(‘input')
	var checkBoxList = [];
	var len = domList.length;　　//缓存到局部变量
	while (len--) {　　//使用while的效率会比for循环更高
		if (domList[len].type == ‘checkbox') {
  　			checkBoxList.push(domList[len]);
	　　}
	}
	```
* 设置一个已知id的div的html内容为 XXXX，字体颜色设置为黑色

	```
	var dom = document.getElementById('id');
	dom.innerHTML = 'XXXX';
	dom.style.color = 'black';
	```
	

* 代码实现getPosition方法，获取一个元素在页面中的位置信息(x值 与 y值)

* 说说outerHTML,innerHTML,innerText的区别？

* 用原生js实现addClass和delClass功能


* js中的children和childNodes的区别

* clientWidth和offsetWidth的区别是什么？盒模型

* 计算浏览器的高度和宽度。

	```
	document.documentElement.clientHeight || document.body.clientHeight;
	```
	
* 如何计算浏览器中当前显示的页面的中心点的位置

	```
	var x = (document.documentElement.clientWidth || document.body.clientWidth)/2 + 'px';
	var y = (document.documentElement.clientHeight || document.body.clientHeight)/2 + 'px';
	```





### 动画

1. 代码实现一个元素的淡入，淡出

===

### 正则表达式

1. 编写一个方法 求一个字符串的字节长度

	```
	var str = '22两是';
	alert(getStrlen(str));
	function getStrlen(str){
        var json = {len:0};
        var re = /[\u4e00-\u9fa5]/;
        for (var i = 0; i < str.length; i++) {
        	if(re.test(str.charAt(i))){
            	json['len']++;
            }
        };
        return json['len']+str.length;
	}
	```

* 去掉重复的字符

	```
	var str = '4555640043aaaabbcdd333555';
	var reg = /(\w)\1+/g;
	console.log(str.replace(reg, '$1'));
	```
	
* 将字符串'<tr><td>{$id}</td><td>{$name}</td></tr>'中的{$id}替换成10，{$name}替换成Tony

	```
	var str = '<tr><td>{$id}</td><td>{$name}</td></tr>';
	str.replace(/{\$id}/g,'10').replace(/{\$name}/g, 'Tony');
	```
* 将字符串"Apple AppStore Webapp"中的app(不区分大小写)替换成APP

	```
	var str = 'Apple AppStore Webapp';
	str.replace(/app/gi,'APP');
	```
	
* 为了保证页面输出安全，我们经常需要对一些特殊字符进行转义，请写一个函数escapeHtml，将<，>, &, 进行转义

	```
	function escapeHtml(str){
		return str.replace(/[<>&]/g,function(match){
			switch(match){
				case "<": return '&lt;';
				case ">": return '&gt;';
				case "&": return '&amp;';
				case "\": return '&quot;';
			}
		});
	}
	```
	
*  判断一个字符串中出现次数最多的字符，并统计

	* **方法一：见字符串**


	* **方法二：正则**
		
		```
		var str = 'abcdffefaaaagsssaeee';
		function test(str){
			var num = 0;
			var value = '';
			str = str.split('');
			str.sort();
			str = str.join('');
			console.log(str);
			var regExp = /(\w)\1+/g;
			str = str.replace(regExp,function($0,$1){
				if($0.length> num){
					num = $0.length;
					value = $1;
				}
			});
			return "出现次数最多的字符是：" + value + ",共出现" + num + "次";
		}
		```
* 字符串转驼峰写法

	* **方法一：见字符串**
	
		
	* **方法二：正则**
	
		```
		var str = 'border-top-color';
		function hump(str){
			var regExp = /-(\w)/g;
			return str.replace(regExp,function($0,$1){
				return $1.toUpperCase();
			});
		}
		```

* 千分符

	```
	var str = '13456785436';
	var reg = /^([1-9]\d{0,2})((?:\d{3})+)$/;
	var s = str.replace(reg,function($0,$1,$2){
		return $1+','+$2.match(/\d{3}/g);
	});
	```

* 写一个函数实现清除字符串左右两边的空格

* 写一个电话号码匹配的正则

* 判断字符串以字母开头，后面可以是数字，下划线，字母，长度为6-30


===

### Math

1. 时间转换，把数字转换成分秒

	```
	function time(num){
		var num = Math.floor(num/60) + ':' + num%60;
		return num;
	}
	time(134);
	```


### Function

1. 下面这个js程序输出什么

	```
	function Foo() {
    	var i = 0;
	    return function() {
    	    console.log(i++);
    	}
	}
	var f1 = Foo(),
    	f2 = Foo();
	f1();    //0
	f1();    //1
	f2();    //0
	```
	
* 输出什么

	```
	function fn(){
		this.a = 0;
		this.b = function(){
			console.log(this.a);
		}
	}
	fn.prototype = {
		b:function(){
			this.a = 20;
			console.log(this.a);
		},
		c:function(){
			this.a = 30;
			console.log(this.a);
		}
	}
	var myfn = new fn();
	myfn.b();   //0
	myfn.c();   //30
	```
	
* 弹出来几次，每一次都是什么，为什么

	```
	var n = 0;
	function a(){
		var n = 10;
		function b(){
			n++;
		}
		b();
		return b;
	}
	var c = a();
	c();
	alert(n);
	```
	> 弹出一次，为0，因为function里面的n是能过var n来定义的属于内部变量，而alert(n)是外部变量，也就是最开始定义的

* 弹出什么

	```
	var s = 'abc12344';
	var num = parseInt(s);
	if(num==NaN){
    	alert('NaN');
	}else if(typeof num == 'number'){
    	alert('number');
	}else if(num=='abc'){
    	alert('abc');
	}else{
    	alert('str');
	}
	```


===

### 闭包

1. 闭包是什么，有什么特性，对页面有什么影响


* 动态生成10个a标签，给每个a标签绑定click事件，显示该元素被创建时的序号

* 例1

	```
	var n = 1;
	function fn(){
		var n = 99;
  		nAdd = function(){
  		  	n++;
		}
		return function inner(){
      		alert(n);
		}
	}
	var result = fn;
	result();   //99
	nAdd();
	result();    //100
	alert(n);    //1
	```
	
* 例2

	```
	function fn(a){
    	return function(b){
        	return a+b;
	    }
	}
	var x = fn(5);
	var x = fn(4);
	var y = fn(7);
	x(1);
	x(3);
	y(1);
	```

* 不用全局变量，用闭包实现输出从1自动递增




===

### 事件

1. 事件委托是什么

2. 如何阻止事件冒泡和默认事件

3. 当一个dom节点被点击时，绑定事件的几种方式是什么？

	* 直接在dom上绑定事件 `<div onclick = "test()"></div>`
	* 在js里通过onclick绑定 `div.onclick = test;`
	* 通知事件添加绑定 `addEventListener(xxx,'click',test)`
	
4. 如何获取用户在输入框里按下了回车键

	```
	function keypressEventHandle(event){
		if(event.keyCode == 13){
			alert('你点击了回车键！');
		}
	}
	someInput.onkeypress = keypressEventHandle;
	```
	
5. javascript的事件流模型都有什么

	* **事件冒泡：**事件是由最具体的元素接受，然后逐级向上传播
	* **事件捕捉：**事件由最不具体的节点先接收，然后逐级向下，一直到最具体的
	* **DOM事件流：**三个阶段：事件捕捉，目标阶段，事件冒泡
	
	





===

### setTimeout和setInterval

1. 如果在页面实现一个倒计时的功能？

* setTimeout和setInterval的区别

* 以下代码中end字符串什么时候输出

	```
	var t =、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、、】【【破哦怕之【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【【o0p-0p9o]\··1·11·12234	】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】】
		t = false;
	},1000);
	while(t){
		console.log('end');
	}
	```




===

### this

1. 写出3个使用this的典型应用
	
	* 事件：如onclick  this-> 发生事件的对象	
	* 构造函数： this-> new 出来的object
	* call/apply:  改变this
2. 例

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
3. 例

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
	_add.call(_sub);
	console.log(_sub.test);
	```
	
4. 例
	
	```
	ar test = 111;
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
	
5. 例
	
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



===

### 预解析

1. 例1

	```
	var a = [1,2,3];
	function aaa(a){
    	 a = [1,2,3,4,]
	}
	aaa(a);
	alert(a);  
	```
	
	```
	function aaa(){
		var a = b = 10;
	}
	aaa();
	alert(a);  
	alert(b);
	```
	> 预解析，因为b前端没有var b = 10，它被当作全局变量
	
2. 例2
	
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
	> 解析
	
3. 例3
	
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
	
4. 例4

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



	

	

===

### argument

1. 判断arguments是不是数组

	```
	alert(arguments instanceof Array);
	alert(arguments instanceceof Object);
	```

* 如何严格的判断一个数据是数组（Array）类的实例

	```
	function isArray(value){
		if(typeof Array.isArray === 'function'){
			return Array.isArray(value);
		}else{
			return Object.prototype.toString.call(value) === '[object Array]';
		}
	}
	```

* 把arguments转换成数组
	
	方法一：内置的类型可以通过prototype找到内置的属性方法，Array.prototype.slice就是访问Array的内置方法slice。通过slice方法，返回一个数组。call是调用一个对象的方法，以另外一个对象替换当前对象。

	```
	var arg = Array.prototype.slice.call(argument,0);
	```
	
	方法二：
	
	```
	var arg = [].slice.call(arguments,0);
	```
	
	方法三：通过循环转变数组
	
	```
	function toArray(arguments){
		var a = [];
		for(var i=0; i<arguments.length; i++){
			a.unshift(arguments[i]);			
		}
		return a;
	}
	```
	
* 求1-n的和

	```
	function fn(n){
		if(n == 1) return n;
		else return n + arguments.callee(n - 1);
	}
	```

* 下面的console.log的结果是[1,2,3,4]的是？

	1）
	
	```
	function foo(x){
		return x;
	}
	foo(1,2,3,4);
	```
	
	2）
	
	```
	function foo(x){
		return x;
	}(1,2,3,4)
	```
	
	3)
	
	```
	(function foo(x){
		return x;
	}(1,2,3,4));
	```
	
	4)
	
	```
	function foo(){
		bar.apply(null,arguments);
	}
	function bar(x){
		console.log(arguments);
	}
	foo(1,2,3,4);
	```
* 用什么方法实现对函数内置的arguments对象进行排序？

* 请举例使用callee属性实现函数的递归


===

### call和apply

1. call和apply的作用，以及区别？

* 例

	```
	function fn1(){
		alert(1);
	}
	function fn2(){
		alert(2);
	}
	fn3 = fn2.call;
	fn2.call(fn1);   //请问输出结果，为什么
	fn3.call(fn1);   //请问输出什么结果，为什么
	fn3.call(fn1);   //请问输出什么结果，为什么
	```


===

### ajax

1. ajax请求的时候get和post方式的区别

	* GET：一般用于信息获取，使用URL传递参数，对所发送信息的数量也有限制，一般在2000个字符
	* POST：一般用于修改服务器上的资源，对所发送的信息没有限制

	* GET方式需要使用 Request.QueryString 来取得变量的值
	* POST方式通过 Request.Form 来获取变量的值
	也就是说 Get 是通过地址栏来传值，而 Post 是通过提交表单来传值。

	* 在以下情况中，请使用 POST 请求：
		* 无法使用缓存文件（更新服务器上的文件或数据库）
		* 向服务器发送大量数据（POST 没有数据量限制）
		* 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠


* ajax请求时，如何解释json数据,什么是Ajax和JSON，它们的优缺点。

* Ajax 是什么？Ajax 的交互模型？同步和异步的区别？如何解决跨域问题？

	* **Ajax 是什么：**
	
		1. 通过异步模式，提升了用户体验
		2. 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用
		3. Ajax 在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。

	* **Ajax 的最大的特点：**
	
		1. Ajax可以实现动态不刷新（局部刷新）
		2. readyState 属性 状态 有5个可取值： 0 = 未初始化，1 = 启动， 2 = 发送，3 = 接收，4 = 完成

	* **Ajax 同步和异步的区别:**
	
		1. 同步：提交请求 -> 等待服务器处理 -> 处理完毕返回，这个期间客户端浏览器不能干任何事
		2. 异步：请求通过事件触发 -> 服务器处理（这是浏览器仍然可以作其他事情）-> 处理完毕
	
	* **ajax.open方法中，第3个参数是设同步或者异步。**

	* **Ajax 的缺点：**
	
		1. Ajax 不支持浏览器 back 按钮
		2. 安全问题 Ajax 暴露了与服务器交互的细节
		3. 对搜索引擎的支持比较弱
		4. 破坏了程序的异常机制
		5. 不容易调试

	* **解决跨域问题：**
	
		1. jsonp
		2. iframe
		3. window.name、window.postMessage
		4. 服务器上设置代理页面

* 描述完成一个异步交互需要的关键步骤及其注意事项

* ajax中如何实现jsonp跨域，说说原生js实现方法

* 表单提交，如何防止用户多次提交，减少服务器端的压力

* 什么是json，它有什么优点？

* ajax有什么优缺点？

	* **优点**
		* 可以使得页面在不重载全部内容的情况下加载局部内容，降低数据传输量
		* 避免用户不断刷新或者跳转页面，提高用户体验
	
	* **缺点**
		* 对搜索引擎不友好
		* 要实现ajax下的前进后退功能成本较大
		* 可能造成请求数的增加
		* 跨域问题限制

* http请求的状态码都有哪些，都代表什么意思？

* json是什么？(json和javascript对象有什么区别？)如何把js对象转化为json字符串？又如何把json字符串转化为javascript对象？

	
	* json是javascript对象表示法，是轻量级的文本数据交换格式
	* 可以通过javascript eval()方法进行解析
	



### 对象

1. js对象的深度克隆代码实现

	```
	function clone(Obj) {
    	var buf;   
	    if (Obj instanceof Array) {
    	    buf = [];  // 创建一个空的数组
       		var i = Obj.length;
	        while (i--) {
    	        buf[i] = clone(Obj[i]);
        	}
	        return buf;
    	} else if (Obj instanceof Object){
        	buf = {};  // 创建一个空对象
	        for (var k in Obj) {  // 为这个对象添加新的属性
    	        buf[k] = clone(Obj[k]);
	        }
    	    return buf;
	    }else{
    	    return Obj;
	    }
	}
	```

* 谈谈Function.prototype.bind这种扩展的优势


### 算法

1. 一列数的规则如下：1，1，2，3，5，8，13，21，34...求第30位数是多少（用递归算法实现）

### 浏览器兼容性

### 概念

1. 闭包

2. ajax的工作原理



### 网页性能优化

1. 你如何优化自己的代码？

	* 代码重用
	* 避免全局变量（命名空间，封闭空间，模块化mvc..）
	* 拆分函数避免函数过于臃肿
	* 注释

	
* js延迟加载的方式有哪些？

	* defer和async
	* 动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）
	* 按需异步载入js
	
* 如何解决跨域问题?

	*  jsonp（jsonp 的原理是动态插入 script 标签）
	* document.domain + iframe
	* window.name、window.postMessage
	* 服务器上设置代理页面
	
	
* 提高web页面传输性能有哪些方法

	* 降低传输文件的大小
		* 尽量减小页面、代码、图片的体积
		* 对静态脚本进行压缩
		* 使用gzip在服务端进行压缩
		* 减少cookie使用
		* 尽量使用get
		
	* 降低传输的请求次数
		* 合并脚本文件
		* 合并图片文件
		* 不滥用ajax
		
	* 服务端
		* 使用cdn，更高性能的静态服务器，动静分离部署、减少转向等等
		
* http怎么处理内存
	

	
### 综合题目

1. 实现一个函数objectClone，可以对javascript中的5种主要的数据类型（包括number,string,Object,Array,Boolean）进行复制

	```
	function clone(obj){
		var newObj = {};
		if(typeof obj == 'object'){
			for(key in obj){
				newObj[key] = clone(obj[key]);
			}
		}else{
			newObj = obj;
		}
		return newObj;
	}
	```
	> * 对于基本数据类型和引用数据类型在内存中存放的是值还是指针这一区别，是否清楚
	* 是否知道如何判断一个变量是什么类型的
	* 递归算法的设计
	
2. 想实现一个对页面某个节点的拖拽，如何做？

	1. 给需要拖拽的元素绑定mousedown,mousemove,mouseup事件
	2. mousedown事件触发时，通过event.clientX和event.clientY，获取拖拽的位置，开始拖拽
	3. mousemove时，同时需要通过event.clientX和event.clientY，获取拖拽的位置，并实时位置
	4. mouseup时，拖拽结束
	5. 需要注意浏览器边界的情况
	
3. 



