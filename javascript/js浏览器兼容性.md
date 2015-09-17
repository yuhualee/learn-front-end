http://www.cnblogs.com/qiuyueguangxuan/p/3994819.html


* **document.documentElement和document.body的区别：**

	如果页面中存在DTD，则用document.documentElement，如果没有，则需要用document.body
	
	> documentElement是整个节点树的根节点root，即html标签；当没有DTD声明时，则以body标签为起始节点，即document.body，不过chroom不认document.documentElement.scrollTop。
	
	```
	document.documentElement.scrollTop || document.body.scrollTop
	```
	
		