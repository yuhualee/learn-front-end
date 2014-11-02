Date: 2014-08-30  
Title:   
Published: true  
Type: post  
Excerpt: 
# js  盒子模型

## 元素页面居中

### 基本概念
##### client
1. **clientWidth**：元素的可见宽度，不包含滚动条和border。
> clientWidth=padding+content(可见内容)
2. **clientHeight**:元素的可见高度，不包含滚动条和border。
> clientHeight = padding + content.
3. **clientLeft**:元素边框的宽度，也就是border-left
4. **clientTop**:元素边框的高度

##### offset
1. **offsetParent**:属性返回一个对象的引用，这个对象是距离调用offsetParent的元素最近的（在包含层次中最靠近的），并且是已进行过CSS定位的容器元素。 如果这个容器元素未进行CSS定位, 则offsetParent属性的取值为根元素的引用。


2. **offsetWidth**:元素自身的绝对宽度，不包括因overflow而未显示的部分。它和clientWidth的区别在于，它包含滚动条的宽度和border
> offsetWidth=content+padding+border+滚动条宽度
3. **offsetHeight**:元素实际内容的高度，包含滚动条的高度和border
> offsetHeight = content + padding + border + 滚动条的高度
4. **offsetLeft**:也就是返回对象元素边界的左上角顶点相对于offsetParent的左上角顶点的水平偏移量。
5. **offsetTop**:也就是返回对象元素边界的左上角顶点相对于offsetParent的左上角顶点的垂直偏移量。
>* 在IE8/9/10及Chrome中:
```offsetLeft = ((offsetParent的border-width)+(offsetParent的padding-left)+中间元素的宽度```。
>* 在FireFox中，不包含offsetParent的border。
```
offsetLeft = (offsetParent的padding-left)+中间元素的宽度。
```


### 注意：它们的返回值都是数字，也就是number类型的，在转换成style.left或style.top时需要加上“px”。

### 元素页面居中
```
var ele = document.getElementById('div1');
	var winWidth = document.documentElement.clientWidth||document.body.clientWidth;
	var winHeight = document.documentElement.clientHeight||document.body.clientHeight;
	var l = winWidth/2-ele.offsetWidth/2;
	var t = winHeight/2-ele.offsetHeight/2;
	ele.style.left = l+"px";
	ele.style.top = t+"px";
```

### 作业题：弹出窗口



http://blog.sina.com.cn/s/blog_6739ffde0100ijy4.html
http://www.cnblogs.com/jscode/archive/2012/09/03/2669299.html
http://www.jb51.net/article/19844.htm
http://www.cnblogs.com/jscode/archive/2012/09/03/2669299.html


## 逻辑运算
### || &&

1. 逻辑||运算，a||b，如果a成立，则返回a，不再进行b运算；如果a不成立，则运算b，不管b成立与否都返回b。||也就是遇到成立的则返回，否则，直到结束。
2. 逻辑&&，a&&b&&c，如果a成立，则向计算；如果a不成立，则返回a。&&也就是遇到不成立的则返回，否则，直到结束。
3. &&比||的优先级要高，所以先运算&&，比如：a||b&&c，它是先运算b&&c，但是返回的时候，如果a成立，则返回的是a，虽然在此先计算了b&&c。其实是||把它前后分为两部分，先分别计算两边的部分，然后再进行比较。
> 
```
var a=1,b=false,c=" ",d=9,e="a";
	alert(a||b);  //1
	alert(a&&b);  //false
	alert(b||c);  //空
	alert(a&&b&&c);  //false
	alert(a||b&&c);  //1
	alert(b||a&&c);  //空
	alert(a||d&&e);
	alert(b||c&&a);  //1
```