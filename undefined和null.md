# undefined、null和NAN

## undefined
**undefined属性用于存放undefined的值。**

1. js在预解析的时候，对var定义的变量会赋值undefined。
2. 变量在声明时，没有初始化，则会赋值为undefined。
3. 当尝试读取不存在的对象属性时也会返回 undefined。

**如下出现未定义的情况：**

> ```
var a = {};
alert(a.b);
alert(typeof b);
var c;
alert(c);
var d = undefined;
alert(d);
```

## null
1. 直接赋值为null，则代表此变量被初始化空值。

## NAN
**NAN:**not a number,不是一个数，它的类型是number。


## undefined和null的区别
1. 类型：undefined是undefined类型的，null是object类型的。
2. 来源：undefined表示一个未声明的变量，或者已声明未赋值的变量，或一个并不存在的对象属性。
3. undefined是无效的对象，null是空对象。
4. 如果是undefined，代表着未定义；如果被赋值为null，则代表此变量被初始化空值。
5. 只能用"==="来判断一个某个值是否未定义，因为 “==” 运算符认为undefined==null。测试：
> ```
alert(undefined==null);   //为true。
alert(undefined===null);   //为false。
alert(typeof undefined == typeof null)   //false
```
