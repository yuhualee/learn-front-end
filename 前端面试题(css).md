# 前端面试题（html+css）

### DOCTYPE

1. 文档类型的作用是什么，你知道多少种文档类型

	* 该标签可声明三种 DTD 类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。
	* HTML 4.01 规定了三种文档类型：Strict、Transitional 以及 Frameset。
	* XHTML 1.0 规定了三种 XML 文档类型：Strict、Transitional 以及 Frameset。
	* Standards （标准）模式（也就是严格呈现模式）用于呈现遵循最新标准的网页，而 Quirks（包容）模式（也就是松散呈现模式或者兼容模式）用于呈现为传统浏览器而设计的网页。
	

2. 浏览器标准模式和怪异模式之间的区别是什么

	盒模型解释不同
	
3. 每个html文件里面开头都有个很重要的东西，Doctype，知道这是干什么的吗

	<!DOCTYPE>声明位于文档中最前面的位置，处于<html>标签之前，此标签可告知浏览器文档使用哪种HTML或XHTML规范。
	重点：告诉浏览器按照何种规范解析页面。
	
### HTML标签

1. 请解释一下什么是语义化的HTML

* html改错

	```
	<div>
		<ol>
			<form method="get" action="xxx.aspx">
				<li>用户名：<input id="input1" type="text" /></li>
				<li>密码：<input id="input1" type="text" /></li>
				<li><input type="submit" value="登陆" /></li>
			</form>
		</ol>
	</div>
	```
	> * id重复
	* post表单需要name属性在服务器获取
	* 密码的类型应该是password
	* 表单方法应该是post
	* form位置应该错了吧
	* 不应该用ol，应该用ul

	
* div+css布局和table布局有何不同？各自的优缺点？为何现在还有table？




### css
	
1. css选择器有哪些

	* 派生选择器，用html标签申明
	* ID选择器
	* 类选择器
	* 属性选择器
	* 后代选择器（利用空格间隔，如.class a{}）
	* 群组选择器（利用逗号间隔，比如p,div,a{}）
	
2. css选择器的优先级是怎样定义的

	基本原则：一般而言，选择器级别越特殊，它的优先级越高。也就是选择器指向的越准确，它的优先级越高。
	
	复杂的计算方法：
	
	* 用1表示派生选择器的优先级
	* 用10表示类选择器的优先级
	* 用100表示id选择器的优先级
	
		
3. position的属性是什么含义，都有哪些值，分别有什么含义？

4. display:none和visibility:hidden的区别？

	* display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，
就当他从来不存在。

	* visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。
	
5. 介绍一下css的盒子模型（**可引申介绍一下css3新属性box-sizing**）

	* 盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)
	
	* 有两种， IE 盒子模型、标准 W3C 盒子模型；IE的content部分包含了 border 和 pading;


6. 兼容性

7. 浮动产生的兼容性问题，以及清除浮动的方法

* 如何让一段文本中所有的英文单词的首字母大写

* 请缩写以下代码

	```
	.box{
		background-position: 10px 20px;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-color: red;
		background-image: url(box.png);
	}
	```
	
* 

* 

















### 网页性能优化

1. 请说出三种减低页面加载时间的方法

	* 压缩css、js文件
	* 合并js、css文件，减少http请求
	* 外部js、css文件放在最底部
	* 减少dom操作，尽可能用变量替代不必要的dom操作
	* css sprite
	* 使用CDN托管
	* 缓存的使用
	
	
2. 请说出三种减少页面加载时间的方法

	* 优化图片 
	* 图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方） 
	* 优化CSS（压缩合并css，如 margin-top, margin-left...) 
	* 网址后加斜杠（如www.campr.com/目录，会判断这个目录是什么文件类型，或者是目录。） 
	* 标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。 当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了） 
	* 减少http请求（合并文件，合并图片）