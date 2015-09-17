### 开发方式

* 类级别的组件开发，即给jQuery命名空间下添加新的全局函数，也称为静态方法。

	```
	jQuery.foo = function(){
		//do something
	}
	```
	
	例如：$.Ajax()、$.extend()
	
* 对象级别的组件开发：即挂在jQuery原型下的方法，这样通过选择器获取的jQuery对象实例也能共享该方法，也称为动态方法。

	```
	$.fn.foo = function(){
		//do something
	};
	这里$.fn === $.prototype
	```
	
* 使用闭包：

	```
	(function($){
	//code...
	})(jQuery)
	```
	
* $.extend(target,[object1],[objectN])

	该方法主要用于合并两个或更多对象的内容(属性)到第一个对象，并返回合并后的第一对象。如果该方法只有一个参数target，则该参数将扩展jQuery的命名空间，即作为静态方法挂在jQuery全局对象下，如jQuery里的$.ajax、$.getJSON全局函数等：
	
	> 值得注意的是：多个对象参数合并时，会破坏第一个对象的结构，所以可传递一个空对象作为第一个参数，如：$.extend({}, object1, object2);
	
* $.fn.extend(target)
	
	
	
```
(function($){

	//参数设置
	var defaults = {
		arg1: 'arg1',
		arg2: 'arg2',
		...
		callback: function(){}
	};	
	
	
	//插件函数
	var Pname = $.fn.pluginName = function(options){
	
		var opts = $.extend({},defaults,options || {});
		
		// 遍历匹配的元素||元素集合，并返回this，以便进行链式调用。
		return this.each(function(){
		
		});
	}
	
	
	
	// 在我们插件容器内，定义一个私有方法
    var privateFunction = function() {
        // code here
    };
    
    //定义公有方法
    Pname.publicFunction = function(){
    }

})(jQuery);
```