## js浏览器对象

### window对象

#### 1. window对象

* window对象是BOM的核心，window对象指当前的浏览器窗口

* 所有的js全局对象、函数以及变量均自动成为window对象的成员

* 全局变量是window对象的属性

* 全局函数是window对象的方法

* 甚至HTML DOM的document也是window对象的属性之一

#### 2. window尺寸

* window.innerHeight - 浏览器窗口的内部高度

* window.innerWidth - 浏览器窗口的内部宽度

#### 3. window方法

* window.open() - 打开新窗口

* window.close() - 关闭当前窗口

	---

### 计时器

#### 1. 计时事件：

通过使用javascript，我们有能力做到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行，我们称之为计时事件。

#### 2. 计时方法：

1. setIntevel() - 间隔指定的毫秒数不停地执行指定的代码

	clearInterval() - 用于停止setInterval()方法执行的函数代码
	
2. setTimeout() - 暂停指定的毫秒数后执行指定的代码

	clearTimeout() - 方法用于停止执行setTimeout()方法的函数代码

	---

### history对象

#### 1. window.history 对象包含浏览器的历史url的集合

#### 2. History方法

* history.back() - 与在浏览器点击后退按钮相同

* history.forward() - 与在浏览器中点击按钮向前相同

* history.go() - 进入历史中的某个页面

	---

### loction对象

#### 1. Location对象：

window.location对象用于获得当前页面的地址URL，并把浏览器重定向到新的页面。

#### 2. Location对象的属性：

* location.hostname 返回web主机的域名
* location.pathname 返回当前页面的路径和文件名
* location.port 返回web主机商品
* location.protocol 返回所使用的web协议（http://或https://）
* loaction.href 属性返回当前页面的url
* loaction.assign() 方法加载新的文档

	```
	location.assign('http://baidu.com');
	```
	
	---

### Screen对象

#### 1. Screen对象

window.screen - 对象包含有关用户屏幕的信息

#### 2. 属性

* screen.availWidth - 可用的屏幕宽度
* screen.availHeight - 可用的屏幕高度
* screen.Height - 屏幕高度
* screen.Width - 屏幕宽度

	---

### 注意

* window.innerHeight - 浏览器窗口内部的高度，不包含工具栏、标题栏等
* screen.availHeight - 屏幕窗口可用的高度，不包含桌面本身的工具栏等
* screen.height - 屏幕窗口的高度，包含工具栏等。

---
---

## js内置对象

### 什么是对象

1. 创建对象

	```
	people = new Object();
	people.name = 'lyh';   <!--属性-->
	people.age = 30;
	alert(people.name + ':' +people.age);   <!--获取对象的属性-->
	```
	```
	people = {name: lyh, age: 30};  <!--创建对象-->
	```
	使用一个函数创建一个对象
	
	```
	function People(name,age){
		this._name = name;
		this._age = age;
	}
	son = new People('hmh',3);
	alert(son._name + ':' + son._age);
	```


### String字符串对象



### Date日期对象

### Array数组对象

### Math对象