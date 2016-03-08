http://www.cnblogs.com/qiuyueguangxuan/p/3994819.html


* **document.documentElement和document.body的区别：**

	如果页面中存在DTD，则用document.documentElement，如果没有，则需要用document.body
	
	> documentElement是整个节点树的根节点root，即html标签；当没有DTD声明时，则以body标签为起始节点，即document.body，不过chroom不认document.documentElement.scrollTop。
	
	```
	var scrollTop = window.payeYOffset  //用于FF
					||	document.documentElement.scrollTop 
					|| document.body.scrollTop
					||0;
	```
	
	
* 常用

	```
	网页可见区域宽： document.body.clientWidth;   实际内容的宽度，不包含border
	网页可见区域宽： document.body.offsetWidth;   实际包含border的宽度
	网页正文全文宽： document.body.scrollWidth;   正文实际宽度，不包含border，但包含滚动条盖住的那一部分
	网页被卷去的高： document.documentElement.scrollTop || document.body.scrollTop;
	```

		