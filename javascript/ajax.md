Date: 2014-09-20  
Title: ajax
Published: true  
Type: post  
Excerpt:   

# ajax

* **ajax:** Asynchronous Javascript and XML 异步javascript和XML

	* **什么是ajax**
	
		* 是在不重新加载页面的情况下，与服务器交换数据并更新部分网页的技术。
	
		* 用javascript异步形式去操作XML
	
		* 数据交互
		
	* **ajax的作用：** 
	
		通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

	
	* **创建ajax实例：**
	
		* **第一步：创建一个ajax对象** 
			
			```
			var xhr = null;
			try{ //代码尝试执行这个块中的内容，如果有错误，则会执行catch，并且传入错误信息。
				xhr = new XMLHttpRequest();  //ie7+ 标准浏览器
			}catch(e){
				xhr = new ActiveXObject("Microsoft.XMLHTTP");  //ie6，ie下的一个插件
			}			
			```	
			```
			if(window.XMLHttpRequest){
				xhr = new XMLHttpRequest();
			}else{
				xhr = new ActiveXObject("Microsoft.XMLHTTP");
			}
			```				
		
		* **第二步：打开一个链接**
		
			```
			xhr.open(method,url,boolean);
			```
			
			* method:发送请求的类型：post或者get。
			
				* **get:**
				
					* **速度快** 与post相比，get简单，也更快。
					* **不安全**  把数据名称和数据值用=连接，如果有多个的话，那么他会把多个数据组合起来。
					
					```
					xhr.open('GET','ajax_test.asp',true);
					xhr.send();
					```
				
				* **post:** 
				
					* 传送大量数据时，post没有数量限制。
					* 加密文件，安全性更高。  
					* 如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：
					   
						```
						xhr.open("POST","ajax_test.asp",true);     
						xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");      
						//向请求添加 HTTP 头。
						//setRequestHeader(header,value)
						xhr.send("fname=Bill&lname=Gates");
						```
				
			* url:发送请求的地址，url+"?t="+new Date().getTime()，可以清除浏览器的缓存。
			
				* 为了避免浏览器的缓存，一般向 URL 添加一个唯一的 ID：，可使用new Date().getTime()永远不会重复。
				
			* boolen:是否发送异步请求的布尔值true和false。
		
		* **第三步：发送请求**
		
			```
			xhr.send();
			```
		
		* **第四步：服务器的响应，接收返回值**
		
			```
			xhr.onreadystatechange = function(){
				if(xhr.readyState == 4){
					if(xhr.status == 200 || xhr.status == 304){
						oDiv.innerHTML = xhr.responseText;
					}else{	
						console.log(xhr.status+":"+xhr.statusText);
					}
				}
			}
			```
			
			> * responseText:作为响应主题被返回的文本，作为字符串形式的响应数据。  
			> * responseXML:如果响应的内容类型是text/xml或者，application/xml,则这个数据中包含着响应数据的xml dom文档。
			> * status:响应的http状态
			> * statusText:http状态的说明


* **onreadystatechange:** 当 readyState 改变时，就会触发 onreadystatechange 事件
	
	* **readyState** 属性存有 XMLHttpRequest 的状态信息。
		
		> 0: 请求未初始化  --尚未调用open方法     
		> 1: 服务器连接已建立   --已经调用open方法，但未调用send方法    
		> 2: 请求已接收   --已经调用send方法，但是尚未接到响应    
		> 3: 请求处理中   --已经接到部分响应    
		> 4: 请求已完成，且响应已就绪   --响应完毕   
			
	* **status:** 
			
		> 200: "ok"   
		> 404: 未找到页面
			
	* 当 readyState 等于 4 且状态为 200 时，表示响应已就绪：
	
		```
		xhr.onreadystatechange = function(){
			if(xhr.readystate == 4 && xhr.status == 200){
				document.getElementById("div").innerHTML = xhr.responseText;
			}
		}
		```
	
* **get和post的区别：**
	
	* get是从服务器上获取数据，post是向服务器传输数据。
	
	* get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。
	
	* get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB。

	* get安全性非常低，post安全性较高。但是执行效率却比Post方法好。 
	
	* 在做数据查询时，建议用Get方式；而在做数据添加、修改或删除时，建议用Post方式；
	
* **http状态码：**

	* 1xx：指示信息--表示请求已接收，继续处理
	* 2xx：成功--表示请求已被成功接收、理解、接受
	* 3xx：重定向--要完成请求必须进行更进一步的操作
	* 4xx：客户端错误--请求有语法错误或请求无法实现
	* 5xx：服务器端错误--服务器未能实现合法的请求

	常用的状态码
	
	* **200:** 请求成功
	* **304:** 内容没有修改
	* **404:** 请求失败
	* **500:** 服务器出错，无法完成请求
	
	
* **表单序列化：**






### 1.3 响应


## 2. ajax




#### xhr.abort取消异步请求。

### 2.2 post和get区别
### 2.3 表单序列化


### ajax的跨域问题

* **jsonp:** json with padding

	是json的一种使用模式，可用于解决主流浏览器跨域数据访问的问题。

	我们利用script加载的文件没有跨域问题，来获得远程json文件，但是用jsonp获取的并不是json，而是javascript。
	
	我的理解是：把远程服务器上的javascript文件加载到本地，来执行本地的javascript函数，来完成数据请求。
	
	* 使用步骤：
	
		1. 在资源加载进来之前，先定义一个函数，这个函数接收一个参数（数据），函数里面利用这个参数做一些事情。
		
		2. 然后需要的时候通过script标签加载远程文件资源，当远程文件资料被加载进来的时候，就会执行我们前面定义好的参数，并且把这个数据当成参数传入进去。
		
	* 例：按需加载 
	
		```
		<html>
		<title>jsonp</title>
		<script>
			fuction fn(data){
				alert(data);
			}
		</script>
		<script>
			var oBtn = document.getElementById("btn");
			oBtn.onclicl = function(){
				//当我们点击按钮的时候再加载远程文件，让他执行。
				var oScript = document.createElement('script');
				oScript.src = "1.txt";
				document.body.appendChild(oScript);
			}
		</script>
		<body>
			<input type="button" id="btn" value="按钮" />
		</body>
		</html>
		``` 
		
---
## 参考

* [get和post](http://www.cnblogs.com/hyddd/archive/2009/03/31/1426026.html)