Date: 2014-08-25  
Title:   
Published: true  
Type: post  
Excerpt: 
#DOM


http://www.cnblogs.com/kissdodog/archive/2012/12/25/2833213.html
  
## document对象

* **获取元素**

	* document.getElementById(); 获取ID
	* document.getElementsByClassName();
	* document.getElementsByTagName();  获取标签名
	* document.getElementsByName();   获取name名，一般用于获取一组表单  
	* querySelector() 返回第一个匹配的元素
	* querySelectorAll()  返回所有匹配的元素
	
* **获取内容**

	* innerText  文本
	* innerHTML  包含文本和html元素


* **遍历**

	* **遍历节点**
	
		* parentNode() 父节点
		* **childNodes()** 所有子节点,它返回指定元素的子元素集合，包括HTML节点，所有属性，文本。
		* firstChild()  第一个子节点
		* lastChild()  最后一个子节点
		* nextSibling()  弟弟节点
		* previousSibling()  哥哥节点
	

	* **nodeType：**节点的类型    
	
		* 9代表Document节点
		* 1代表Element节点
		* 3代表Text节点
		* 8代表Comment节点
		* 11代表DocumentFragment节点
		
	* **nodeVlue：**    Text节点或Comment节点的文本内容
	* **nodeName：**    元素的标签名(如P,SPAN,#text(文本节点),DIV)，以大写形式表示


* **遍历元素树：**

	* **children:** 返回所有子元素，浏览器兼容性不好。
	* firstElementChild  第一个子元素节点
	* lastElementChild  最后一个子元素节点
	* nextElementSibling  下一个子元素节点
	* previousElementSibling  上一个子元素节点
	* childElementCount  子元素节点数

* **创建**

	* document.createElement() 创建元素
	* document.createNodeText()  创建文本节点


* **插入**

	* ele.appendChild(newEle);  添加子节点，添加在最后面
	* insertBefore(newEle, oldEle);  插入到指定元素之前。
	
* **删除和替换**
	
	* **removeChild():**  直接父元素调用，删除直接子元素
	* **replaceChild(newEle,oldEle):**  替换节点
	
* **复制节点**

	* **cloneNode()**

	
	
	* ele.attributes;   返回指定节点的属性集合，有length，可遍历
	* ele.childNodes;   返回节点的子节点集合
	* ele.className;   返回元素的样式名
	* ele.clientHeight;  返回元素的可见高度，它的高度=heigh+padding，不包含border。
 

## attribute



