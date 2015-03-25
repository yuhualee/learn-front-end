### jQuery三种事件绑定

* **target.click()**

* **target.bind():** 

	添加一个或多个事件处理程序，并规定事件发生时运行的函数。（只能给当前存在的元素绑定）

	```
	$(selector).bind({event:function, event:function, ...})
	```
	> jquery遍历所有的selector元素，并绑定事件。


* **target.live():** 

	添加一个或多个事件处理程序，并规定事件发生时运行的函数。在绑定方面它和bind相同，但是它附加的事件处理程序适用于匹配选择器的**当前及未来的元素**（比如由脚本创建的新元素）。
	
	**原因：**由于只有在事件发生的时候，live方法才会去检测绑定事件的对象是否存在，
	
	> jquery把事件绑定到document上，只要有事件触发document，就查找它是否符合绑定。


* **bind()和live()的区别：**

	* **绑定的时间：**bind()在绑定的阶段进行绑定，而live()是在事件发生的时候才去检测元素是否存在，再进行绑定，所以它可以给未来的元素进行绑定。
	
	* bind()可以绑定任何javascript事件，而live()不可以
	
	* live() 并不完全支持通过DOM遍历的方法找到的元素。取而代之的是，应当总是在一个选择器后面直接使用 .live()方法。 
	
	* 当一个元素采用live方法进行事件的绑定的时候，如果想阻止事件的传递或冒泡，就要在函数中return false,仅仅调用stopPropagation()是无法实现阻止事件的传递或者冒泡的
	
	
* **delegate():** delegate() 方法为指定的元素（*属于被选元素的子元素*）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数。使用 delegate() 方法的事件处理程序适用于**当前或未来的元素**（比如由脚本创建的新元素）。

	```
	$(selector).delegate(childSelector,event,data,function)
	```
	> 为childSelector绑定方法，但它通过**事件委托**绑定在了selector上面。



* **delegate()和live():**

	```
	$(a).live("click",fn(){});
	//相当于：
	$(document).delegate("a","click",fn(){});
	```

	* live()绑定事件的方法是：先遍历a，然后存储为jquery对象，
	
	* delegate()绑定事件的方法是：delegate方法仅需要查找并存储$(document)元素
	
* **on():**  在jquery 1.7中，全用on()来代替delegate()。

	```
	$("table").on("click","td",function(){});
	```
	
* **几种事件绑定的区别：**

	* bind()是直接绑定在元素上
	* live()则是通过冒泡的方式来绑定到元素上的。更适合列表类型的，绑定到document DOM节点上。和bind()的优势是支持动态数据。
	* delegate()则是更精确的小范围使用事件代理，性能优于.live()
	* on()则是最新的1.9版本整合了之前的三种方式的新事件绑定机制