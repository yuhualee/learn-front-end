Date: 2014-09-12  
Title:toString()方法   
Published: true  
Type: post  
Excerpt:   

# javascript中的toString()方法


### 1. 基本数据类型的toString方法
##### 1. Boolean.toString()
可以把一个逻辑转换成字符串，并返回结果。

```
true.toString();    //true;
```
##### 2. Array.toString() 

可以把一个Number对象转化成字符串，并返回结果；

Number.toString(radix);其中radix表示数字的基数，使 2 ~ 36 之间的整数。省略，则为10.

```
var a = 11;
console.log(a.toString());   //11
console.log(a.toString(2));  //1011
console.log(a.toString(3));  //102
console.log(a.toString(8));  //13
```
##### 3. 可以把数组转化成字符串，并返回结果，返回值与没有参数的 join() 方法返回的字符串相同。

```
var a = ["lyh","Love","baby"];
console.log(a.toString());  
//输出：lyh,Love,baby
```

##### 4. Date.toString()
把Date对象转换成字符串，采用本地时间。

```
var today = new Date()
console.log(today);
console.log(today.toString());
console.log(today.toLocaleString());
```
> * Date {Fri Sep 26 2014 16:56:42 GMT+0800 (CST)}
> * Fri Sep 26 2014 16:56:42 GMT+0800 (CST)
> * 2014/9/26 下午4:56:42

##### 5. Function.toString()
把函数转化成字符串。
