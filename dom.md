Date: 2014-08-25  
Title:   
Published: true  
Type: post  
Excerpt: 
#DOM
  
## document对象

### 获取dom对象

* 通过document获取节点
	* 明清document.getElementById(); 获取ID
	* asdfasd
	* document.getElementsByTagName();  获取标签名
	* document.getElementsByName();   获取name名，一般用于获取一组表单   

**2. 通过父节点获取**

* ele.firstChild: 获取已知元素的第一个子节点。
* ele.lastChild: 获取已知元素的最后一个子节点。

**3. 通过临近节点获取**


**4. 通过子节点获取**   

* childNode.parentNode: 获取已知节点的父节点

## element
1. ele.appendChild(newEle);  添加子节点，添加在最后面
2. ele.attributes;   返回指定节点的属性集合，有length，可遍历
3. ele.childNodes;   返回节点的子节点集合
4. ele.className;   返回元素的样式名
5. ele.clientHeight;  返回元素的可见高度，它的高度=heigh+padding，不包含border。
 

## attribute

