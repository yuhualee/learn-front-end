Date: 2014-08-30  
Title:   
Published: true  
Type: post  
Excerpt:   

# js动画
##### 代码一：
```
var ele = document.getElementById('div1');
	// var begin = 800;
	var begin = ele.offsetLeft;
	var target = 600;
	var change = target - begin;
	var duration = 500;
	var interval = 20;
	var times = 0;   //time += interval;
	function step(){
		times += interval;
		if(times<=duration){
			ele.style.left = times/duration*change+begin+"px";
		}else if(times>duration){
			ele.style.left = target+"px";
			window.clearInterval(step);
		}	
	}
	window.setInterval(step,interval);
```
##### 代码二
```
```




window.getComputedStyle(ele,"before").color;


www.zhufengpeixun.cn/tween

## 作业 ：向左向右