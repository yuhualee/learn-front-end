Date: 2014-09-10  
Title: arguments  
Published: true  
Type: post  
Excerpt:   


# arguments

## arguments定义
所有的函数都有一个自己的arguments对象，用来储存它实际接受到的参数，而不局限于函数声明时所定义的参数列表。它不是数组却类似数组，具有数组一样的访问性质及方式，可以由arguments[n]来访问对应的单个参数的值，并拥有数组长度属性length。但是却不具有数组的一些方法。可以通过call把arguments转化成真正的数组，然后进行数组的操作。

```
var args = Array.prototype.slice.call(arguments);
```
## 类数组
### 1. 判断arguments是不是数组

alert(arguments instanceof Array);
alert(arguments instanceof Object);

### 2. 如何严格的判断一个数据是数组（Array）类的实例

```
function isArray(value){
     if (typeof Array.isArray === "function") {
         return Array.isArray(value);    
     }else{
         return Object.prototype.toString.call(value) === "[object Array]";    
     }
}
```
### 3. 把arguments转换成数组
**方法一：**内置的类型可以通过prototype找到内置的属性方法，Array.prototype.slice就是访问Array的内置方法slice。通过slice方法，返回一个数组。call是调用一个对象的方法，以另外一个对象替换当前对象。

```
var arg = Array.prototype.slice.call(arguments,0);
```
**方法二：**比方法一性能要差一点，因为它是先创建一个数组，然后再进行的

```
var arg = [].slice.call(arguments,0);
```
**方法三：通过循环转变成数组**

```
function toArray(arguments){
	var a = [];
	for(var i=0;i<arguments.length;i++){
		a.unshift(arguments.[i]);
	}
	return a;
}
```

## caller
当一个函数被另一个函数调用的时候，被调用的函数会自动生成一个caller属性，指向调用它的函数对象，如果函数未被调用，则caller为null。

```
function testCaller() {  
    var caller = testCaller.caller;  
    alert(caller);  
}   
function aCaller() {  
    testCaller();  
}    
aCaller();  
```
> 弹出的是函数aCaller的内容。

## arguments.callee
arguments.callee指向正在运行的函数自身,返回正被执行的 Function 对象，也就是所指定的 Function 对象的正文。

**注意：arguments.length是实参长度，arguments.callee.length是形参长度，通常用来判断形参与实参长度是否一致**

**通过arguments获得函数的实参，通过arguments.callee获得函数的形参**


#### 例：callee求1-n的和
```
function fn(n){
	if(n==1) return n;
	else return n+arguments.callee(n-1);
}
```
> 它可以让一个匿名函数自己调用自己


#### 例:

```
function list(type){
  var result = "<"+type+"l><li>";
  var args = Array.prototype.slice.call(arguments,1);
  result += args.join("</li><li>");
  result += "</li></"+type+"l>";
  return result;
}
var listHtml = list("o","one","two");
console.log(listHtml);
```
#### 例2：面试题：下面的console.log结果是[1,2,3,4]的是？

```
function foo(x){
	console.log(arguments);
	return x;
}
foo(1,2,3,4);
```
```
function foo(x){
	console.log(arguments);
	return x;
}(1,2,3,4)
```
> 在预解释的时候，function fn(){}(1);会被分开处理，分成两个函数，第一个是function fn()
{}，而第二个则为匿名函数：(1)。如果第二个不带参数，就会报错，但是上面的函数包含在一个()里面，则是正确的。

> ```
> (function fn(){
>  console.log(arguments);
> }(1,2,3,4));
> ```

```
(function foo(x){
	console.log(arguments);
	return x;
})(1,2,3,4)
```
```
function foo(){
	bar.apply(null,arguments);
}
function bar(x){
	console.log(arguments);
}
foo(1,2,3,4);
```


