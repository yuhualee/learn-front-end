Date: 2014-09-10  
Title: css兼容性  
Published: true  
Type: post  
Excerpt: 

  
* **ie6下实现相对于窗口位置固定的元素实现无抖动效果：**

	当你想在页面的某个区域始终存在（浮动）一个网页元素，比如一个DIV，你希望它能始终浮动在窗口的某个位置（比如页面两侧）。

	在IE7以上的浏览器以及标准浏览器，都支持一个属性 position:fixed ，可以很简单地实现想要的效果，而且当窗口滚动时，该元素的滚动也会很平滑。。。但是在IE6及以下的版本浏览器下，并不支持该属性，所以只好使用position:absolute来代替实现，但新问题出现，你会发现，当滚动窗口时，该元素会出现抖动的现象，看起来就很不舒服，为了去掉这个抖动的BUG，为了实现平滑滚动，就有了以下代码：

	
	```
*html{
	_background-image:url(about:blank);
	_background-attachment:fixed;
}
```

* **css实现背景半透明，而文字不透明**

	```
	div{
		background-color:rgba(0,0,0,0.5)!important;
		background:#000;
		filter:alpha(opacity=50);
	}
	div p{
		position:relative;
	}
	```

## haslayout

* position: absolute 
* float: left|right 
* display: inline-block  
* width: 除 “auto” 外的任意值 
* height: 除 “auto” 外的任意值 （例如很多人闭合浮动会用到 height: 1%  ） 
* zoom: 除 “normal” 外的任意值 


http://www.iyunlu.com/view/css-xhtml/55.html


position

background

z-index

display 盒子模型

图片垂直居中，多种方法：

http://www.cnblogs.com/cnliu/archive/2012/06/20/image-
center.html

清除浮动：多种方法

http://www.iyunlu.com/view/css-xhtml/55.html