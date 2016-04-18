### 开发方式

[参考](http://javascript.ruanyifeng.com/jquery/plugin.html#toc0)

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
	
### jQuery组件

1. **闭包**

	```
	$(function($){
	})(jQuery);
	```
	> 这是来自jQuery官方的插件开发规范要求，使用这种编写方式有什么好处呢？
	> 
	> a) 避免全局依赖。
	> 
	> b) 避免第三方破坏。
	> 
	> c) 兼容jQuery操作符'$'和'jQuery '

* **扩展**

	* **$.extend - 用于扩展自身方法，例：$.ajax、$.getJSON**
	
		jQuery.extend(): Merge the contents of two or more objects together into the first object.(把两个或者更多的对象合并到第一个当中)；
	
	* **$.fn.extend - 用于扩展jQuery类，包括方法和对jQuery对象的操作**
	
		jQuery.fn.extend():Merge the contents of an object onto the jQuery prototype to provide new jQuery instance methods.(把对象挂载到jQuery的prototype属性，来扩展一个新的jQuery实例方法)
		
		 `jQuery.fn = jQuery.prototype` 即指向jQuery对象的原型链，对其它进行的扩展，作用在jQuery对象上面；一般用此方法来扩展jQuery的对象插件  
	
* **选择器**

	*  尽量使用Id选择器，jQuery的选择器使用的API都是基于getElementById或getElementsByTagName，因此可以知道 效率最高的是Id选择器，因为jQuery会直接调用getElementById去获取dom，而通过样式选择器获取jQuery对象时往往会使用 getElementsByTagName去获取然后筛选。
	
	* 样式选择器应该尽量明确指定tagName, 如果开发人员使用样式选择器来获取dom，且这些dom属于同一类型，例如获取所有className为jquery的div，那么我们应该使用的写法 是$('div.jquery')而不是$('.jquery')，这样写的好处非常明显，在获取dom时jQuery会获取div然后进行筛选，而不是 获取所有dom再筛选。
	
	* 避免迭代，很多同学在使用jQuery获取指定上下文中的dom时喜欢使用迭代方式，如$('.jquery .child')，获取className为jquery的dom下的所有className为child的节点，其实这样编写代码付出的代价是非常大 的，jQuery会不断的进行深层遍历来获取需要的元素，即使确实需要，我们也应该使用诸如$(selector,context), $('selector1>selector2'), $(selector1).children(selector2), $(selctor1).find(selector2)之类的方式。


* **组件1**

	* 容器：一个即时执行函数
	
		根本上来说，每个插件的代码是被包含在一个即时执行的函数当中，如下：
		
		```
		;(function($){
			//code
		})(jQuery);
		```
		
	* 插件： 一个函数
	
		```
		;(function($){
			$.fn.pluginName(options){
				//code...
				return this;
			}
		})(jQuery);
		```
		
	* 多个元素：理解Sizzle
	
		这里我添加了一小段代码，它让你的插件代码为多元素集合中每个元素单独地起作用：
		
		```
		;(function($){
			// 向jQuery中被保护的“fn”命名空间中添加你的插件代码，用“pluginName”作为插件的函数名称
			$.fn.pluginName(options){
				// 返回“this”（函数each（）的返回值也是this），以便进行链式调用。
				return this.each(function(){
					// 此处运行代码，可以通过“this”来获得每个单独的元素
				});
			}
		})(jQuery);
		```
		
	* 功能：公有方法和私有方法
	
	[未完待续：](http://blog.jobbole.com/30550/)


* **组件2**

	* 开始


		```
		$.fn.myPlugin = function(){
			this.css('color','#f90');
			$(this).each(function(){
				$(this).append(' ' + $(this).attr('href'));
			});
		}
		$('a').myPlugin();
		```
		
	* 接收参数
	
		```
		$.fn.setCss = function(options){
			var defaults = {
				'color' : '#f90',
				'fontSize' : '14px'
			};
			var settings = $.extend(defaults,options || {});
			return this.css({
				'color': settings.color,
				'fontSize' : settings.fontSize
			});
		}
		<!--调用插件-->
		$('a').setCss({'color':'#f00'});
		```
		
	* 保护好默认参数
	
		将一个新的空对象做为$.extend的第一个参数，defaults和用户传递的参数对象紧随其后，这样做的好处是所有值被合并到这个空对象上，保护了插件里面的默认值。
	
		```
		$.fn.setCss = function(options){
			var defaults = {
				'color' : '#f90',
				'fontSize' : '14px'
			};
			var settings = $.extend({},defaults,options || {});  //将一个空对象作为第一个参数
			return this.css({
				'color': settings.color,
				'fontSize' : settings.fontSize
			});
		}
		<!--调用插件-->
		$('a').setCss({'color':'#f00'});
		```
		
	* 面向对象的插件开发
	
		```
		//定义Beautifier的构造函数
		var Beautifier = function(ele,opts){
			this.element = ele;
			this.defaults = {
				'color' : '#f00',
				'fontSize' : '14px',
				'textDecoration' : 'none'
			};
			this.options = $.extend({},this.defaults,opts || {})
		}
		//定义Beautifier的方法
		Beautifier.prototype = {
			beautify : function(){
				return this.element.css({
					'color' : this.options.color,
				'fontSize' : this.options.fontSize,
				'textDecoration' : this.options.textDecoration
				});
			}
		}
		//在插件中使用Beautifier对象
		$.fn.myPlugin = function(options){
			var beautifier = new Beautifier(this,options);
			return beautifier.beautify()
		}
		$('a').myPlugin();
		```
		
	* 用自调用匿名函数包裹你的代码
	
		```
		;(function(){
			//body...
		})();
		```
		当我们这样做之后，window等系统变量在插件内部就有了一个局部的引用，可以提高访问速度会有些许性能的提升

		最后我们得到一个非常安全结构良好的代码：
		
		```
		;(function($,window,document,undefined){
			//code....
		})(jQuery,window,document);
		```
		> 而至于这个undefined，稍微有意思一点，为了得到没有被修改的undefined，我们并没有传递这个参数，但却在接收时接收了它，因为实际并没有传，所以‘undefined’那个位置接收到的就是真实的'undefined'了。是不是有点hack的味道，值得细细体会的技术
