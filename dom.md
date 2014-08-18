Date: 2014-08-16  
Title: DOM  
Published: true  
Type: post  
Excerpt:   

# DOM


1. undefined是从null继承来的
2. 面向对象，继承
3. 包装类
4. 万物皆对象
5.

```
Math.abs;
Math = {};
Math.PI;  //用一个实例来组织归纳具有相同意义的方法和属性（常量）（把相同分类的方法和属性定义在一个对象的实例上）。这种管理和组织方法的方式叫：单例模式（命名空间）。
```

### 打分程序：去掉一个最高、最低
方法一：

```
function average(){
	var a = Array.prototype.slice.call(arguments,0);//把参数转为数组
	//或者： var a = [].slice.call(arguments,0);[]代表Array的一实例，实例上的一个方法相当于Array.prototype
	a.sort(function(a,b){return a-b });
	a.pop();
	a.shift();
	var count = null;
	for(var i=0; i<a.length; i++){
		count+=a[i];
	}
	return count/a.length;
}
var val = average(43,64,64,75,86,23,95);
alert(val);
```
方法二：

```
function average(){
	var a = Array.prototype.slice.call(arguments,0);//把参数转为数组
	a.sort(function(a,b){return a-b });
	a = a.slice(1,a.length-1);
	var count = null;
	var str = a.join("+");
	var count = eval(str);
	return count/a.length;
}
var val = average(43,64,64,75,86,23,95);
alert(val);
```

> #### 对象和数组有什么联系和区别
> 1. 数组是对象，并且是对象存值的升级
> 2. 数组不能ary.0，只能使用ary[0]
> 3. object类型的可操作性不好，--升级--只按数字为索引--扩展一些方法，把散列无序的表，升级成有序的表
> 4. 只有数组类上有这些操作有序集合的这些方法
> 5. Js还有类数组的概念--类数组可以去用数组上定义的这些方法

##下周练习：
##### 1. 把数组类的18个方法按以上原则写下来，并且每一个方法都要最少配上一个小例子
##### 2. 实现以下功能的函数：在m个数中，随机取出n个数来（比如：有100个数，随机取出其中的10个来。）
> 先写一个随机函数，可以根据一个范围，得到一个随机数，比如说：得到0-99之间的一个随机数，randowm(n,m)
> var result = [];

##### 3. Object.prototype.toString.call(null);//object类的toString方法


## call和apply
### call和apply作用一样


```
var innerHTML = "window的innerHTML"；
var obj = {innerHTML:"obj的innerHTML",fn:function(a,b,c){
	alert((a+b+c)+","+this.innerHTML)；
}}
	obj.fn(1,1,1);
	obj.fn.call(window,2,3,4);
	var ele = document.getElementById("div");
	obj.fn.call(ele,5,5,5);
	//call的参数中，从第2个位置开始，往后都是给fn的参数
	//obj.fn.apply(ele);
	obj.fn.apply(ele,["abc",5,"cde5"]);  //apply最多需要两个参数，第二个参数是集合，把传给fn的参数打包传给fn
function fn(){
	fn2.apply(null,arguments);
}	
```

### aplly的奇怪用法：
```
var a = [8,3,99,22,77,34,76,31,85,56];
//以最快捷的方式，在这个数组里找到最大值或最小值
//方法一：a.sort(function(a,b){return a-b});
//方法二：
Math.min.apply(null,a);//利用apply的辅助功能，把一个打包的参数集合传给了min方法;
Math.min(a);
```
### 什么时候用call和apply
>* 只要需要改变：方法运行时的上下文（this），则必须考虑call或者apply方法。
>* call可包含多个参数
>* apply只包含两个参数，第二个参数是集合，是把传给fn的参数进行打包


### 闭包：当一个函数运行的时候，产生的私有作用域就叫闭包； 

### DOM core 
1. document.all["div1"];
2. document.forms;
3. document.anchors;
4. document.getElementById("div1").style.height;

