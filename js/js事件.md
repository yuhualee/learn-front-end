### **javascript事件**

* **事件绑定：**

	* 直接在DOM结构里面绑定:   
		```
		<div onclick="fn()"></div>
		```
		
	* 在javascript里面绑定：    
		```
		div.onclick = function(){};
		```
		
	* 事件监听：   
		```
		addEventListener(div,'click',fn);
		```


* **事件流：**  

	DOM(文档对象模型)结构是一个树型结构，当一个HTML元素产生一个事件时，该事件会在元素结点与根节点之间按特定的顺序传播，路径所经过的节点都会收到该事件，这个传播过程可称为DOM事件流。事件顺序有两种类型：事件捕捉和事件冒泡。

* **事件冒泡：**从dom结构的最里层向外扩散，最终到达document。像水泡从水里浮起一样。

	* 例3.1：

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
	> 点击最里层时，四个div上的事件都会被触发，最终到达document上面。
	
	* **阻止事件冒泡：**
	
		```
		e = e || window.event;
		if(e.stopPropagation){
			e.stopPropagation();  //标准游览器阻止事件冒泡。
		}else{
			e.cancelBubble = true;   //IE浏览器。
		}
		```
		
		* 例3.2  （*修改例3.1*）
		
		```
		l4.onclick = function(e){
			e = e || window.event;
			if(e.stopPropagation){
				e.stopPropagation();  //标准游览器阻止事件冒泡。
			}else{
				e.cancelBubble = true;   //IE浏览器。
			}
			alert("l4");
		}
		```

* **事件捕获：**像石子落入水中一样。（*IE，opera浏览器中，是不存在这个阶段的*）

* **javascript事件代理：**

* **javascript事件委托：**

	事件委托就是用事件传播的机制，无论哪一个网页元素，它的click事件都会最终传到document上。这样，则只需在document上处理click事件既可。


	事件委托是冒泡的一个应用，可以减少绑定次数，同时也不用担心内部元素的改变，也不需要在内部元素改变后，重新进行绑定。


	* 例：6.1 （*个性3.2的例子*）
	
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
		
	* 例6.2 （*修改6。1中的例子*）
	
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
		
		例7.2 （*修改7.1*）
		
		```
		l1.addEventListener("click",AddEvent,true);
		l2.addEventListener("click",AddEvent,true);
		l3.addEventListener("click",AddEvent,true);
		l4.addEventListener("click",AddEvent,true);
		```
		> 点击之后，从l1向l4执行---捕获阶段。*IE，opera中无变化，因为不存在捕获阶段）*
	

	* true : 捕获阶段



