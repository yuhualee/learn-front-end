# **javascript事件**

#### 事件流

DOM(文档对象模型)结构是一个树型结构，当一个HTML元素产生一个事件时，该事件会在元素结点与根节点之间按特定的顺序传播，路径所经过的节点都会收到该事件，这个传播过程可称为DOM事件流。事件顺序有两种类型：事件捕捉和事件冒泡。

1. 事件流

	描述的是在页面中接受事件的顺序


* 事件冒泡

	由最具体的元素接收，然后逐级向上传播至最不具体的元素的节点（文档）
	
	```
	//html
	<div id="l1">这是l1
		<div id="l2">这是l2
			<div id="l3">这是l3
				<div id="l4">这是l4</div>
			</div>
		</div>
	</div>
	```
	```
	//javascript
	;(function(){
		var l1 = document.getElementById("l1");
		var l2 = document.getElementById("l2");
		var l3 = document.getElementById("l3");
		var l4 = document.getElementById("l4");
		l1.onclick = function(){
			alert("l1");
		}
		l2.onclick = function(){
			alert("l2");
		}
		l3.onclick = function(){
			alert("l3");
		}
		l4.onclick = function(){
						alert("l4");
		}
		document.onclick = function(){
			alert("这是document");
		}
	})();
	```
	> 点击最里层时，四个div上的事件都会被触发，最终到达document上面。所以我们很多时候会利用事件冒泡，把事件绑定到document上，通过判断e.target，来触发事件，就是事件委托。


* 事件捕获

	最不具体的节点先接收事件，而最具体的节点应该是最后接收事件
	
#### 事件处理

1. html事件处理

	直接添加到html结构中
	
	```
	<button onclick = 'demo()'> 点击</button>
	```
	> 1. 结构和表现不分离
	
	> * 修改麻烦
	

* dom0级事件处理

	把一个函数赋值给一个事件处理程序属性
	
	```
	obj.onclick = function(){
		//code
	}	
	obj.onclick ＝ null;
	```
	
	> 缺点，多个事件会被覆盖掉
	
		```
		obj.onclick = function(){
			//code  111
		}
		obj.onclick = function(){
			//code  222
		}
		```

	
* dom2级事件处理

	* addEventListener('事件名'，‘事件处理函数’，‘布尔值’);
	
		* true - 事件捕获
		
		* false - 事件冒泡
		
		```
		function demo1(){
			// ...code...
		}
		function demo2(){
			//...code...
		}
		function demo3(){
			//...code...
		}
		obj.addEventListener('click',demo1,false);
		obj.addEventListener('click',demo2,false);
		obj.addEventListener('click',demo3,false);
		```
		> 事件不会覆盖
	
	* removeEventListener();
	
		```
		obj.removeEventListener('click',demo2);
		```

* ie事件处理程序

	* attachEvent
	
		```
		if(btn.addEventListener){
			btn.addEventListener('click',fn,false);
		}else if(btn.attachEvent){
			btn.attachEvent('onclick',fn);
		}else{  //ie8之前的浏览器，只能处理dom0级事件处理
			bnt.onclick = fn();
		}
		```
	
	* detachEvent - 
	
#### 事件对象

* 事件对象

	在触发DOM事件的时候都会产生一个对象
	
* 事件对象event

	1. e: 
	
		```
		function demo(e){
			var e = e || window.event;   //标准事件
			var target = e.target || e.srcElement;  //目标元素
			var type = e.type;   //事件类型
			//阻止默认行为
			if(e.preventDefault){
				e.preventDefault();    //标准浏览器，
			}else{
				e.returnValue = false;   //ie
			}
			//阻止事件传播
			if(e.stopPropagation){
				e.stopPropagation();
			}else{
				e.cancelBubble = true;
			}
		}	
		//-----
		```


	* type: 获取事件类型 
	
		```
		document.getElementById('btn').addEventListener('click',showType);
		function showType (e) {
		  alert(e.type);
		}
		```
	
	* target: 获取事件目标
	
		```
		function show(e){
		    alert(e.target);
		}
  		document.body.addEventListener('click',show);
  		//[object HTMLButtonElement]
		```
	
	* stopPropagation(): 阻止事件冒泡
	
	* preventDefault(): 阻止事件默认行为
	
	* 事件绑定
	
		```
		//事件绑定----	
		function addEventHandle(target,type,fn){
			if(target.addEvnetListener){ //IE9及以上，标准浏览器
				target.addEventListener(type,fn,flase);
			}else if(target.attachEvent){  //ie8及以下
				target.attachEvent('on'+type,fn);
			}else{
				target['on'+type] = fn();
			}
		}
		```
		
	* 解除绑定
	
		```
		function removeEventHandle(target,type,fn){
			if(target.removeEventListener){
				target.removeEventListener(type,fn);
			}else if(target.detachEvent){
				target.detachEvent('on'+type,fn);
			}else{
				delete target['on'+type];
			}
		}
		```


* **事件委托：**

	事件委托就是用事件传播的机制，无论哪一个网页元素，它的click事件都会最终传到document上。这样，则只需在document上处理click事件既可。


	事件委托是冒泡的一个应用，可以减少绑定次数，同时也不用担心内部元素的改变，也不需要在内部元素改变后，重新进行绑定。


	* 例：6.1 
	
		```
		;(function(){	
			document.onclick = function(e){
				e = e || window.event;
				var t = e.target || e.srcElement;  //兼容
				var id = t.getAttribute("id");
				alert(id);
			}
		})();
		```
		
	* 例6.2 
		
		```
		//注意：如果在例6.1中加入下面的代码，将阻止冒泡
		l3.onclick = function(e){
			e.stopPropagation();
		}
		```
		
		* 点击l4,l3都将阻止冒泡，因为在l3阶段阻止了，其内部的冒泡也会被阻止掉。
		
		* 如果委托内部有其它点击事件也需要单独处理，如果不处理，也会把点击事件委托到外层。
		
		* 内部的a链接也会被委托的事件代替，需要单独处理，阻止链接事件的冒泡```e.stopPropagation();```。如果a链接要绑定委托事件，则```return false;```。
		
		
* **事件监听：**

	* addEventListener(type,fn,boolean)，前面两个参数不用解释，第三个参数boolean，就是决定注册事件发生在捕 获阶段还是冒泡阶段，
		
		```
		obj.addEventListener("click", func, true); // 捕获方式
		obj.addEventListener("click", func, false); // 冒泡方式
		```
	
	* false : 冒泡阶段
	
		例7.1 继续上面的例子  
		 
		```
		;(function(){
			var l1 = document.getElementById("l1");
			var l2 = document.getElementById("l2");
			var l3 = document.getElementById("l3");
			var l4 = document.getElementById("l4");
			function AddEvent(e){
				var id = this.getAttribute("id");
				alert(id);
			}
			l1.addEventListener("click",AddEvent,false);
			l2.addEventListener("click",AddEvent,false);
			l3.addEventListener("click",AddEvent,false);
			l4.addEventListener("click",AddEvent,false);
		})();
		```
		> 点击之后，从l4到l1向外执行----冒泡阶段
		
	* true : 捕获阶段
		
		例7.2 （*修改7.1*）
		
		```
		l1.addEventListener("click",AddEvent,true);
		l2.addEventListener("click",AddEvent,true);
		l3.addEventListener("click",AddEvent,true);
		l4.addEventListener("click",AddEvent,true);
		```
		> 点击之后，从l1向l4执行---捕获阶段。*IE，opera中无变化，因为不存在捕获阶段）*
	

	