DOM通用，并且跨平台的API。

```
var ele1 = document.getElementsByTagName("*");
//中间html代码块
var ele2 = document.getElementsByTagName("*");
alert(ele1===ele2);
//当网页在浏览器中加载的时候，就会形成DOM树，并且不同类型的节点，会事先安排好不同的集合对象
//DOM nodeList,ElementCollection
//并且DOM集合里的元素只依赖于文档的文化的，不能使用其它方法来
```

#### 页面上的li排序


```
<html>
<body>
<ul>
	<li>54</li>
	<li></li>
</ul>
</body>
</html>
```

```
var oLis = document.getElementsByTagName("li");
try{
	//异常捕捉机制，主动补救措施
	var a = [].slice.call(oLis,0);  //var a = Array.prototype.slice.call(oLis,0);
}catch(e){//e相当于一个形参变量，当发生异常的时候，会把异常对象赋给e变量。
	var a = [];
	for(var i=0;i<oLis.length;i++){
		a.push(oLis[i]);
	}
}finally{
	//即使上边try和catch都出错了，finally里面的代码都会执行
}
a.sort(function(a,b){return a.innerHTML-b.innerHTML});
for(var i=0;i<a.length;i++){
	a[i].parentNode.appendChild(a[i]);
}
```
> IE6,7,8不兼容[].slice(Array.prototype.slice),用try catch解决

```
function listToArray(eles){//封装
		try{
			return [].slice.call(eles,0);
		}catch(e){
			var ary = [];
			for(var i=0;i<eles.length;i++){
				ary.push(eles[i]);
			}
			return ary;
		}
	}
	var oLis = document.getElementsByTagName("li");
	var ary = listToArray(oLis);
	// var ary = [].slice.call(oLis,0);
	console.log(ary);
	ary.sort(function(a,b){return a.innerHTML-b.innerHTML});
	for(var i=0;i<ary.length;i++){
		ary[i].parentNode.appendChild(ary[i]);
	}
```

## 中文排序
---

> 如果对这些li进行排序，不能直接去操作DOM集合，因为DOM集合是依赖页面元素的位置，不能直接修改
> 则先需要把DOM集合转化为数组，然后对数组进行排序
> 因为数组和页面没有依赖关系，数组里面DOM元素的位置虽然被调整了，但不会影响页面的变化
> 使用appendChild重新调整页面上元素的位置（根据数组里的顺序）


### View

* Toggle live preview: Shift + Cmd + I   切换左右
* Toggle Words Counter: Shift + Cmd + W  关闭
* Toggle Transparent: Shift + Cmd + T  
* Toggle Floating: Shift + Cmd + F  
* Left/Right = 1/1: Cmd + 0   平分窗口
* Left/Right = 3/1: Cmd + +   黑变大
* Left/Right = 1/3: Cmd + -   黑变小
* Toggle Writing orientation: Cmd + L   
* Toggle fullscreen: Control + Cmd + F   搜索

#### Actions

