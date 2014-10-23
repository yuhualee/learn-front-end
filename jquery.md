Date: 2014-08-31  
Title:jqeury   
Published: true  
Type: post  
Excerpt: 

# jQuery

#### 1. 天生闭包

```
$(document).ready(function(){
	//代码块
});
```
```
$(function(){
	//代码块
})
```

#### 2. 查找
1. find 在所有子孙元素中查找
2. filter 在平级元素中查找
3. children 在子元素中查找
4. eq()
5. :even,:odd,:first,:last,:eq(),:gt(8)<!--大于8-->,:lt(8)<!--小于8的-->,:first-child
> first是指第一个子元素，first-child是指所有里面的老大，比如一个里面有三个ul，每个ul里面有li，first则指第一个，而first-child是指每个ul里面的第一个li老大。



#### jQuery有五种参数方式
1. 参数是function
2. css选择器格式的字符串，则执行一个dom查找的行为。
3. 参数是dom对象，则将此dom对象包装成一个jQuery对象。
4. 是一个html格式的字符串，表示按此格式生成dom对象。
5. 什么也不传，或传一个空的jquery对象。


#### 实现：(5).plus(3).reduce(2)=5+3-2=6;

```
Number.prototype.plus=function(n){
	return this+n;
}
Number.prototype.reduce=function(n){
	return this-n;
}
console.log((5).plus(3).reduce(2));
```

## 自己封装一个类Query库