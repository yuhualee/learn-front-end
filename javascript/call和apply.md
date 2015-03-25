Date: 2014-08-24  
Title:   
Published: true  
Type: post  
Excerpt: 
# call和apply
## 定义
1. **定义：**调用一个对象的一个方法，以另一个对象替换当前对象。
2. **参数：**call(thisObj,arg1,agr2...)
> thisObj：可选项，将被用作当前对象的对象
> arg1，arg2...可选项，将被传递方法参数序列
3. **说明：**call方法可以用来代替另一个对象调用一个方法。call方法可以将一个函数的对象上下文从初始的上下文改变为thisObj指定的新对象。如果没有thisObj，那么Global对象被用作thisObj。

## 边走边看
#### 1.调用方法
##### obj1.method1.call(obj2,arg1,arg2):call的作用就是把obj1的方法放到obj2上使用，后面的arg作为参数传入。
如下：

```
function add(a,b){alert(a+b);}
function sub(a,b){alert(a-b);}
add.call(sub,3,1);
```
> 如果把add的对象当作window，那么就是window.add.call(sub,3,1)，也就是sub.add(3,1)。其实就是把add当成sub的一个方法调用。

#### 2.继承

```
funciont class1(){
	this.showTxt = function(txt){
		alert(txt);
	}
}
function class2(){
	class1.call(this);
}
var c2 = new class2();
cs.showTxt("cc");
```
> 这样class1.call(this)的意思：此时的this指向class2，也就是class2中就是有了class1的属性和方法，c2对象就能直接调用class2的方法和属性了。执行结果就是：alert("cc");

#### 3. 改变this
##### 例1：

```
var test = 111;
function _add()  
{  
    this.test = 444;  //注释①
    console.log(this.test);  
}  
function _sub()
{  
    this.test = 222;
    console.log(this.test);  
}  
_add();//弹出444          
_sub();//弹出222
_add.call(_sub);
console.log(_sub.test);
```  
##### 例2：
```
ar test = 111;
function _add()  
{  
    //this.test = 444;  //注释①
    console.log(this.test);  
}  
function _sub()
{  
    this.test = 222;
    console.log(this.test);  
}  
_add();//弹出111,_add中this指向window      
var d=new _sub();//_sub中this指向d
console.log(test);//弹出111  ！！！！！！！！
_sub();//弹出222,_sub中的this继续指向window
console.log(test);//执行_sub()的结果！！！！！！！！
_add.call(_sub);//_add中this指向_sub,_sub无test属性,undefined
```
##### 例3：
```
var test = 111;
function _add()  
{  
    this.test = 444;  //注释①
    console.log(this.test);  
}  
function _sub()
{  
    this.test = 222;
    console.log(this.test);  
}  
_add();//弹出444,_add中this指向window,则window.test变成444      
var d=new _sub();//_sub中this指向d，弹出222
console.log(test);//弹出444，第一步执行结果
_sub();//弹出222,_sub中的this继续指向window
console.log(test);//执行_sub()的结果222
_add.call(_sub);//_add中this指向_sub,相当于_sub.test = 444;console.log(_sub.test);注意，这里的_sub.test和_sub里面的this.test并不是同一个。
```
##### 例4：
```
var test = 111;
function _add()  
{  
    this.test = 444;  //注释①
    this();
    console.log(this.test);  
}  
function _sub()
{  
    this.test = 222;
    console.log(this.test);  
}  
_add.call(_sub);
```
> 上面的代码相当于
>
```
function _add(){
  _sub.test = 444;
  _sub(); //弹出222，改变window.test的值为222
  //function _sub(){
    //window.test = 222;
    //console.log(_window.test);
  //}
  console.log(_sub.test);//弹出444
}
```


## call和apply的区别
##### call和apply其实是一样的，唯一的区别在于他们调用参数，call是一个一个的调用 ，而apply是是调用一个数组，或者类数组。

```
foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments) == this.foo(arg1, arg2, arg3)
```
> call, apply方法区别是,从第二个参数起, call方法参数将依次传递给借用的方法作参数, 而apply直接将这些参数放到一个数组中再传递, 最后借用方法的参数列表是一样的.