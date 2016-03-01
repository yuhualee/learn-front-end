# 前端面试题（html+css）

### 备忘 

1. CSS动画原理
2. 圣杯布局


### <!DOCTYPE>定义和用法 

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
		
* **html5的文档类型和字符集是什么**

	* html5的文档类型<!DOCTYPE html>
	
	* html5的字符集是: charset = 'utf-8'
	
* **html5的输出元素是什么**

	output - 标签定义不同类型的输出，比如脚本的输出。
	
		```
		<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
		   <input type="range" id="a" value="50">100
		   +<input type="number" id="b" value="50">
		   =<output name="x" for="a b"></output>
		</form> 
		```
		
	* for - 定义输出域相关的一个或多个元素，值为元素的id
		
	* form - 定义输入字段所属的一个或多个表单，form_id
	
	* name - -定义对象的唯一名称, name

	
* **html5应用程序缓存和浏览器缓存**

	* html5应用程序缓存：这意味着web应用可进行缓存，并可在没有因特网连接时进行访问。
	
		* 优势
		
			1. 离线浏览 - 用户可在应用离线时使用它们
			2. 速度 - 已缓存资源加载更快
			3. 减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。
			
		* 实现缓存：
		
			如需启用应用程序缓存，请在文档的<html>标签中包含mainfest属性，mainfest文件的建议的文件扩展名是：'.appcahe'
			
	* 游览器缓存：
	* 

		
### 语义化标签

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
				
				


### 块级元素和行内元素，以及它们之间的转换

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

### DOCTYPE 网页文档模型

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

#### 1. 语义化HTML


1. 请解释一下什么是语义化的HTML

	根据内容的结构，选择合适的标签，便于开发者阅读和写出更优雅的代码，同时更利于seo优化，有于搜索引擎。
	
*  语义化的好处：
	
	1. 有利于搜索引擎；
	
	* 良好的用户体验；
		
	* 利于团队合作中可维护性和可扩展性；
		
	* 有利于盲人阅读器。　
	
* 写html代码时应注意什么？

	a. 尽量少使用无意义的标签，如div和span
	
	* 不要使用纯样式标签，如：b、font、u等，可以用css设置。
	
	* 使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。表头和一般单元格要区分开，表头用th，单元格用td；
	
	* html5更语义化的标签




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
	
* css选择器的优先级是怎样定义的

	基本原则：一般而言，选择器级别越特殊，它的优先级越高。也就是选择器指向的越准确，它的优先级越高。
	
	复杂的计算方法：
	
	* 用1表示派生选择器的优先级
	* 用10表示类选择器的优先级
	* 用100表示id选择器的优先级
	
		
* position的属性是什么含义，都有哪些值，分别有什么含义？

* display:none和visibility:hidden的区别？

	* display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，
就当他从来不存在。

	* visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。
	
* 介绍一下css的盒子模型（**可引申介绍一下css3新属性box-sizing**）

	* 盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)
	
	* 有两种， IE 盒子模型、标准 W3C 盒子模型；IE的content部分包含了 border 和 pading;


* 兼容性

* 浮动产生的兼容性问题，以及清除浮动的方法

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
	

