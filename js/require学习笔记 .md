## 模块加载器原理

* **按依赖关系加载js**: document.createElement("script") & appendChild()

* **document.currentScript:** 获得当前正在执行的script。

* 使用模块加载器后最头疼的是构建发布问题



## requirejs

* **功能**  RequireJS 可以帮助用户异步按需的加载 JavaScript 代码，并解决 JavaScript 模块间的依赖关系，提升了前端代码的整体质量和性能。

	1. 加载javascript文件 
	2. 定义javascript模块
	
* **加载requirejs**

	```
	<script src="js/require.js" defer async="true" data-main="js/main"></script>  
	```
	> defer : 该属性用来通知浏览器，这段脚本代码将不会产生任何文档内容。延迟脚本的执行。
	    
	> saync : async="true/false":该属性为html5中新增的属性，它的作用是能够异步地下载和执行脚本，不因为加载脚本而阻塞页面的加载。一旦下载完毕就会立刻执行。 
	   
	> data-main: 告诉require.js，在它加载之后加载main.js   


* **配置requireJs**

	```
	require.config({
		baseUrl: "./js",
		paths: {
			"some": "some/v1"
		},
		waitSeconds: 10
	});
	require(["some/module","my/module","js/a.js"],function(someM,myM,aM){
		//
	);
	```
	
	* **baseUrl**
	
		> 1. baseUrl指明的是所有模块的base url，比如，some/module 加载的是 ./js/some/module.js。
		> 2. 但是以.js，"/"，或者“http”，的文件加载时不会使用该路径。它仍然会使用当前index.html所在的相对路径来加载。   

		> 3. 如果baseUrl没有指定，就会全用data-main中指定的路径。
		
	* **paths**  替换路径
	
		> paths 中定义的路径是用于替换模块中的路径，如上例中的 some/module 具体的 JavaScript 文件路径是 /js/some/v1/module.js 。
		
	* **waitSecondes** 延迟加载javascript文件
	
	* **shim:** 参数解决了使用非AMD方式定义的模块（如jquery插件）及其载入顺序。
	
		```
		//让jquery先加载进来
		require.config({
			shim: {
				"jquery-slide": ["jquery"]
			}
		});
		require(["jquery-slide"]);
		```
		> 保证先加载jquery.js，再加载jquery-slide.js。
		
	* **map:** 解决同一模块，不同版本的问题。
	
		```
		require.config({
			map: {
				"a": {
					"jquery" :"jquery-1.6.4"
				},
				"b": {
					"jquery": "jquery-1.7.2"
				}
			}
		})
		reuqire(["a"]);  //a模块加载jquery-1.6.4
		require(["b"]);  //b模块加载jquery-1.7.2
		```
		
	* **config:** 用来给指定的模块传递一些有用的数据。
	
		```
		require.config({
			config:{
				"A": {
					info:{
						name:"lee"
					}
				}
			}
		})
		```
		在a模块中使用a.config().info来获取；
		
		```
		require(["A"],function(a){
			var info = a.config().info;
			console.log(info);
		})
		```
		
	* **errbacks:** 函数调用不成功时。
	
		```
		require(["a"],function(suc){
			console.log(suc);
		},function(err){
			console.log(err);
		})
		```
	

	
* **使用requirejs:** 

	* **定义模块：** define 用来存储代码作为一个已命名的模块。Asynschronous Moduls Definition 异步模块定义。
	
		```
		//独立模块
		define(function(){
    		return {
		        createStudent : function(a,b){
        		    //代码
        		}
    		};
		});		
		```
		```
		//带引用其它模块
		define(["a.js","b.js"],function(aM,bM){
			//code...
		});
		```



	* **main.js**

		```
		
		```

* **requirejs 2.0：**

	


	
* **优化requirejs optimizer:** 的使用，合并与压缩

	是requireJs自带的压缩工具，
	
	1. 首页需要安装node.js，然后下载[r.js](http://requirejs.org/docs/download.html#rjs).
	
	2. 使用方法：
	
		* 方法一：直接在命令行里面进行优化
		
			```
			node r.js -o baseUrl=js name=main out=built.js
			```
			> 1. **-o:** 表示优化，该参数是固定的，必选。
			> 2. **baseUrl:**  指存放模块的根目录，这里是js，如果没有设置将从当前目录中查找main.js。
			> 3. **name:** 模块的入口文件，这里设置成“main”，那么r.js会从baseUrl+main去查找。这里实际是js/main.js。r.js会分析main.js，找出其所依赖的所有其它模块，然后合并压缩。
			> 4. **out:** 指合并压缩后输出的文件路径，这里直接是built.js，那么将输出到根目录r4下。
			> 5. **excludeShallow=selector:**  合并时将排除该文件，单独加载。
			> 6. **optimize (none/uglify/closure) :** 指定是否压缩，以哪种文件压缩。默认是uglify。
			
			```
			//如果使用的google cdn 上的jquery，我们压缩的时候不需要把它进行压缩，可以使用paths
			require.config({
				baseUrl: 'js',
				paths: {
					"jquery": "https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min"
				}
});
			```
			> 同时使用 `paths.jquery=empty:` 这样就会单独加载它。*注意empty后面有一个冒号*
		
		
		* 方法二：使用配置文件
		
			```
			({
    			appDir: "./",
			    baseUrl: "js",
			    dir: "../r-build",
			    paths: {
			        jquery: 'empty:'
			    },
			    modules: [
		        {
        		    name: "main"
		        },
		        {
		            name: "add"
        		}
			    ]
			})
			```
			
	* **使用r.js压缩css文件**
	
		```
		node r.js -o cssIn=css/main.css out=css/build.css optimizeCss=standard
		```
		
		> * none  不压缩，仅合并
		> * standard  标准压缩 去换行、空格、注释
		> * standard.keepLines  除标准压缩外，保留换行
		> * standard.keepComments  除标准压缩外，保留注释
		> * standard.keepComments.keepLines  除标准压缩外，保留换行和注释
		
	
	参考文章 		：
	
	[requirejs合并与压缩](http://www.oschina.net/translate/optimize-requirejs-projects)。
		 
 	[前端优化：RequireJS Optimizer 的使用和配置方法](http://segmentfault.com/a/1190000000391986)
 	
 	[requireJs进阶](http://www.cnblogs.com/snandy/archive/2012/06/07/2537477.html)
 	
 	[requireJs 2.0](http://www.cnblogs.com/snandy/archive/2012/06/04/2532997.html)

* **requirejs工作原理**

	```
	function loadjscssfile(filename, filetype) {
    if (filetype == "js") { //作为js文件载入
        var fileref = document.createElement('script')
        fileref.setAttribute("type", "text/javascript")
        fileref.setAttribute("src", filename)
    }
    else if (filetype == "css") {  //作为css文件载入
        var fileref = document.createElement("link")
        fileref.setAttribute("rel", "stylesheet")
        fileref.setAttribute("type", "text/css")
        fileref.setAttribute("href", filename)
    }
    if (typeof fileref != "undefined")
        document.getElementsByTagName("head")[0].appendChild(fileref)
	}
	loadjscssfile("myscript.js", "js")
	loadjscssfile("javascript.php", "js")
	loadjscssfile("mystyle.css", "css")
	```
	> RequireJS 会顺着依赖链（也就是顺着模块声明的依赖层层进入，直到没有依赖为止）把所有需要加载的模块按顺序一一加载完毕，然后才执行回调函数。

---










[中文档](http://makingmobile.org/docs/tools/requirejs-api-zh/#config)


## seajs

## 两者的区别



参考：[两者的区别](http://www.zhihu.com/question/21157540)