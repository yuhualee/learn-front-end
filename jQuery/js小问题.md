1. **jquery对象本身是一个集合。所以如果jquery对象要转换为dom对象则必须取出其中的某一项，一般可通过索引取出。**

	```
	$("#msg")[0];
	$("div").eq(1)[0];
	$("div").get()[1];
	$("td")[5]
	```

	这些都是dom对象，可以使用dom中的方法，但不能再使用Jquery的方法。
	
	```
	$("#msg").html();
	$("#msg")[0].innerHTML;
	$("#msg").eq(0)[0].innerHTML;
	$("#msg").get(0).innerHTML;
	```
	
	js和jquery相互转换：
	
	```
	var id = document.getElementById('id');   //js对象
	var $id = $(id);   //转化为$对象
	var j_id = $(id).get(0);
	```
	
	