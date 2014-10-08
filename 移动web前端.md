Date: 2014-09-14  
Title:移动web前端   
Published: true  
Type: post  
Excerpt:   

参考：

# 移动端web前端入门

### 1. webkit内核
#### 1.1、首先我们来看看webkit内核中的一些私有的meta标签，这些meta标签在开发webapp时起到非常重要的作用

```
<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0;" name="viewport" />
<meta content="yes" name="apple-mobile-web-app-capable" />
<meta content="black" name="apple-mobile-web-app-status-bar-style" />
<meta content="telephone=no" name="format-detection" />
```

第一个meta标签表示：强制让文档的宽度与设备的宽度保持1:1，并且文档最大的宽度比例是1.0，且不允许用户点击屏幕放大浏览；
第二个meta标签是iphone设备中的safari私有meta标签，它表示：允许全屏模式浏览；
第三个meta标签也是iphone的私有标签，它指定的iphone中safari顶端的状态条的样式；
第四个meta标签表示：告诉设备忽略将页面中的数字识别为电话号码；

### 2.HTML5标签的应用
#### 2.1 html5语义化标签   
**section:**独立的一个区块，比如：页眉、页脚、章节，通常由内容和标题组成。    
**article:**可以理解为特殊的section，独立的，完整的内容区块。比如：一条评论，一篇文章，一篇帖子。   
**nav:**用于放页面上链接的团体   
**aside:**页面主体内容的辅助区域，可有可无。  
**header:**标签定义文档的页眉，通常是一些引导和导航信息，不局限于头部。  
**hgrounp:**放置标题元素（h1-h6）进行组合.   
**footer:**页面或section的底部信息。  

**参考：**  
[html5语义化标签](http://www.rainleaves.com/html/1338.html)   
[html5布局](http://www.rainleaves.com/html/1701.html);

#### 2.2表单
#### 2.3属性
#### 2.4新功能
### 3.放弃的css属性
##### 3.1 放弃float。可作用display:inline-block或css3属性来代替。  

### 4.css3的使用

##### 4.1 自适应布局

为适应不同尺寸的屏幕，建立不要把容器的宽度定死，可以用百分比来定宽。并且不再像pc端那样，全用float来布局，因为float会破坏文档流。而且，由于不再考虑兼容性问题，css3为我们提供了更强大方法来解决布局的问题：   
**方法二：webkit-box**  
**方法二：box-flex**

### 5. 移动端性能优化
1. 图片进行压缩，大图换成小图。  
2. 数据离线化，可以全用html5的localStorage。
3. 图片使用css sprites或data uri
4. 尽量全用css3代替图片
5. 使用css3动画代替js动画
6. 保证html结构简洁，降低层级数。

### 6. 基础样式 
**字体设置：**建议使用无衬字体，
     
```
body {   
    font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif;   
}
```
> 英文字体设置为Helvetica，ios中使用，
> 中文字体使用：STHeiTi华文黑体，
> sans-serif：宋体，最后以无衬线字体结尾，保证在不同的设备上都会显示。
   
```
a, img {
    -webkit-touch-callout: none; /* 禁止长按链接与图片弹出菜单 */
}
html, body {
    -webkit-user-select: none;   /* 禁止选中文本（如无文本选中需求，此为必选项） */
    user-select: none;
}
```