* Copy HTML: Option + Cmd + C  复制
* Strong: Select text, Cmd + B  加粗
* Emphasize: Select text, Cmd + I   斜体
* Inline Code: Select text, Cmd + K  `代码块`
* Strikethrough: Select text, Cmd + U  ~~划掉~~
* Link: Select text, Control + Shift + L  
* Image: Select text, Control + Shift + I   ![image](http://)
* Select Word: Control + Option + W    
* Select Line: Shift + Cmd + L  选择整行
* Select All: Cmd + A   选择全部
* Deselect All: Cmd + D   删除全部
* Convert to Uppercase: Select text, Control + U  变大写
* Convert to Lowercase: Select text, Control + Shift + U   小写
* Convert to Titlecase: Select text, Control + Option + U  选词
* Convert to List: Select lines, Control + L
* Convert to Blockquote: Select lines, Control + Q
* Convert to H1: Cmd + 1
* Convert to H2: Cmd + 2
* Convert to H3: Cmd + 3
* Convert to H4: Cmd + 4
* Convert to H5: Cmd + 5
* Convert to H6: Cmd + 6
* Convert Spaces to Tabs: Control + [
* Convert Tabs to Spaces: Control + ]
* Insert Current Date: Control + Shift + 1
* Insert Current Time: Control + Shift + 2
* Insert entity <: Control + Shift + ,
* Insert entity >: Control + Shift + .
* Insert entity &: Control + Shift + 7
* Insert entity Space: Control + Shift + Space
* Insert Scriptogr.am Header: Control + Shift + G
* Shift Line Left: Select lines, Cmd + [
* Shift Line Right: Select lines, Cmd + ]
* New Line: Cmd + Return
* Comment: Cmd + /
* Hard Linebreak: Control + Return

#### Edit

* Auto complete current word: Esc
* Find: Cmd + F
* Close find bar: Esc

#### Post

* Post on Scriptogr.am: Control + Shift + S
* Post on Tumblr: Control + Shift + T

#### Export

* Export HTML: Option + Cmd + E
* Export PDF:  Option + Cmd + P





***
---
---




An email <example@example.com> link.

Simple inline link <http://chenluois.com>, another inline link [Smaller](http://smallerapp.com), one more inline link with title [Resize](http://resizesafari.com "a Safari extension").

A [reference style][id] link. Input id, then anywhere in the doc, define the link with corresponding id:

[id]: http://mouapp.com "Markdown editor on Mac OS X"

Titles ( or called tool tips ) in the links are optional.

#### Images

An inline image ![Smaller icon](http://smallerapp.com/favicon.ico "Title here"), title is optional.

A ![Resize icon][2] reference style image.

[2]: http://resizesafari.com/favicon.ico "Title"

#### Inline code and Block code

Inline code are surround by `backtick` key. To create a block code:

	Indent each line by at least 1 tab, or 4 spaces.
    var Mou = exactlyTheAppIwant; 

####  Ordered Lists

Ordered lists are created using "1." + Space:

1. Ordered list item
2. Ordered list item
3. Ordered list item

#### Unordered Lists

Unordered list are created using "*" + Space:

* Unordered list item
* Unordered list item
* Unordered list item 

Or using "-" + Space:

- Unordered list item
- Unordered list item
- Unordered list item

#### Hard Linebreak

End a line with two or more spaces will create a hard linebreak, called `<br />` in HTML. ( Control + Return )  
Above line ended with 2 spaces.

#### Horizontal Rules

Three or more asterisks or dashes:

***

---

- - - -

#### Headers

Setext-style:

This is H1
==========

This is H2
----------

atx-style:

# This is H1
## This is H2
### This is H3
#### This is H4
##### This is H5
###### This is H6


### Extra Syntax

#### Footnotes

Footnotes work mostly like reference-style links. A footnote is made of two things: a marker in the text that will become a superscript number; a footnote definition that will be placed in a list of footnotes at the end of the document. A footnote looks like this:

That's some text with a footnote.[^1]

[^1]: And that's the footnote.


#### Strikethrough

Wrap with 2 tilde characters:

~~Strikethrough~~


#### Fenced Code Blocks

Start with a line containing 3 or more backticks, and ends with the first line with the same number of backticks:

```
Fenced code blocks are like Stardard Markdown’s regular code
blocks, except that they’re not indented and instead rely on
a start and end fence lines to delimit the code block.
```

#### Tables

A simple table looks like this:

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

If you wish, you can add a leading and tailing pipe to each line of the table:

| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |

Specify alignement for each column by adding colons to separator lines:

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right


### Shortcuts


### And more?

Don't forget to check Preferences, lots of useful options are there.

Follow [@chenluois](http://twitter.com/chenluois) on Twitter for the latest news.

For feedback, use the menu `Help` - `Send Feedback`