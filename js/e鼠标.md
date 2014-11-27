# 事件对象

## 复习jQuery

1、#### forEach  移动端开发

```
var a = ["a","b","c","d"];
	a.forEach(function(a,b,c){
		alert(a+":"+b+":"+c);
		// alert(this);
	},document.body)
	//第一个参数是遍历执行的时候要运行的方法，给这个方法要传三个参数：分别是当前遍历的对象（即数组里的第某项），第二项出现在数组中索引位置，第三项原数组本身。
```

#### jQuery与js对象之间的转换

## 事件

### 1

用 event.pageX 和 event.pageY 来表示鼠标相对于文档的位置，如果你有一个 500*500 的窗口并且你的鼠标在绝对中间，那么 pageX 和 pageY  的值都是 250，如果你向下滚动  500， 那么 pageY 将变成 750。
MSIE 正好相反，它使用 event.clientX 和 event.clientY 表示鼠标相当于窗口的位置，而不是文档。在同样的例子中，如果你向下滚动500，clientY 依然是 250，因此，我们需要添加 scrollLeft 和 scrollTop 这两个相对于文档的属性。最后，MSIE 中文档并不是从 0，0 开始，而是通常有一个小的边框（通常是 2 象素），边框的大小定义在  document.body.clientLeft 和 clientTop 中，我们也把这些加进去。


### 事件

e = e||window.event

e.clientX  相对于浏览器的，鼠标不动，滚动条变化时，它的值不变

e.pageX  相对于文档的，当有滚动条滚动时，它是变化的

e.target||e.srcElement

e.keyCode  

e.type  事件类型

e.preventDefault()//标准浏览器阻止默认行为

e.returnVale = false;  //IE阻止默认行为

e.stopPropagation();  //标准阻止冒泡

e.cancelBubble = true;   //IE取消冒泡

```
if(e.preventDefault()){
	e.preventDefault();
}else{
	e.returnValue = false;
}
if(e.stopPropagation){
	e.stopPropagation();
}else{
	e.cancleBubble = true;
}
```

//停止事件传播

```
if(e.)
e.stopPropagation() 
```

事件源和事件传播息息相关
事件传播包括：冒泡和捕获

### 冒泡和捕获

### 事件委托

**事件委托：**事件委托就是用事件传播的机制，无论哪一个网页元素，它的click事件都会最终传到document上。这样，则只需在document上处理click事件既可。

## 兼容性

### 1. e = e||window.event
### 2. 事件源：e.target||e.srcElement
### 3. 阻止事件传播(事件冒泡)

stopPropagation()方法用于立即停止事件在DOM层次中的传播，即取消进一步的事件捕获或冒泡。如下，阻止注册在document.body上面的事件处理程序。

```
var btn = document.getElementById("btn");
btn.onclick = function(e){
	var e = e|window.event;
	alert("按钮");
	if(e.stopPropagation){//标准浏览器
		e.stopPropagation();//阻止事件向外扩散
	}else{//IE浏览器
		e.cancelBubble = true;
	}
}
document.body.onclick = function(){
	alert()
}
```

阻止事件传播：e.stopPropagation(),e.cancelBubble=true;

### 4. 阻止浏览器的默认行为

阻止事件的默认行为：e.preventDefault(),e.returnValue=false;

```
function fn(e){
	var e = e|window.event;
	if(e.preventDefault){  //标准浏览器
		e.preventDefault();
	}else{  //IE浏览器
		e.returnValue = false;
		return false;
	}
}
```


### 5. js事件监听：
#### 5.1 绑定：e.addEventListener()和e.attachEvent()
* **绑定的方式:**IE9及以上，标准浏览器下，绑定事件的方法是：e.addEventListener()。ie8及以下浏览器：e.attachEvent()。
* > 
```
//addEventListener:监听Dom元素的事件    
//target：监听对象 
//type：监听函数类型，如click,mouseover 
//func：监听函数 
function addEventHandle(target,type,func){
	if(target.addEventListener){
		target.addEventListener(type,func,false);
	}else if(target.attachEvent){
		target.attachEvent("on"+type,func);
	}else{
		target["on"+type] = func;
	}
}
```
* **绑定的方法的this关键词：**IE是window，标准浏览器是指当前被触发事件的元素。
* **绑定的顺序：**标准浏览器是先绑定的先执行，IE是无序的。
* > 解决IE无序绑定问题：(请见附件：*无序绑定.html*)
 > 
