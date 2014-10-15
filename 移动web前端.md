Date: 2014-09-14  
Title:移动web前端   
Published: true  
Type: post  
Excerpt:   

参考：

# 移动端web前端入门

### 1. webkit内核

* 1.1、首先我们来看看webkit内核中的一些私有的meta标签，这些meta标签在开发webapp时起到非常重要的作用
	
	```
<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0;" name="viewport" />
<meta content="yes" name="apple-mobile-web-app-capable" />
<meta content="black" name="apple-mobile-web-app-status-bar-style" />
<meta content="telephone=no" name="format-detection" />
```

	* 第一个meta标签表示：强制让文档的宽度与设备的宽度保持1:1，并且文档最大的宽度比例是1.0，且不允许用户点击屏幕放大浏览；
	
	* 第二个meta标签是iphone设备中的safari私有meta标签，它表示：允许全屏模式浏览；
	
	* 第三个meta标签也是iphone的私有标签，它指定的iphone中safari顶端的状态条的样式；
	
	* 第四个meta标签表示：告诉设备忽略将页面中的数字识别为电话号码；
	
	* **user-scalable**： 用户是否可以手动缩放，是实现position:fixed的关键

### 2.HTML5标签的应用

* **2.1 html5语义化标签**  header, nav, article, section, aside, footer, time, canvas, audio, video, source
  
	* **section:**独立的一个区块，比如：页眉、页脚、章节，通常由内容和标题组成。
	    
	* **article:**可以理解为特殊的section，独立的，完整的内容区块。比如：一条评论，一篇文章，一篇帖子。   
	* **nav:**用于放页面上链接的团体   
	* **aside:**页面主体内容的辅助区域，可有可无。  
	* **header:**标签定义文档的页眉，通常是一些引导和导航信息，不局限于头部。  
	* **hgrounp:**放置标题元素（h1-h6）进行组合.   
	* **footer:**页面或section的底部信息。  

	> **参考：**  
	[html5语义化标签](http://www.rainleaves.com/html/1338.html)   
	[html5布局](http://www.rainleaves.com/html/1701.html);

* **2.2表单**

* **2.3属性**

* **2.4新功能**

###  **3.移动端css**

* **3.1 放弃的css属性**

	* 3.1.1 放弃float。可作用display:inline-block或css3属性来代替。  

* **3.2 css3的使用**

	* **background-size**

* **3.3 css差异**

	* position:fixed
	
	* overflow:scroll
	
		```
		{
			-webkit-overflow-scrolling:touch;
			overflow:auto;
		} 
	```



###  **4. 自适应布局**

	为适应不同尺寸的屏幕，建立不要把容器的宽度定死，可以用百分比来定宽。并且不再像pc端那样，全用float来布局，因为float会破坏文档流。而且，由于不再考虑兼容性问题，css3为我们提供了更强大方法来解决布局的问题：  
 
 		**方法一：** webkit-box
 	
 		
 		
 	
 		**方法二：** box-flex
 	
 		**方法三：** 
 		
 		1. column-count：num/auto;
 		
 			```
 		column-count:3;  //列数，宽度自适应；
 		column-count:auto;   //由其他属性决定列数，比如 "column-width"。
 		```
 		
 		2. column-gap:
 		
 		3. column-rule:
	

###  **5. 移动端性能优化**

		1. 图片进行压缩，大图换成小图。  
	2. 数据离线化，可以全用html5的localStorage。
	3. 图片使用css sprites或data uri
	4. 尽量全用css3代替图片
	5. 使用css3动画代替js动画
	6. 保证html结构简洁，降低层级数。

###  **6.基础样式**

* **字体设置：**建议使用无衬字体，
     
	```
body {   
    font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif;   
}
```

	> 1. 英文字体设置为Helvetica，ios中使用，
	> 2. 中文字体使用：STHeiTi华文黑体，
	> 3. sans-serif：宋体，最后以无衬线字体结尾，保证在不同的设备上都会显示。
   
	```
a, img {
    -webkit-touch-callout: none; /* 禁止长按链接与图片弹出菜单 */
}
html, body {
    -webkit-user-select: none;   /* 禁止选中文本（如无文本选中需求，此为必选项） */
    user-select: none;
}
```
* **Media query**

	* 在css中使用：
	
		```
		```

	* **注意：**在link中使用（注意：即使不符合条件也会加载文件）
	
		```
	<link rel="stylesheet" media="screen and (max-width: 600px)" href="small.css" />
	```
	
	* 多个media queries
	
		```
		```
		
	* 针对高清视网膜屏
	
		```
		<link rel="stylesheet" media="only screen and (-webkit-min-device-pixel-ratio: 2)" type="text/css" href=“test.css" />
		```
		
	* 设备橫竖状态
	
		```
		<link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css"> 
		<link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css">
		```
		
去掉点击链接和文本框对象的半透明覆盖层(iOS)或者虚框(Android):
-webkit-tap-highlight-color:rgba(0,0,0,0); //慎重使用，可能会给Android表单控件带来巨大麻烦
禁用长按页面时的弹出菜单(iOS下有效):
-webkit-touch-callout:none;
禁止文字自动调整大小(默认情况下旋转设备的时候文字大小会发生变化):
-webkit-text-size-adjust: none;
禁止页面文字选择:
-webkit-user-select: none;
局部滚动(仅iOS 5以上支持):
-webkit-overflow-scrolling:touch;
转变盒模型(width定义变为包含padding border-width,不含margin):
-webkit-box-sizing: border-box;
消除输入框和按钮的原生外观，在iOS上加上这个属性才能给按钮和输入框自定义样式:
-webkit-appearance: none;
	
### 7.移动端javascript

* **click事件**

	一系列事件的触发顺序
  touchstart
  touchmove (可能没有)
  touchend
  mouseover
  mousemove
  click
  
 * **ios阻止默认的click事件**
 
 需要注意： (1) 只是iOS，其他平台不必
(2) 在touchend时就看手指移动情况来决定该阻止click或者是取消touch事件
(3) 只有event类型为click时才有必要阻止
在touchend的时候与touchstart时比较时间、位置，以区别是否要执行“按下”的操作。
Zepto比较好的解释了这个“按下”事件，由一系列的touch  事件封装成一个”tap”事件。

github [https://github.com/madrobby/zepto/blob/master/src/touch.js
]


### **8. 移动端调度**