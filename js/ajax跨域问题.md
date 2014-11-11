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