```
function bind(ele,type,handler){
	if(ele.addEventListener){
		ele.addEventListener(type,handler,false)
	}else if(ele.attachEvent){
		if(!ele["aBind"+type]){//如果不存在这个属性，则创建一个
			ele["aBind"+type]=[];
		}
		var tempFn=function (){handler.call(ele);}
		//变形这个方法，让这个方法运行的时候this指向被绑定的元素
		tempFn.photo=handler;    //photo标识型的属性,用做和handler关联
		for(var i=0;i<ele["aBind"+type].length;i++){
			if(ele["aBind"+type][i].photo==handler){
				return; 
			}
		}
		ele["aBind"+type].push(tempFn);
		ele.attachEvent("on"+type,tempFn);
	};
}
```


#### 5.2 解除绑定：e.removeEventListener()和e.detachEvent()
* IE9及以上，标准浏览器下，绑定事件的方法是：e.removeEventListener()。ie8及以下浏览器：e.detachEvent()
* >
```
//addEventListener:监听Dom元素的事件    
//target：监听对象 
//type：监听函数类型，如click,mouseover 
//func：监听函数 
function removeEventHandle(target,type,func){
	if(target.removeEventListener){
		target.removeEventListener(type,func,false);
	}else if(target.detachEvent){
		target.detachEvent("on"+type,func);
	}else{
		delete target["on"+type];
	}
}
```
* 无序解绑
* >
```
function unbind(ele,type,handler){
	if(ele.removeEventListener){
		ele.removeEventListener(type,handler,false);
	}else if(ele.detachEvent){
		var a=ele["aBind"+type];
		if(a){
			for(var i=0;i<a.length;i++){
				if(a[i].photo==handler){
					ele.detachEvent("on"+type,a[i]);
					a[i]=null;
					return ;
				}
			}		
		}	
	}
}
```


### 6. 文档加载完成的事件：
document.addEventListener("DOMContentLoaded");

7. 7
8. 89. 
9. 9
10. 10
11. 11




### 1. 事件对象本身：
> * 火狐浏览器是虚参数，就是给方法定一个形参，但运行（事件触发运行）时不会人为的传实参，那么浏览器会自动把事件对象赋给这个参数。
> * IE是全局对象window.event。
> * chrome浏览器是二者兼有之。
2. 写在HTML里面的事件绑定，相当于把事件后边的字符串当参数，传给new Function("fn()")，相当于生成了这样一个方法：function(){fn();} 相当于：
> div.onclick = function(){fn();}
> FireFox里生成的匿名方法是这样的：
> ```
> div.onclick = function(event){fn();}
> ```
3. 这个function(event){}匿名方法才是直接被绑定到click事件上的方法，它的形式参数名叫event。而fn是在匿名方法里被调用(invoke)，如果fn需要被事件对象，则必须传参：就是event。只有一个方法，直接被绑定给事件才不需要传参数。

### 事件源

1. e.target||e.srcElement;
2. 相对于文档的鼠标坐标：e.pageX,e.pageY, IE不支持
3. 鼠标滚轮事件：IE和chrome都是onmousewheel,Firefox是DOMMouseScroll
4. dom二级的事件绑定
> 1. 绑定方式：ele.addEventListener标准浏览器的，ele.attachEvent这是ie的
> > * 绑定的方法的this关键字：ie中是window
> > * 绑定的方法执行顺序问题：标准浏览器是先绑定再执行，而ie是无序的。
> 2. 移除事件绑定的：ele.removeEventListener,ele.detachEvent；
> 3. 阻止事件的默认行为：e.preventDefault()，e.returnValue = false;
> 4. 阻止事件传播：e.stopPropagation()，e.cancleBubble = true;
5. 文档加载完成的事件：document.addEventListener("DOMContentLoaded");

window.event

### onmouseover和onmouseenter

1. onmouseenter事件是对onmouseover的改进
2. 对于传播过来的事件不响应
3. 会判断触发onmouseover事件之前，是在哪个元素上离开的：relatedTarget。如果上一次离开的元素是自己的后代元素，或是自己本身，也不触发。
4. 和onmouseenter相对应的事件叫onmouseleave


#### 绑定多个事件

```
if(ele.addEventListener){//标准浏览器下
	ele.addEventListener("click",fn1,false);
	ele.addEventListener("click",fn2,false);
	//可以同时绑定多个方法，当为false时，在冒泡阶段处理它
}else{//ie浏览器
	ele.attachEvent("onclick",fn1);
	ele.attachEvent("onclick",fn2);
}
```
> DOM2级的事件绑定：方法不同
> 绑定给事件的方法，当事件触发的时候，方法里的this关键字代表的对象不同。IE里this是window，标准浏览器里是指当前被触发事件的元素
> 绑定事件上的方法的执行顺序不一样







#### tagName和nodeName  区别？？？？