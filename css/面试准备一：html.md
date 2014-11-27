Date: 2014-09-20  
Title:面试准备一：HTML   
Published: true  
Type: post  
Excerpt:   

# HTML
## <!DOCTYPE>定义和用法 

* **doctype：** document type,用来说明你用的是xhtml或者html的版本，作用是以哪种规则来解析你的document文档，建立符合哪种标准的网页。

	* **作用：**
	
		1. 告诉浏览器是以何种规范来解析文档标签。浏览器有三种解析文档的模式：
		
			* **怪异模式**： 缺少doctype会触发怪异模式，比如ie不加这个标识，它会用自己的盒模型来解析 。
			* 标准模式
			* 兼容模式
			
	* **html5的头部申明：**
	
		在html4.0中，<!DOCTYPE>引用了DTD，因为它是基于SGML（标准通用标记语言），DTD规定了标记语言的规则。html5不是基于SGML,所以它不需要引入DTD，可以简写。
		
		```
		<!DOCTYPE html>
		```
		
## 语义化标签

* **什么是语义化标签？**

	* **html标签语义化**

		语义化就是用合理的html标记以及其特有的属性来格式化文档。通俗的说就是什么东西做什么事。
	
		在html中div和span标签是无意义的，一般用来布局。但是当html5的出现，大量语义化的标签代替了div和span。

	* **css命名语义化：**
	
		* 尽量使用英文单词。
		* 尽量使用“_”,"-",或者驼峰命名法。
		* 尽量不要用命两种及以上的命名规范。
		
	* **html5标签语义化**
	
		* **语义化标签：**
		
			section,article,nav,aside,header,hgroup,footer,audio,details,
		
		* **如何让ie支持html5标签：**
		
			* 方法一：引用google的html5 shiv
			
				```
				<!--[if IE]>
				<script src=”http://html5shiv.googlecode.com/svn/trunk/html5.js”></script>
				< ![endif]-->
				```
				
			* 方法二：用js创建新标签：
			
				```
				<!-- [if it IE] -->
				<script>
				;(function(){
					if(!/*@cc_on!@*/0) return;
					var eles = "abbr, article, aside, audio, canvas, datalist, details, dialog, eventsource, figure, footer, header, hgroup, mark, menu, meter, nav, output, progress, section, time, video".split(",");
					var i = eles.length;
					while(i--){
						document.createElement(e[i]);
					}
				})();
				</script>
				<![endif]-->
				```
				> 在ie中有一个鲜为人知的条件编译，@cc_on在脚本的注释内启用条件编译功能...。极力推荐在注释中使用[@cc_on](http://baike.baidu.com/view/1097041.htm?fr=aladdin) 语句。
				
			* 初始化新标签的css
			
			
				```
				/*html5*/  
				article,aside,dialog,footer,header,section,footer,nav,figure,menu{display:block}
				```
				
				


## 块级元素和行内元素，以及它们之间的转换

* **块状元素：**

	div、p、dl、ul、li、form、h1~h6、table、（html5:header、footer、nav、section、article）

* **内联元素：**

	img、input、textarea、select、object、a、abbr、em 、font、i 、kbd、label、small、span、strong 
	

	* **替换元素：** 是浏览器根据其标签的元素与属性来判断显示具体的内容。  
 
		img、input、textarea、select、object
	

	* **非替换元素：** 大多数元素都不是替换元素，它们将要显示的内容直接告诉浏览器，让其显示出来。

		a、abbr、em 、font、i 、kbd、label、small、span、strong 、
		
	> * 给替换元素添加上下margin，是有作用的，给非替换元素添加上下margin是不起作用的。
	
	> * 给替换元素添加上下padding，占位，会撑开父元素。而给非替换元素添加上下padding，有位置，添加背景色可以看到，但不会撑开父元素。
	

## 你真的了解html吗