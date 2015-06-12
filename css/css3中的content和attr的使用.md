####  知识点： content,:after,attr


####  content用法

可以通过content，往html元素里面填写内容

```
.div:after{
	content: "我是通过content添加的内容"；
}
```


#### :after 伪类

* :after,在匹配的元素内容之后插入新内容

* :before，在匹配的元素内容 之前插入新内容

> 所有主流浏览器都支持，但是ie8及之前的版本，需要声明<!DOCTYPE>。
	
	
#### attr

如果不想把content里面的内容写死，可以通过attr表达式来从页面元素中动态的获取内容：

```
/* <div data-role="girl"></div> */
```

```
div:after{
	content:attr(data-role);
}
```
> ttr属性通常和自定义属性data-配合使用，因为传统的其它属性虽然也能存值，但通常不适合存放表达性文字。

content还可以进行字符串拼接：

```
div:after{
	content: "role:" attr(data-role);
}
```



#### demo

[table自适应布局](https://github.com/yuhualee/css/blob/master/demo/table%E8%87%AA%E9%80%82%E5%BA%94%E5%B8%83%E5%B1%80.html)