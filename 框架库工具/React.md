

* **HTML模板**

	```
	babel src --out-dir build
	```
	> 上面命令可以将 src 子目录的 js 文件进行语法转换，转码后的文件全部放在 build 子目录。
	
	
* **reactDOM.render()**

	ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

	例1：
	
	```
	ReactDOM.render(
		<h1>Hello,world!</h1>
		document.getElementById('example')
	);
	```
	
	或者：要渲染 HTML 标签，只需在 JSX 里使用小写字母开头的标签名。
	
	```
	var myDivElement = <div className="red" />;
	React.render(myDivElement,document.body);
	```
	> 声明变量采用 首字母小写。
	
	要渲染 React 组件，只需创建一个大写字母开头的本地变量。
	
	```
	var MyComponent = React.createClass({
		//code..
	});
	var myDiv = <MyComponent someProperty={true}/>;
	React.render(myDiv,document.body);
	```
	
	> React 的 JSX 里约定分别使用首字母大、小写来区分本地组件的类和 HTML 标签。
	

	
* **语法**

	1. HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写，**如例1**。
	
	2. 遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。
	
		例2：
	
		```
	var names = ['lyh','hxf','hmh'];
    ReactDOM.render(
      <div>
      {
        names.map(function(name){
          return <p>hello,{name}</p>
        })
      }
      </div>,
      document.getElementById('example')
    );
	```
	
	

	* JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员（查看
	
		例3：
	
		```
	var arr = [
      <li>我是一只小小鸟</li>,
      <li>宝宝</li>,
      <li>爸爸</li>
    ];
    ReactDOM.render(
      <ul>{arr}</ul>,
      document.getElementById('example')
    );
	```
	
	* **{}** - js执行
	
	* **{{}}**
	
	
	
### 样式

由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。

```
var Hello = React.createClass({
   render: function() {
     var styleObj = {
       color: "green",
       fontSize: "20px"
     };
     return <div className="red">Hello <span style={{color:"blue"}}>{this.props.title}</span> <span style={styleObj}>{this.props.name}</span></div>;
   }
 });
```
	
1. **className**  

	```
	<div className="red"></div>
	```

2. **行内样式不能用字符串来表示，要用样式对象来表示** - 键值对，驼峰写法

	```
	<div style={{color:'red'}}
	```

3. **变量**

	```
	var styleObj = {
		color:'red',
		fontSize:'12px'
	};
	```
	
---


	
### 组件

* **React.createClass** - 生成组件类

	```
	var HelloMessage = React.createClass({
       render: function() {
         return <h1>Hello {this.props.name}</h1>;
       }
    });
    ReactDOM.render(
       <HelloMessage name="John" />,
       document.getElementById('example')
    );
	```
	> * 变量 HelloMessage 就是一个组件类。模板插入 <HelloMessage /> 时，会自动生成 HelloMessage 的一个实例。所有组件类都必须有自己的 render 方法，用于输出组件。
	
	> * 组件类的第一个字母必须大写，否则会报错，比如HelloMessage不能写成helloMessage。另外，组件类只能包含一个顶层标签，否则也会报错。
	
	> * 组件的用法与原生的 HTML 标签完全一致，可以任意加入属性，比如 <HelloMessage name="John"> ，就是 HelloMessage 组件加入一个 name 属性，值为 John。组件的属性可以在组件类的 this.props 对象上获取，比如 name 属性就可以通过 this.props.name 读取。
	
	> * 添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。
	
	```
	var HelloMessage = React.createClass({
        render: function() {
     		return <h1 className="h1">Hello {this.props.name}<p>可以这样吗</p></h1>;        
     	}
   	});
	```
	
* #### props

	rops 就是组件的属性，由外部通过 JSX 属性传入设置，一旦初始设置完成，就可以认为 this.props 是不可更改的，所以不要轻易更改设置 this.props 里面的值


* #### state

	state 是组件的当前状态，可以把组件简单看成一个“状态机”，根据状态 state 呈现不同的 UI 展示。

	一旦状态（数据）更改，组件就会自动调用 render 重新渲染 UI，这个更改的动作会通过this.setState 方法来触发。
	
	* **getInitialState:** 初始化 this.state 的值，只在组件装载之前调用一次。
	
	* **getDefaultProps:** 只在组件创建时调用一次并缓存返回的对象（即在 React.createClass 之后就会调用）。

		
### this.props.children

* **this.props.children** - 它表示组件的所有子节点

	可以把 props 看作是组件的配置属性，在组件内部是不变的，只是在调用这个组件的时候传入不同的属性（比如这里的 name）来定制显示这个组件。
	
### Virtual DOM

### Data Flow


### PropTypes

组件的属性可以接受任意值，字符串、对象、函数等等都可以。有时，我们需要一种机制，验证别人使用组件时，提供的参数是否符合要求。

```
var data = 'this is string';
var Mytitle = React.createClass({
	propTypes:{
		title:React.propTypes.string.isRequired,
	},
	render:function(){
		return <h1>{this.props.title}</h1>
	}
});
ReactDOM.render(
	<Mytitle title={data} />,
	document.getElementById('example')
);
```	

### 参考：
[阮一峰](http://www.ruanyifeng.com/blog/2015/03/react.html)
	

	
	