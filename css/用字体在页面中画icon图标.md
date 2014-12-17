# icon font

## 如何把你的图标转换成web字体

1. **创建图标：**  使用能创建矢量图标的程序，可以输出svg格式， 需要注意两点，一是纯色图标，二是导出svg格式。

2. **导入到icoMoon：**  打开 [icoMoon app](https://icomoon.io/app/#/select) 导入上面创建的svg图标，点击**import icon**按钮，上传你的图标。

3. 


---

## 在网页中使用icon font

* 见[icomoon]()，把字体放在fonts文件夹中，在样式文件中引入：
	
	```
	@font-face{
		font-family: "imooc-icon";
		src:url("fonts/icomoon.eot");  /*ie9 标签浏览器*/
		src:url("fonts/icomoon.eot?#iefix") format("embedded-opentype")  //ie6-ie8
		, url("fonts/icomoon.svg") format("svg")   /* Legacy iOS */
		, url("fonts/icomoon.ttf") format("truetype")  /* Safari, Android, iOS */
		, url("fonts/icomoon.woff") format("woff");   /* Modern Browsers */
	}	
	```
	
	* **@font-face**: 能够加载服务器端的字体文件，让客户端显示客户端所没有安装的字体。
	
	* **font-family**: 设置文本的字体名，在如下的font-family里面会引用，和普通字体一样。
	
	* **src**: 设置引入字体的路径，
	
	* **format**: 此值指的是你自定义的字体的格式，主要用来帮助浏览器识别，其值主要有以下几种类型：
		* **.ttf字体** ：truetype
			【IE9+,Firefox3.5+,Chrome4+,Safari3+,Opera10+,iOS Mobile Safari4.2+】
			
		* **woff字体** ：woff     
			【IE9+,Firefox3.5+,Chrome6+,Safari3.6+,Opera11.1+】
			
		* **eot字体** ：ie专用字体    
			支持这种字体的浏览器有【IE4+】
			
		* **svg** ：.svg字体是基于SVG字体渲染的一种格式    
			支持这种字体的浏览器有【Chrome4+,Safari3.1+,Opera10.0+,iOS Mobile Safari3.2+】。
			
		
		
	* **PC端应用常见问题：**
	
		* 字体图标在safair或chrome浏览器下被加粗？
		
			以上现象是由于字体图标存在半个像素的锯齿，在浏览器渲染的时候直接显示一个像素了，导致在有背景下的图标显示感觉加粗；所以在应用字体图标的时候需要对图标样式进行抗锯齿处理，CSS代码设置如下：
			
			```
			-webkit-font-smoothing: antialiased;   /*icon font字体图标在chrome抗锯齿*/
			-moz-osx-font-smoothing:grayscale;  /*icon font字体图标在火狐*/
			```
			
		* 字体图标在IE7浏览器显示中图标右侧出现小方框现象；
		
			出现以上现象可以对引用字体图标的非块标签进行以下CSS定义:
			
			```
			display: block;
			```
			
		* 字体图标在pc端的chrome浏览器下出现严重的锯齿；
		
			出现以上现象可以对字体图标的边缘进行模糊；（只支持webkit内核浏览器,参数数值不宜设置得很大，这会带来图标加粗的问题）
			
			```
			-webkit-text-stroke-width: 0.2px;
			```

* **参考**

	[icoMoon](https://icomoon.io)    
	[iconFont](http://www.iconfont.cn)  
	[用字体在页面中画icon图标](http://flowerboys.cn/font/tutorial.html)