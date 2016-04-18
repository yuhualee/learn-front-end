* **json**

	javascript Object Notation 


1. json对象格式的字符串，严格的对象格式的字符串，它是一种数据
> var strJson = {"name":"李玉华","age":27};
2. 它是跨语言，在每一种语言里，都有把json字符串转化为当前这种语言的对象（数据）的方法。
>* JSON.parse();  //把Json字符串转为js对象。
>* JSON.stringify();  //把对象序列化成Json字符串
>
```
var obj = {name:"李玉华",age:28,item1:null,item2:undefined};
var a = JSON.stringify(obj);
console.log(a);
console.log(JSON.parse(a));
> ```
3. eval，相当于在单独的一个空间里面进行了解析 ~~?????????~~
>
```
var strJson = {"name":"李玉华","age":"34"};
//var obj = eval(strJson); 有语法错误
var obj = eval("("+strJson+")");
```
> {}在Js里面有两个意义：1. 脚本块； 2. 在赋值运算符的右边才表示对象
> 必须把{}当成值来使用的时候，才是对象，所有值放在（）里面就会当成一个值来解释。
4. Json的兼容性问题解决
> IE6,7不支持
>
```
function JSONParse(str){
	//if(JSON){}这种方法不能用，不能直接判断一个变量，如果一个变量没有被定义，它会报语法错误
	//方法一：
	if(typeof JSON!="undefined"){
		return JSON.parse(str);
	}else{
		return eval("("+str+")");
	}
	//方法二：
	if(window.JSON){//window.JSON不是当作变量来用，而是当作属性，变量没有被定义不能用，但是属性可以用。
		return JSON.parse(str);
	}else{
		return eval("("+str+")");
	}
	//方法三：
	try{
		return JSON.parse(str);
	}catch(e){
		return eval("("+str+")");
	}
}
```


## json方法

* **解析json字符串**

	```
	var jsJson = JSON.parse(jsonString);
	```
	
* **将对象转化为json**

	```
	var foo = {};
	foo.bar = "new property";
	foo.baz = 3;
	var jsonString = JSON.stringify(foo);
	```
	
	```
	function censor(key, value) {
  if (typeof(value) == "string") {
    return undefined;
  }
  return value;
}
var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
var jsonString = JSON.stringify(foo, censor);
	```

* **JSON.parse**

	**JSON.parse()**  - 方法可以将一个 JSON 字符串解析成为一个 JavaScript 值。在解析过程中，还可以选择性的篡改某些属性的原始解析值。
	
	```
	JSON.parse('{}');              // {}
	JSON.parse('true');            // true
	JSON.parse('"foo"');           // "foo"
	JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
	JSON.parse('null');            // null
	```

* **JSON.stringify**

	JSON.stringify() 方法可以将任意的 JavaScript 值序列化成 JSON 字符串。
	
	```
	JSON.stringify({});                        // '{}'
	JSON.stringify(true);                      // 'true'
	JSON.stringify("foo");                     // '"foo"'
	JSON.stringify([1, "false", false]);       // '[1,"false",false]'
	JSON.stringify({ x: 5 });                  // '{"x":5}'
	//
	JSON.stringify({x: 5, y: 6});              
	// '{"x":5,"y":6}' 或者 '{"y":6,"x":5}' 都可能
	JSON.stringify([new Number(1), new String("false"), new Boolean(false)]); 
	// '[1,"false",false]'
	JSON.stringify({x: undefined, y: Object, z: Symbol("")}); 
	// '{}'
	JSON.stringify([undefined, Object, Symbol("")]);          
	// '[null,null,null]' 
	JSON.stringify({[Symbol("foo")]: "foo"});                 
	// '{}'
	JSON.stringify({[Symbol.for("foo")]: "foo"}, [Symbol.for("foo")]);
	// '{}'
	JSON.stringify({[Symbol.for("foo")]: "foo"}, function (k, v) {
	  if (typeof k === "symbol"){
	    return "a symbol";
	  }
	});
	// '{}'  
	// 不可枚举的属性默认会被忽略：
	JSON.stringify( Object.create(null, { x: { value: 'x', enumerable: false }, 	y: { value: 'y', enumerable: true } }) );
	// '{"y":"y"}'
	```




