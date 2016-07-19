### 一、HTML标签 与 React组件 对比

React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)。

要渲染 HTML 标签，只需在 JSX 里使用小写字母开头的标签名。

```
var myDivElement = <div className="foo" />;
React.render(myDivElement, document.body);
```

要渲染 React 组件，只需创建一个大写字母开头的本地变量。

```
var MyComponent = React.createClass({/*...*/});
var myElement = <MyComponent someProperty={true} />;
React.render(myElement, document.body);
```

React 的 JSX 里约定分别使用首字母大、小写来区分本地组件的类和 HTML 标签。

> 由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。

> ```
	React.render(  
			<label className="xxx" htmlFor="input">content</label>,   
			document.getElementById('example')
		);
	 	```
	 	
### 命名空间式组件

* 比如开发组件的时候，一个组件有多个子组件，你希望这些子组件可以作为其父组件的属性，那么可以像这样用：

	```
	var Form = MyFormComonent;
	var App = (
		<Form>
			<Form.Row>
				<Form.Label />
				<Form.Input />
			</Form.Row>
		</Form>
	);
	```
	这样你只需将子组件的 ReactClass 作为其父组件的属性：
	
	```
	var MyFormComponent = React.createClass({ ... });
	MyFormComponent.Row = React.createClass({ ... });
	MyFormComponent.Label = React.createClass({ ... });
	MyFormComponent.Input = React.createClass({ ... });
	```
	而创建子元素可以直接交给JSX转化器：
	
	```
	var App = (
		React.createElement(Form, null,
			React.createElement(Form.Row, null,
				React.createElement(Form.Label, null),
				React.createElement(Form.Input, null)
			)
		)
	);
	```


### 二、转换

JSX 把类 XML 的语法转成纯粹 JavaScript，XML 元素、属性和子节点被转换成 React.createElement 的参数。

```
var Nav;
// 输入 (JSX):
var app = <Nav color="blue" />;
// 输出 (JS):
var app = React.createElement(Nav, {color:"blue"});
```

注意，要想使用 <Nav />，Nav 变量一定要在作用区间内。

JSX 也支持使用 XML 语法定义子结点：

```
var Nav, Profile;
// 输入 (JSX):
var app = <Nav color="blue"><Profile>click</Profile></Nav>;
// 输出 (JS):
var app = React.createElement(
  Nav,
  {color:"blue"},
  React.createElement(Profile, null, "click")
);
```


### 三、JavaScript 表达式

* **JavaScript表达式：** 要使用 JavaScript 表达式作为属性值，只需把这个表达式用一对大括号 ({}) 包起来，不要用引号 ("")。

	JSX是HTML和JavaScript混写的语法，当遇到 < ，JSX就当HTML解析，遇到 { 就当JavaScript解析。


	```
	// 输入 (JSX):
	var person = <Person name={window.isLoggedIn ? window.name : ''} />;
	// 输出 (JS):
	var person = React.createElement(
  		Person,
  		{name: window.isLoggedIn ? window.name : ''}
	);
	```
	
	**子节点表达式**
	
	同样地，JavaScript 表达式可用于描述子结点：


	```
	// 输入 (JSX):
	var content = <Container>{window.isLoggedIn ? <Nav /> : <Login />}</Container>;
	// 输出 (JS):
	var content = React.createElement(
		Container,
  		null,
  		window.isLoggedIn ? React.createElement(Nav) : React.createElement(Login)
	);
	```
	
	```
	var Nav = React.createClass({
		render: function () {
			return <div>nav</div>
		}
	});
	React.render(
		<div>
			{2 > 1 ? <Nav/> : <div>div</div>}
		</div>,
		document.body
	);
	```
		
* **属性表达式：**

	```
	React.render(
		<div className={2 > 1 ? 'class-a' : 'class-b'}>content</div>,
		document.body
	);
	```
	> 结果： `<body><div class="class-a">content</div></body>`

	
* **注释：**

	JSX 里添加注释很容易；它们只是 JS 表达式而已。你只需要在一个标签的子节点内(非最外层)小心地用 {} 包围要注释的部分。
	
	```
	var content = (
		<Nav>
    	{/* 一般注释, 用 {} 包围 */}
	    <Person
    	  /* 多
         行
         注释 */
      name={window.isLoggedIn ? window.name : ''} // 行尾注释
    />
  </Nav>
);
	```
	
### JSX陷阱

* **style属性：**

	在React中写行内样式时，要这样写，不能采用引号的书写方式


	```
	React.render(
		<div style={{color:'red'}}> xxxx </div>,
		document.body
	);
	```

* **HTML属性：**

	比如我们有一些内容是用户输入的富文本，从后台取到数据后展示在页面上，希望展示相应的样式,
	React默认会进行HTML的转义，避免XSS攻击，如果要不转义，可以这么写：
	
	```
	var content='<strong>content</strong>';
	React.render(
		<div dangerouslySetInnerHTML={{__html: content}}></div>,
		document.body
	);
	```	



---


------

* **React.createElement：**

	JSX:
	
	```
	<a href="http://baidu.com">百度</a>
	```
	
	JS
	
	```
	React.createElement('a',{href: 'http://baidu.com'},'百度');
	```
	> 第一个参数是标签名，第二个参数是属性对象，第三个参数是子元素。
	
	包含子元素的例子：
	
	```
	var child = React.createElement('li', null, 'Text Content');
	var root = React.createElement('ul', { className: 'my-list' }, child);
	React.render(root, document.body);
	```
	对于常见的 HTML 标签，React 已经内置了工厂方法：
	
	```
	var root = React.DOM.ul({ className: 'my-list' },
             React.DOM.li(null, 'Text Content')
           );
	```


### 参考

