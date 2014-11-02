
* **-webkit-box:** 流体布局
	
	* 浏览器支持：目前没有浏览器支持，代替属性：
	
		```
	//例：
	.wrap{
		display:box;  //必须给父元素设置此属性，此属性为内联元素。
		display:-webkit-box;
		display:-moz-box;
	}
	.wrap .one{
		-webkit-box-flex:1;  //父元素的1/3
		-moz-box-flex:1;
		box-flex:1;
	}
	.wrap .two{
		-webkit-box-flex:2;   //父元素的2/3
		-moz-box-flex:2;
		box-flex:2;
	}
	```
	* **box属性：**
	
		```
	box-orient:horizontal | inline-axis 
	//水平排列方式 ，此时如果父容器定义了高度值，其子容器的高度值设置则无效状态，所有子容器的高度等于父容器的高度值；如果父容器不设置高度值，其子容器的高度值才有效并且取最大高度值的子容器的高度。
	box-orient:vertical | block-axis
	//此时如果父容器定义了宽度值，其子容器的宽度值设置则无效状态；如果父容器不设置宽度值，其子容器的宽度值才有效并且取最大宽度值的子容器的宽度。
	box-orient:inherit
	//属性则是让子容器继承父容器的相关属性。
	```
	```
	box-direction:nomarl   //默认顺序排列
	box-direction:reverse   //倒序
	```
	``` 
	//垂直对齐方式
	box-align:start    //top对齐
	box-align:end    //bottom对齐
	box-align:center   //居中
	box-align:stretch   //拉伸对齐
	```
	```
	//水平对齐方式
	box-pack:start | end | center | justify
	```
	
* **box-sizing:** 属性允许您以特定的方式定义匹配某个区域的特定元素。

	```
//例：
div
{
	box-sizing:border-box;
	-moz-box-sizing:border-box; /* Firefox */
	-webkit-box-sizing:border-box; /* Safari */
	width:50%;
	float:left;
}
	```
	
	* 浏览器兼容性：
	
		* Internet Explorer、Opera 以及 Chrome 支持 box-sizing 属性。
		* Firefox 支持替代的 -moz-box-sizing 属性。
	
	* 语法：
	
		```
		box-sizing: content-box|border-box|inherit;
		```
		
		值          |   描述
		------------|----------------------------
		content-box | 宽度和高度分别应用到元素的内容框。内容宽 = width;
		border-box  | 为元素设定的宽度和高度决定了元素的边框盒。  内容宽 = width-padding-borderWidth
		inherit     | 从父元素继承。


* **column: 创建多个列来对文本进行布局 - 就像报纸那样！**

	```
	div
	{	
		columns:100px 3;
		-moz-columns:100px 3; /* Firefox */
		-webkit-columns:100px 3; /* Safari 和 Chrome */
	}
	```

	* column-count：num/auto;  属性规定元素应该被分隔的列数：
	
		* 浏览器支持
		
			1. Internet Explorer 10 和 Opera 支持多列属性。
			2. fierfox:  -moz-
			3. chrome和safair:  -webkit-
		
 		
 			```
 		-moz-column-count:3; 	/* Firefox */
		-webkit-column-count:3; /* Safari 和 Chrome */
		column-count:3;  //列数，宽度自适应；
 		column-count:auto;   //由其他属性决定列数，比如 "column-width"。
 		```
 		
 	* column-gap: 属性规定列之间的间隔。
 	
 		* 浏览器支持
		
			1. Internet Explorer 10 和 Opera 支持多列属性。
			2. fierfox:  -moz-
			3. chrome和safair:  -webkit-
		

 	
 	* column-span:
 	
 		```
 	h2
	{
		-webkit-column-span:all; /* Chrome */
		column-span:all;
	}
 		```
 		
 	* column-width: 
 		
 		
 		
 		
 	  属性             |    描述                     
 	------------------|-----------------------------
 	**column-count**  | 规定元素应该被分隔的列数。       
    **column-count**  | 规定元素应该被分隔的列数。       
 	**column-fill**   | 规定如何填充列。               
 	**column-span**	   | 规定属性应该跨越的列数 。 
 	**column-width**  |  规定列的宽度。
	
