

####  **关于DTD说明**

1. 页面具有DTD，或者说指定了DOCTYPE时，使用 `document.documentElement`
2. 页面不具有DTD,或者没有指定DOCTYPE时，使用`document.body`
	
为了兼容，不管有没有DTD，可以使用如下代码：
	
	
```
	 
```


1. clientWidth/clientHeight: 可见内容区域，包含padding
2. offsetWidth/offsetHeight:  包含边线的内容区域
3. scrollWidth/scrollHeight:  全文p宽高
4. clientLeft/clientTop: border的宽度
5. offsetTop/offsetLeft: 距离最近的父元素的距离，从元素的padding开始，不包含border。
6. scrollTop/scrollLeft: 


* 网页可见区域宽：  ```document.body.clientWidth```