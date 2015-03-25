* **什么是回调函数**   
	把一个函数当成参数传入到另外一个函数当中，这个函数就是回调函数。 
	
	```
//例1：不带参数的回调函数
function a(b,c){
    return b()+c();
}
function b(){
    return 10;
}
function c(){
    return 7;
}
alert(a(b,c));  //17
```
```
//例2：带参数的回调函数
function f(a,b,fn){
    var c = a+b;
    fn(c);
}
function fn(c){
    alert(c);
}
f(1,2,fn);
```

	* 举例：**forEach回调函数**
	
		```
//例3：计算数组总和
var ary = [1,2,45,66];
var total=0;
ary.forEach(function(num){
	total+=num;
});
console.log(total);   //114
	```
	* jQuery里面的回调函数
	
		```
	//例4：
	$("div").click(function(){
		//code...
	})
	```
	
* **回调函数是怎样运行的**    
当我们把函数当成参数传递给函数时，我们可以像对象变量一样，对待回调函数。我们传递的只是函数的定义，并没有在参数中执行该函数，而是在函数内某个特定的时间点被回调。*比如例3中，在每次forEach时，都会调用回调函数。*

* **回调函数是闭包**    


*  **实现回调函数的基本原理**   
		
```   
//全局变量
var allUserData = [];

//普通的logStuff函数，将内容打印到控制台     
function logStuff (userData){
    if ( typeof userData === "string")
    {
        console.log(userData);
    }
    else if ( typeof userData === "object"){
        for(var item in userData){
            console.log(item + ": " + userData[item]);
        }
    }
} 

//一个接收两个参数的函数，后面一个是回调函数     
function getInput (options, callback){
    allUserData.push(options);
    callback(options);
}

//当我们调用getInput函数时，我们将logStuff作为一个参数传递给它     
//因此logStuff将会在getInput函数内被回调（或者执行）     
getInput({name:"Rich",speciality:"Javascript"}, logStuff);
//name:Rich
//speciality:Javascript

```

* **在执行之前确定回调函数是一个函数**

	```
	function(options,callback){
		if(typeof callback == "function"){
			callback();
		}
	}
	```

*  **使用this对象的方法作为回调函数时的问题**

	当回调函数是一个this对象的方法时，我们必须改变执行回调函数的方法来保证this对象的上下文。
	
	```
	var obj = {
    name:"李玉华",
    age:18,
    show:function(name,age){
        alert(this.name+":"+this.age);
    }
}
var name = "胡畅";
var age = 2;
function fn(name,age,callback){
    //this.name = name;
    //this.age = age;
    callback(name,age);
}
obj.show();
fn("胡雄飞",28,obj.show);
alert(window.name);
	```
	
	可以全用call和apply来改变上下文。
	
	
	
	
	
	
* **回调函数的使用场合**

	资源加载：动态加载js文件后执行回调，加载iframe后执行回调，ajax操作回调，图片加载完成执行回调，AJAX等等。
DOM事件及Node.js事件基于回调机制(Node.js回调可能会出现多层回调嵌套的问题)。
setTimeout的延迟时间为0，这个hack经常被用到，settimeout调用的函数其实就是一个callback的体现
链式调用：链式调用的时候，在赋值器(setter)方法中(或者本身没有返回值的方法中)很容易实现链式调用，而取值器(getter)相对来说不好实现链式调用，因为你需要取值器返回你需要的数据而不是this指针，如果要实现链式方法，可以用回调函数来实现
setTimeout、setInterval的函数调用得到其返回值。由于两个函数都是异步的，即：他们的调用时序和程序的主流程是相对独立的，所以没有办法在主体里面等待它们的返回值，它们被打开的时候程序也不会停下来等待，否则也就失去了setTimeout及setInterval的意义了，所以用return已经没有意义，只能使用callback。callback的意义在于将timer执行的结果通知给代理函数进行及时处理。

异步调用（例如读取文件，进行HTTP请求，等等）
时间监听器/处理器
setTimeout和setInterval方法
一般情况：精简代码

* **回调函数的传递**

	上面说了，要将函数引用或者函数表达式作为参数传递。
	
	```
$.get('myhtmlpage.html', myCallBack);//这是对的
$.get('myhtmlpage.html', myCallBack('foo', 'bar'));//这是错的，那么要带参数呢？
$.get('myhtmlpage.html', function(){//带参数的使用函数表达式
myCallBack('foo', 'bar');
});
```
另外，最好保证回调存在且必须是函数引用或者函数表达式


**参考：**   
<http://www.html-js.com/article/1592>
