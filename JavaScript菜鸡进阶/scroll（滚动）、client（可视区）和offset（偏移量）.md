###Offset

>   偏移量(offset dimension)是javascript中的一个重要的概念。涉及到偏移量的主要是offsetLeft、offsetTop、offsetHeight、offsetWidth这四个属性。当然，还有一个偏移参照——定位父级offsetParent。本文将详细介绍该部分内容
![](https://upload-images.jianshu.io/upload_images/9249356-f3f240e29eda2359.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 定位父级

　　在理解偏移大小之前，首先要理解offsetParent。人们并没有把offsetParent翻译为偏移父级，而是翻译成定位父级，很大原因是offsetParent与定位有关

　　定位父级offsetParent的定义是：与当前元素最近的经过定位(position不等于static)的父级元素，主要分为下列几种情况 

　　【1】元素自身有fixed定位，offsetParent的结果为null

　　当元素自身有[fixed固定定位](http://www.cnblogs.com/xiaohuochai/p/5321487.html#anchor2)时，我们知道固定定位的元素相对于视口进行定位，此时没有定位父级，offsetParent的结果为[null](http://www.cnblogs.com/xiaohuochai/p/5665637.html#anchor3)

　　[注意]firefox浏览器有兼容性问题
```
<div id="test" style="position:fixed"></div>    
<script>
//firefox并没有考虑固定定位的问题，返回<body>，其他浏览器都返回null
console.log(test.offsetParent);
</script>
```
　　【2】元素自身无fixed定位，且父级元素都未经过定位，offsetParent的结果为<body>
```
<div id="test"></div>    
<script>
console.log(test.offsetParent);//<body>
</script>
```
　　【3】元素自身无fixed定位，且父级元素存在经过定位的元素，offsetParent的结果为离自身元素最近的经过定位的父级元素
```
<div id="div0" style="position:absolute;">
    <div id="div1" style="position:absolute;">
        <div id='test'></div>    
    </div>    
</div>
<script>
console.log(test.offsetParent);    //<div id="div1">
</script>
```
　　【4】<body>元素的parentNode是null
```
console.log(document.body.offsetParent);//null
```
## [深入理解定位父级offsetParent及偏移大小](https://www.cnblogs.com/xiaohuochai/p/5828369.html)
##Client

![image.png](https://upload-images.jianshu.io/upload_images/9249356-230aa65e33731619.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# [深入理解客户区尺寸client](https://www.cnblogs.com/xiaohuochai/p/5830053.html)

###注意 client 和 offset 属性都是只读的

#scroll

### 滚动宽高

**scrollHeight**

　　scrollHeight表示元素的总高度，包括由于溢出而无法展示在网页的不可见部分

**scrollWidth**

　　scrollWidth表示元素的总宽度，包括由于溢出而无法展示在网页的不可见部分

###滚动长度
**scrollTop**

　　scrollTop属性表示被隐藏在内容区域上方的像素数。元素未滚动时，scrollTop的值为0，如果元素被垂直滚动了，scrollTop的值大于0，且表示元素上方不可见内容的像素宽度

**scrollLeft**

　　scrollLeft属性表示被隐藏在内容区域左侧的像素数。元素未滚动时，scrollLeft的值为0，如果元素被水平滚动了，scrollLeft的值大于0，且表示元素左侧不可见内容的像素宽度

　　[注意]IE7-浏览器返回值是不准确的

　　【1】没有滚动条时，scrollHeight与clientHeight属性结果相等，scrollWidth与clientWidth属性结果相等


 ```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;"></div>
<script>
//120 120
console.log(test.scrollHeight,test.scrollWidth);
//120 120
console.log(test.clientHeight,test.clientWidth);
</script>
```
【2】存在滚动条时，但元素设置宽高大于等于元素内容宽高时，scroll和client属性的结果相等
```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:1;">
    内容<br>内容<br>
</div>
<script>
//103(120-17) 103(120-17)
console.log(test.scrollHeight,test.scrollWidth);
//103(120-17) 103(120-17)
console.log(test.clientHeight,test.clientWidth);
</script>
```
【3】存在滚动条，但元素设置宽高小于元素内容宽高，即存在内容溢出的情况时，scroll属性大于client属性

　　[注意]scrollHeight属性存在兼容性问题，chrome和safari浏览器中，scrollHeight包含padding-bottom；而IE和firefox不包含padding-bottom
```
<div id="test" style="width: 100px;height: 100px;padding: 10px;margin: 10px;border: 1px solid black;overflow:scroll;font-size:20px;line-height:200px;">
    内容</div>
<script>
//chrome/safari:220(200+10+10)
//firefox/IE:210(200+10)
console.log(test.scrollHeight);
//103(120-17)
console.log(test.clientHeight);
</script>
```
# [深入理解滚动scroll](https://www.cnblogs.com/xiaohuochai/p/5831640.html)

DIV跟着滚动条到底部
![](https://upload-images.jianshu.io/upload_images/9249356-1abc695a448e0128.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-e891c3ddff6723d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




