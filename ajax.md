Date: 2014-09-20  
Title: ajax
Published: true  
Type: post  
Excerpt:   

# ajax
## 1. 准备
### 1.1 post和get
1.1.1 get是从服务器上获取数据，post是向服务器传输数据。


### 1.2 http状态码

##### 1.2.1 200K 
##### 1.2.2 304 not modified
##### 1.2.3 404 not found
##### 1.2.4 500 Internal Server Error

### 1.3 响应


## 2. ajax

### 2.1简单的ajax实例

```
//第一步：创建一个ajax对象
var xhr = null;
try{
	var xhr = new XMLHttpRequest();   //标准浏览器，ie7+
}cathc(e){
	var xhr = new ActiveXObject("Microsoft.XMLHTTP");  //IE6
}
//第二步：打开一个链接
xhr.open(method,url,boolen);
//method:发送请求的类型：post或者get。
//url:发送请求的地址，url+"?t="+new Date().getTime()，可以清除浏览器的缓存。
//boolen:是否发送异步请求的布尔值true和false。
//第三步：发送请求
xhr.send(null);
//第四步：接收返回值
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
> * responseText:作为响应主题被返回的文本
> * responseXML:如果响应的内容类型是text/xml或者，application/xml,则这个数据中包含着响应数据的xml dom文档。
> * status:响应的http状态
> * statusText:http状态的说明

#### readyState

表示请求/响应过程的当前阶段，分为五个状态：

* 0: 未初始化:尚未调用open()方法
* 1: 启动：已经调用open()方法，但尚未调用send()方法
* 2: 发送：已经调用send()方法，但是尚未接到响应
* 3: 接收：已经接到到部分的响应数据
* 4: 完成：接收完毕。

#### xhr.abort取消异步请求。

### 2.2 post和get区别
### 2.3 表单序列化