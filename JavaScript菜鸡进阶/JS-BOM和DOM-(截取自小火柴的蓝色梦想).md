##BOM
##### 定时器

语法：

setTimeout(code,millisec);
setInterval(code,millisec[,"lang"])
它们都有两个参数，一个是将要执行的代码字符串，还有一个是以毫秒为单位的时间间隔，当过了那个时间段之后就将执行那段代码。
这两个函数的区别就在于，setInterval在执行完一次代码之后，经过了那个固定的时间间隔，它还会自动重复执行代码，而setTimeout只执行一次那段代码。
每5秒alert一次时间
  
      var showTimes=setInterval("showTime()",    5000);
      function showTime()
      {
    var today = new Date();
    alert("The time is: " + today.toString());
      }
setTimeout也可以实现，代码如下：

        var showTimes=null;
      showTime();
      function showTime()
      {
    var today = new Date();
    alert("The time is: " + today.toString());
    showTimes=setTimeout("showTime()", 5000);
      }
>这样写是不是看起来没有什么区别，但是setTimeout方法不会每隔5秒钟就执行一次showTime函数，它是在每次调用setTimeout后过5秒钟再去执行showTime函数。这意味着如果showTime函数的主体部分需要1秒钟执行完，那么整个函数则要每6秒钟才执行一次。而setInterval却没有被自己所调用的函数所束缚，它只是简单地每隔一定时间就重复执行一次那个函数。

>所以这两个函数需根据不同的情景去使用，如果需要在每隔一个固定的时间间隔后就精确地执行某动作，那么最好使用setInterval，而如果不想由于连续调用产生互相干扰的问题，尤其是每次函数的调用需要繁重的计算以及很长的处理时间，那么最好使用setTimeout。

setInterval和setTimeout都返回定时器对象标识符，用于clearInterval和clearTimeout调用
eg:

clearTimeout(showTimes) //清除已设置的setTimeout对象
clearInterval(showTimes) //清除已设置的setInterval对象
#### setTimeout()和clearTimeout()

在指定的毫秒数到达之后执行指定的函数，只执行一次

```javascript
// 创建一个定时器，1000毫秒后执行，返回定时器的标示
var timerId = setTimeout(function () {
  console.log('Hello World');
}, 1000);

// 取消定时器的执行
clearTimeout(timerId);
```

#### setInterval()和clearInterval()

定时调用的函数，可以按照给定的时间(单位毫秒)周期调用函数

```javascript
// 创建一个定时器，每隔1秒调用一次
var timerId = setInterval(function () {
  var date = new Date();
  console.log(date.toLocaleTimeString());
}, 1000);

// 取消定时器的执行
clearInterval(timerId);
```
>[注意]HTML5标准规定，setTimeout的最短时间间隔是4毫秒；setInterval的最短间隔时间是10毫秒，也就是说，小于10毫秒的时间间隔会被调整到10毫秒
>
>　　大多数电脑显示器的刷新频率是60HZ，大概相当于每秒钟重绘60次。因此，最平滑的动画效的最佳循环间隔是1000ms/60，约等于16.6ms
>
>　　为了节电，对于那些不处于当前窗口的页面，浏览器会将时间间隔扩大到1000毫秒。另外，如果笔记本电脑处于电池供电状态，Chrome和IE10+浏览器，会将时间间隔切换到系统定时器，大约是16.6毫秒

###运行机制
**setTimeOut**
![](https://upload-images.jianshu.io/upload_images/9249356-b10e18662f0d08f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如图所示，尽管在255ms处添加了定时器代码，但这时候还不能执行，因为onclick事件处理程序仍在运行。定时器代码最早能执行的时机是在300ms处，即onclick事件处理程序结束之后


**setInterval**

![](https://upload-images.jianshu.io/upload_images/9249356-1fd48cb8bda4e348.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>setInterval()的问题
 
　　使用setInterval()的问题在于，定时器代码可能在代码再次被添加到队列之前还没有完成执行，结果导致定时器代码连续运行好几次，而之间没有任何停顿。而javascript引擎对这个问题的解决是：当使用setInterval()时，仅当没有该定时器的任何其他代码实例时，才将定时器代码添加到队列中。这确保了定时器代码加入到队列中的最小时间间隔为指定间隔

　　但是，这样会导致两个问题：
1、某些间隔被跳过；
2、多个定时器的代码执行之间的间隔可能比预期的小

　　假设，某个onclick事件处理程序使用setInterval()设置了200ms间隔的定时器。如果事件处理程序花了300ms多一点时间完成，同时定时器代码也花了差不多的时间，就会同时出现跳过某间隔的情况
例子中的第一个定时器是在205ms处添加到队列中的，但是直到过了300ms处才能执行。当执行这个定时器代码时，在405ms处又给队列添加了另一个副本。在下一个间隔，即605ms处，第一个定时器代码仍在运行，同时在队列中已经有了一个定时器代码的实例。结果是，在这个时间点上的定时器代码不会被添加到队列中

>   迭代setTimeout
>为了避免setInterval()定时器的问题，可以使用链式setTimeout()调用
```
setTimeout(function fn(){
    setTimeout(fn,interval);
},interval);
```
　　这个模式链式调用了setTimeout()，每次函数执行的时候都会创建一个新的定时器。第二个setTimeout()调用当前执行的函数，并为其设置另外一个定时器。这样做的好处是，在前一个定时器代码执行完之前，不会向队列插入新的定时器代码，确保不会有任何缺失的间隔。而且，它可以保证在下一次定时器代码执行之前，至少要等待指定的间隔，避免了连续的运行

<br>


- - -
##DOM
for循环是在页面加载的时候,执行完毕了 
  
       for(var k=0;k<5;k++){
                  }
         console.log(k);//  k=5
事件是在触发的时候,执行的

两种状态的样式变换可以用.toggle()方法
```      
 my$("dv").classList.toggle('cls');
      this.value = my$("dv").className!="cls"? "隐藏" : "显示";
```

  设置标签中的文本内容,应该使用textContent属性,谷歌,火狐支持,IE8不支持
   设置标签中的文本内容,应该使用innerText属性,谷歌,火狐,IE8都支持

  如果这个属性在浏览器中不支持,那么这个属性的类型是undefined
  判断这个属性的类型 是不是undefined,就知道浏览器是否支持

#####在html标签中添加的自定义属性,如果想要获取这个属性的值,需要使用getAttribute("自定义属性的名字")才能获取这个属性的值

  * 文档:document
  * 元素:页面中所有的标签,元素---element,  标签----元素---对象
  * 节点:页面中所有的内容(标签,属性,文本(文字,换行,空格,回车)),Node
  * 根元素:html标签

####元素按标签算，节点包括里面的内容
* 节点的属性:(可以使用标签--元素.出来,可以使用属性节点.出来,文本节点.点出来)
  * nodeType:节点的类型:1----标签,2---属性,3---文本
  * nodeName:节点的名字:标签节点---大写的标签名字,属性节点---小写的属性名字,文本节点----#text
  * nodeValue:节点的值:标签节点---null,属性节点---属性值,文本节点---文本内容
