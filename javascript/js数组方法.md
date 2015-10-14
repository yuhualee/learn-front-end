### javascript数组操作

#### 一、数组的操作

* **数组的创建：**

	```
	var arr = [];
	var arr = new Array();
	var arr = new Array([size]);   //创建并指定长度
	var arr = new Array([ele1,ele2,ele3...]);  //创建并赋值
	```
	
* **数组的访问：**

	```
	var getArr = arr[1];    //获取
	arr[1] = 'new value';   //赋值
	```

* **数组的添加：**

	* arr.push([item1,item2,item3...]);   //添加到最后
	* arr.unshift([item1,item2,item3...])   //添加到开头
	* arr.splice(insertPos,0,[item1,item2,item3...]);   //添加到指定位置
	
* **数组元素的删除：**

	* arr.pop();  //删除最后一个
	* arr.shift();   //删除第一个
	* arr.splice(deletePos，deleteCount);    //删除指定位置的，指定个数；
	* arr.slice(start,[end]);    
	
* **数组的合并：**

	* arr.concat([item1,item2,item3...]);

* **数组的拷贝：**

	* array.slice(0); //返回数组的拷贝数组，注意是一个新的数组，不是指向
	* array.concat(); //返回数组的拷贝数组，注意是一个新的数组，不是指向
	
* **数组的排序：**

	* array.reverse(); //反转元素（最前的排到最后、最后的排到最前），返回数组地址
	* array.sort(); //对数组元素排序，返回数组地址

* **数组的字符串化：**

	* array.join(separator); //返回字符串，这个字符串将数组的每一个元素值连接在一起，中间用 separator 隔开。
	* toLocaleString 、toString 、valueOf：可以看作是join的特殊用法，不常用



#### 二、数组的方法

* **splice():** 方法向/从数组中添加/删除/替换项目，然后**返回被删除**的项目，**原数组改变**。
	
	```
	Array.splice(index,howmany,item...itemx);
	```
	
	> splice() 方法可删除从 index 处开始的howmany(零个或多个)元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。

	```
	var a = [2,"a","b","c",64,33];
	b = a.splice(2,1,["d","e"]);
	alert(a);  //[2,"a","d","e","c",64,33]  原数组改变
	alert(b);  // b  返回被删除的项目
	c = a.splice(2,0,"f","h");
	alert(a);  // 2,a,f,h,d,e,c,64,33
	```
	
	> 1. 返回被删除的项目。
	> 2. 原数组会改变。
	> 3. 如果howmany为0，则为添加。添加时，没有返回值。
	> 4. **第三个参数，可以是各个参数的列表，也可以以数组的方式传入**
	
* **slice():** 可从已有的数组中返回选定的元素。**返回一个新数组**，包括start，不包含end。**不修改原数组**。它的作用是复制、截取新数组。

	```
	Array.slice(start,end);
	```
	
	> start:规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。   
	> end: 规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。
	
```
我以前一直分不清，splice和slice，因为老师讲的时候总是强调说，你们要区分它们俩，好像俩差不多似的，反而导致我们分不清，但你真正认清它们俩的关系的时候，才发现，原来它们根本就不一样。

1. splice是向数组中添加、删除、替换
2. slice是从数组中复制、截取
3. 从1，2两点中可以看出，它们的目的不一样，一个是为了改变原数组，一个是为了复制新数组。
```
	
* **concat():** 用于连续两个或多个数组，该方法不会改变原有的数组，会返回一个被连接数组的复本。

	```
	Array.concat(arry1,arry2...arryx);
	```
	
	> 可以是具体的值，也可以是数组，可以是一个
	
	```
	var a = [2,"a","b","c",64,33];
	b = ["lyh","hxf"];
	alert(a.concat(b,"hmh","hch",4));
	```
	
* **join():** 把数组中的所有元素放入一个字符串，通过指定的分隔符进行分隔。

	```
Array.join(separator)
```
> separator：分隔符，如果省略，则为逗号。    
> 返回一个字符串   
> 如果为空字符，则直接连接。

	```
	var a = ["I","love","you"];
	console.log(a.join(""));   //Iloveyou
	console.log(a.join(" "));  //I love you
	console.log(a.join());  //I,love,you
	```
* **pop():** 删除并返回数组的最后一个**元素**，**原数组改变**。

	```
	var a = ["I","love","you"];
	alert(a.pop());   //you
	alert(a);   //["I","love"];
	```	

* **shift():** 删除并返回数组的第一个**元素**，**原数组改变**。

	```
	var a = ["I","love","you"];
	alert(a.shift());   //I
	alert(a);   //["love","you"];
	```
	
* **push():** 向数组的末尾添加一个或多个元素，**原数组改变**，并**返回新数组的长度**。   
**unshift():** 向数组的开头添加一个或多个元素，**原数组改变**，并**返回新数组的长度**。 

	```
	var a = ["I","love","you"];
	var b = a.push("!");
	alert(b);  //4
	alert(a);  //["I","love","you","!"]
	```	
	
	> 传入的参数可以是一个数组，但数组是当成一个数来传入的，当作原数组的一项，所以长度只能增加1。
	
		```
		var a = ["I","love","you"];
		var c = ["!","you","?"]
		var b = a.push(c);
		alert(b);
		alert(c.length);
		alert(a[3]);
		```

* **reverse():** 颠倒数组，更改原数组。

	```
	var a = ["I","love","you"];
	alert(a.reverse());
	alert(a);
```

* **sort():** 对原数组进行排序，按字符编码。**原数组改变**。因为它只对第一位进行排序，你可通过传入比较函数对它进行排序。

	```
	//例1：直接排序
	var a = [12,44,6,77,47,9];
	alert(a.sort());   //12,44,47,6,77,9
	```
	```
	//排序函数
	var a = [12,44,6,77,47,9];
	function sortNumber(a,b){
    	return a - b;
	}
	alert(a.sort(sortNumber));
	//6,9,12,44,47,77
	```
	
* **toString():** 把数组换成字符串，并返回结果。数组之间用逗号隔开。

#### 三、数组属性

* **length属性：**

* **prototype属性：**  返回对象类型原型的引用，prototype属性是object共有的。

	* 例：返回数组中的最大值：
	
		```
		Array.prototype.max = function(){
		  return this.sort(function(a,b){
		    return b - a;
		  })[0];
		};
		[1,2,3,4,10,5].max();
		```
		
* **construtor属性：** 表示创建对象的函数

	object.constructor // object 是对象或函数的名称。
