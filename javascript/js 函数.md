### 了解函数

* **函数：** 

	函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块。
	
* **定义函数**

	```
	//方法一：
	function fn(){
		//code...
	}
	//方法二：
	var fn = function(){
		//code...
	}
	```

* **调用函数**

	* 方法一：

		```
		function fn(){
			//code...
		}
		fn();   //函数执行
		```
	
	* 方法二：
	
		```
		(function fn(){
			//code...
		})();
		```
		
	* 方法三
	
	
		```
		<button type="button" value="点我" onclick = 'fn()' />	
		```

* **带参数的函数**

* **带返回值的函数**

* **局部变量和全局变量**