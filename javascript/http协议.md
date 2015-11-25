
### http协议简介

* 在Web应用中，服务器把网页传给浏览器，实际上就是把网页的HTML代码发送给浏览器，让浏览器显示出来。而浏览器和服务器之间的传输协议是HTTP，所以：

	* HTML是一种用来定义网页的文本，会HTML，就可以编写网页；

	* HTTP是在网络上传输HTML的协议，用于浏览器和服务器的通信。

* 在浏览器中打开开发者工具，netword显示浏览器和服务器的通信。

	* 例如： 
	
		```
		GET / HTTP/1.1
		```
		> `get` -- 表示一个读取请求，将从服务器获得网页数据， `/`-- 表示url的路径，url总是以`/`开头，`/`就表示首页，最后的 `HTTP/1.1`指采用的http协议版本是1.1。但是大部分服务器也支持1.0版本，主要区别在于1.1版本允许多个HTTP请求复用一个TCP连接，以加快传输速度。
		
		```
		Host: www.sina.com.cn
		```
		> 表示请求的域名是www.sina.com.cn。如果一台服务器有多个网站，服务器就需要通过Host来区分浏览器请求的是哪个网站。
		
		```
		200 OK
		```
		
		> 200表示一个成功的响应，后面的OK是说明。失败的响应有404 Not Found：网页不存在，500 Internal Server Error：服务器内部出错，等等。
		
		```
		Content-Type: text/html
		```
		
		> `Content-Type`指示响应的内容，这里是`text/html`表示HTML网页。请注意，浏览器就是依靠`Content-Type`来判断响应的内容是网页还是图片，是视频还是音乐。浏览器并不靠URL来判断响应的内容，所以，即使URL是`http://example.com/abc.jpg`，它也不一定就是图片。

		当浏览器读取到新浪首页的HTML源码后，它会解析HTML，显示页面，然后，根据HTML里面的各种链接，再发送HTTP请求给新浪服务器，拿到相应的图片、视频、Flash、JavaScript脚本、CSS等各种资源，最终显示出一个完整的页面。所以我们在Network下面能看到很多额外的HTTP请求。
		
		
### http请求

* 步骤1：浏览器首先向服务器发送HTTP请求，请求包括：

	* 方法：GET还是POST，GET仅请求资源，POST会附带用户数据；

	* 路径：/full/url/path；

	* 域名：由Host头指定：Host: www.sina.com.cn

	* 以及其他相关的Header；

	* 如果是POST，那么请求还包括一个Body，包含用户数据。


* 步骤2：服务器向浏览器返回HTTP响应，响应包括：

	* 响应代码：200表示成功，3xx表示重定向，4xx表示客户端发送的请求有错误，5xx表示服务器端处理时发生了错误；
	
	* 响应类型：由Content-Type指定；
	
* 步骤3：如果浏览器还需要继续向服务器请求其他资源，比如图片，就再次发出HTTP请求，重复步骤1、2。

### http格式

每个HTTP请求和响应都遵循相同的格式，一个HTTP包含Header和Body两部分，其中Body是可选的。

* HTTP协议是一种文本协议，所以，它的格式也非常简单。HTTP GET请求的格式：

	```
	GET /path HTTP/1.1
	Header1: Value1
	Header2: Value2
	Header3: Value3
	```	
	> 每个Header一行一个，换行符是\r\n。

* HTTP POST请求的格式：

	```
	200 OK
	Header1: Value1
	Header2: Value2
	Header3: Value3

	body data goes here...
	```



### http协议详解之url篇

* http（超文本传输协议）是一个基于请求与响应模式的、无状态的、应用层的协议，

	```
	http://host[":"port][abs_path]
	```
	> * http表示要通过http协议来定位网络资源
	
	> * host：表示合法的Internet主机域名或者IP地址；
	
	> * psrt：指定一个端口号，为空则使用缺省的端口80；
	
	> * abs_path指定请求资源的URI；如果URL中没有给出abs_path，那么当它作为请求URI时，必须以“/”的形式给出，通常这个工作浏览器自动帮我们完成。
	
### http协议详解之请求篇

http请求由三部分组成，分别是：请求行、消息报头、请求正文

* 请求格式  

	```
	Method Request-URI HTTP-Version CRLF  
	```
	> 其中 Method表示请求方法；Request-URI是一个统一资源标识符；HTTP-Version表示请求的HTTP协议版本；CRLF表示回车和换行（除了作为结尾的CRLF外，不允许出现单独的CR或LF字符）。
	
	* 请求方法
	
		* GET     请求获取Request-URI所标识的资源
		
			* GET方法：在浏览器的地址栏中输入网址的方式访问网页时，浏览器采用GET方法向服务器获取资源，eg:GET /form.html HTTP/1.1 (CRLF)
			
		* POST    在Request-URI所标识的资源后附加新的数据
		
			* POST方法要求被请求服务器接受附在请求后面的数据，常用于提交表单。
			
		* DELETE  请求服务器删除Request-URI所标识的资源
	
### http协议详解之响应篇

在接收和解释请求消息后，服务器返回一个HTTP响应消息。

HTTP响应也是由三个部分组成，分别是：状态行、消息报头、响应正文

1. 状态格式

	* 1xx：指示信息--表示请求已接收，继续处理
	* 2xx：成功--表示请求已被成功接收、理解、接受
	* 3xx：重定向--要完成请求必须进行更进一步的操作
	* 4xx：客户端错误--请求有语法错误或请求无法实现
	* 5xx：服务器端错误--服务器未能实现合法的请求
	
	常见状态代码、状态描述、说明：
	
	* 200 OK      //客户端请求成功
	* 400 Bad Request  //客户端请求有语法错误，不能被服务器所理解
	* 401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 
	* 403 Forbidden  //服务器收到请求，但是拒绝提供服务
	* 404 Not Found  //请求资源不存在，eg：输入了错误的URL
	* 500 Internal Server Error //服务器发生不可预期的错误
	* 503 Server Unavailable  //服务器当前不能处理客户端的请求，一段时间后可能恢复正常
	
---
	
	
* 参考  [HTTP协议详解](http://www.cnblogs.com/li0803/archive/2008/11/03/1324746.html)