#### 筛选

* 

#### 遍历

* **.add**

	```
	<p>这是一个p标签</p>
	```
	```
	$('p').add('<div>这是一个div</div>').addClass('box').appendTo(document.body).css('color','#f90');
	```
	> 选择匹配条件的p标签，并添加上一个div标签，给他们加入样式box,并插入到body上


* **.map** 遍历数组和类似数组的对象

	* 该函数返回：
	
		* 转换后的值，该值会被映射到最终的结果数组中
		* null或者undefined，用于移除该元素
		* 数组，会将该数组中的元素添加到最终的结果数组中
		   

	* 案例：

	```
	$.map([1,2,3,4],function(n,i){
		return n*i
	})	
	```
	> 结果：[0, 2, 6, 12]

	```
	$.map([0,1,2],function(n){
    	return n > 0 ? n+1 : null;
	})
	[2, 3]
	```
	
* **filter**

* **:contains(text)**  包含文字过滤

* **:has(selector)** 过滤选择器

* **:hidden** 过滤选择器的功能是获取全部不可见的元素，这些不可见的元素中包括type属性值为hidden的元素。`:visible`


#### 表单

* **:text** 获取单行文本框
* **:password:** 获取密码输入文本框



#### 核心

* **.makeArray** 将类数组转换成数组。







	