* **IE盒子模型和w3c盒子模型**

	
	![盒子模型](http://yspe2371e4aa7697989.yunshipei.cn/dHlwZT1mdyZzaXplPTY0MCZzcmM9YUhSMGNDVXpRU1V5UmlVeVJuZDNkeTVqYjIxemFHRnljQzVqYjIwbE1rWlhjbWwwWVdKc1pTVXlSbEpsYzI5MWNtTmxKVEpHWDFKaGJtUnZiVjhsTWtZeU1ERXdMVEEyTFRFeUpUSkdjREV1WjJsbQ== "盒子模型")

	* **IE6盒子模型：**
	
		包含内容、padding、border在内。
	
		```
		width = content + padding + border
		```
		
		* **IE盒模型总结：**
		
			* IE6 IE7 IE8 IE9，不声明doctype，触发Quirks怪异模式，采用IE盒模型展现。   
		
			* 但是当声明doctype时，它会按符合w3c的盒子模型来解析。
		
		* **border区背景色是否填充**
			
			* 非IE浏览器下，标准模式渲染，div的背景颜色充满了padding和border。border透明时，可发现border区域填充了背景色；
			
			* IE6 IE7 IE8 IE9在Quirks怪异模式下，border区域都不会填充背景色；
		
	* **w3c盒子模型：**
	
		只包含width，padding、border、margin被排队在外。
		
		```
		width = content
		```
		
		* **W3C盒模型总结：**
		
			* W3C盒模型Width = contentWidth + pdding + margin + border；

			* IE6 IE7 IE8 IE9，声明doctype，触发标准模式，采用W3C盒模型展现。非IE浏览器采用标准模式渲染；
			
		* **border区背景色是否填充**

			* 非IE浏览器下，div的背景颜色充满了padding和border。border透明时，可发现border区域填充了背景色。

			* IE8和IE9在标准模式下，和非IE浏览器渲染一致，border区域填充背景色；
		
			* IE6 IE7标准模式下，border区域不填充背景色；
		
	* **事实上ie6的盒子模型更合理，在我们布局的时候，我们不会管里面的内容占多少，有什么，我们只会考虑整个物理尺寸。w3c为了纠正之个问题，在css3里面新添加了属性box-sizing。**	

	*  **box-sizing 改变盒子模型**



### 浏览器加载和渲染

1. **css浏览器的渲染**

	![dom渲染](http://pic2.zhimg.com/b2b7c07bd7f5af231cdeaa0c3804a686_r.jpg)

	* **从右向左解析**

		如果正向解析，例如「div div p em」，我们首先就要检查当前元素到 html 的整条路径，找到最上层的 div，再往下找，如果遇到不匹配就必须回到最上层那个 div，往下再去匹配选择器中的第一个 div，回溯若干次才能确定匹配与否，效率很低。


* **浏览器加载和渲染html顺序**

	1. IE下载的顺序是从上到下，渲染的顺序也是从上到下，下载和渲染是同时进行的。
	
	* 在渲染到页面的某一部分时，其上面的所有部分都已经下载完成（并不是说所有相关联的元素都已经下载完）

	* 如果遇到语义解释性的标签嵌入文件（JS脚本，CSS样式），那么此时IE的下载过程会启用单独连接进行下载。
	
	* 并且在下载后进行解析，解析过程中，停止页面所有往下元素的下载。阻塞加载
	
	* 样式表在下载完成后，将和以前下载的所有样式表一起进行解析，解析完成后，将对此前所有元素（含以前已经渲染的）重新进行渲染。
	
	* JS、CSS中如有重定义，后定义函数将覆盖前定义函数

* **JS的加载**

	1. 不能并行下载和解析（阻塞下载）

	* 当引用了JS的时候，浏览器发送1个js request就会一直等待该request的返回。因为浏览器需要1个稳定的DOM树结构，而JS中很有可能有代码直接改变了DOM树结构，比如使用 document.write 或 appendChild,甚至是直接使用的location.href进行跳转，浏览器为了防止出现JS修改DOM树，需要重新构建DOM树的情况，所以 就会阻塞其他的下载和呈现。
	
* **HTML页面加载和解析流程**

	1. 用户输入网址（假设是个html页面，并且是第一次访问），浏览器向服务器发出请求，服务器返回html文件；
	
	* 浏览器开始载入html代码，发现＜head＞标签内有一个＜link＞标签引用外部CSS文件；
	
	* 浏览器又发出CSS文件的请求，服务器返回这个CSS文件；(使用外链，并行下载）
	
	* 浏览器继续载入html中＜body＞部分的代码，并且CSS文件已经拿到手了，可以开始渲染页面了；
	
	* 浏览器在代码中发现一个＜img＞标签引用了一张图片，向服务器发出请求。此时浏览器不会等到图片下载完，而是继续渲染后面的代码；
	
	* 服务器返回图片文件，由于图片占用了一定面积，影响了后面段落的排布，因此浏览器需要回过头来重新渲染这部分代码；(所以我们要写定图片的大小，防止重新渲染)
	
	* 浏览器发现了一个包含一行Javascript代码的＜script＞标签，赶快运行它；
	
	* Javascript脚本执行了这条语句，它命令浏览器隐藏掉代码中的某个＜div＞ （style.display=”none”）。突然少了这么一个元素，浏览器不得不重新渲染这部分代码；
	
	* 终于等到了＜/html＞的到来，浏览器泪流满面……
	
	* 等等，还没完，用户点了一下界面中的“换肤”按钮，Javascript让浏览器换了一下＜link＞标签的CSS路径；
	
	* 浏览器召集了在座的各位＜div＞＜span＞＜ul＞＜li＞们，“大伙儿收拾收拾行李，咱得重新来过……”，浏览器向服务器请求了新的CSS文件，重新渲染页面。

	
	[游览器渲染](http://www.jianshu.com/p/e141d1543143)


### 兼容性


### 移动端









### 网页性能优化

1. 请说出三种减低页面加载时间的方法

	1. 减少http请求次数
	
		a. 合并文件，比如css，js
		b. css sprite
		
	* 减少DNS查找次数: DNS查询和解析域名也是消耗时间的，所以要减少对外部JavaScript、CSS、图片等资源的引用，不同域名的使用越少越好


	a. 书写html时结构语义化；
	

	
	* css,js数量及大小的优化： 压缩css、js文件； 合并js、css文件，减少http请求

	* 图片的处理
	
		
		2. 选择合适的图片格式
		
		3. base64
		
		4. 字体图片icon font  
		
		5. 指定图像尺寸
	

	* 减少dom操作，尽可能用变量替代不必要的dom操作
	
	* 使用CDN托管
	
		`内容分发网络其基本思路是尽可能避开互联网上有可能影响数据传输速度和稳定性的瓶颈和环节，使内容传输的更快、更稳定。通过在网络各处放置节点服务器所构成的在现有的互联网基础之上的一层智能虚拟网络，CDN系统能够实时地根据网络流量和各节点的连接、负载状况以及到用户的距离和响应时间等综合信息将用户的请求重新导向离用户最近的服务节点上。`
	
	* 缓存的使用
	
	* 避免坏请求，避免空的图像src
	
	* 避免重定向
	
	* 推迟加载内容
	
	* 预加载
	
	
2. 请说出三种减少页面加载时间的方法

	* 优化图片 
	* 图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方） 
	* 优化CSS（压缩合并css，如 margin-top, margin-left...) 
	* 网址后加斜杠（如www.campr.com/目录，会判断这个目录是什么文件类型，或者是目录。） 
	* 标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。 当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了） 
	* 减少http请求（合并文件，合并图片）
	
### web前端：可用性，可访问性，可维护性

1. 可用性：产品是否容易上手，用户能否完成任务，效率如何，以及这过程中用户的主观感受可好，是从用户的角度来看产品的质量。可用性好意味着产品质量高，是企业的核心竞争力。

* 可访问性：一是当系统出现问题时，快速定位并解决问题的成本，成本低则可维护性好。二是代码是否容易被人理解，是否容易修改和增强功能。可维护性和可复用性、可扩展性等有交叉的地方。构建可维护性好的代码，对企业的长期发展非常重要。

* 可维护性：出现问题，可快速定位；团队协作，维护成本；可复用、可扩展性。