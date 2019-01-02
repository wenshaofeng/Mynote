#执行上下文
#####何为执行上下文
我们总结一下，在“准备工作”中完成了哪些工作：

- 变量、函数表达式——变量声明，默认赋值为undefined；
- this——赋值；
- 函数声明——赋值；
这三种数据的准备情况我们称之为“执行上下文”或者“执行上下文环境”。
![执行上下文.png](https://upload-images.jianshu.io/upload_images/9249356-873a604bd58fbf1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####作用域与执行上下文环境
![](https://upload-images.jianshu.io/upload_images/9249356-c2ca29e3c09f8354.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-d5dd5382e4d6a7ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>作用域只是一个“地盘”，一个抽象的概念，其中没有变量。要通过作用域对应的执行上下文环境来获取变量的值。同一个作用域下，不同的调用会产生不同的执行上下文环境，继而产生不同的变量的值。所以，作用域中变量的值是在执行过程中产生的确定的，而作用域却是在函数创建时就确定了。

所以，如果要查找一个作用域下某个变量的值，就需要找到这个作用域对应的执行上下文环境，再在其中寻找变量的值。

##自由变量
![](https://upload-images.jianshu.io/upload_images/9249356-23a719c6206874b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####自由变量取值
![](https://upload-images.jianshu.io/upload_images/9249356-f6b4afd9cc2df808.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>要到创建这个函数的那个作用域中取值——是“创建”，而不是“调用”，切记切记——其实这就是所谓的“静态作用域”。
>
>对于本文第一段代码，在fn函数中，取自由变量x的值时，要到哪个作用域中取？——要到创建fn函数的那个作用域中取——无论fn函数将在哪里调用。


#闭包
 JavaScript闭包无处不在，你只需要能够识别并拥抱它。

### 闭包的定义：

当函数可以记住，并且访问所在的词法作用域时，就产生了闭包。即使函数是在当前词法作用域之外执行。
>《Javascript高级程序设计》上对闭包的定义是：有权限访问另一个函数作用域中的变量的函数。也就是说，闭包是一个函数，那什么样的函数才能是闭包呢？他能访问另一个函数作用域中的变量。这样的解释让我们直接想起了一个函数的内部函数，因为根据作用域链的规则，只有嵌套的函数才能达到这个效果。并且这个闭包函数是作为父函数的返回值返回，而且这个闭包函数通常是个匿名函数。

闭包demo：

```
function foo(){
	var a = 2;
	function bar(){
		console.log(a)
	}

	return bar
}

var baz = foo();
baz(); //2 ，这就是闭包

```

1 .闭包神奇之处：阻止内部作用域销毁。在函数允许结束之后，还保留对该函数作用域的引用。
2. 无论通过何种手段将内部函数传递到所在的词法作用域以外，它都会持有对原始定义作用 域的引用，无论在何处执行这个函数都会使用闭包。


3.  你就会看到闭包在这些函数中的应用。在定时器、事件监听器、 Ajax 请求、跨窗口通信、Web Workers 或者任何其他的异步（或者同步）任务中，只要使 用了回调函数，实际上就是在使用闭包！

### 循环和闭包
循环闭包最常见的例子
```
for(var i=0;i<=5;i++){
	// 此时作为参数i值为当前迭代值。
	setTimeout(function timer(){
		//回调函数调用最终i的值。
		console.log(i);
	},i * 1000) //   结果：每隔一秒输出一个6 
}
```
回调函数会在for循环结束后再执行，此时i的值为6 
为什么输出是6，因为timer函数能够共享变量i的副本。访问的是全局作用域。根据作用域的工作原理，尽管五个函数是在各个迭代中分别定义的，但是它们都被封闭在一个共享的全局作用域中，因此实际上只有一个i

**解决办法，为i创建一个局部作用域和变量存储i的值。**

```
for(var i=0;i<=5;i++){
	(function(j){
		setTimeout(function timer(){
			console.log(j);
		}, j * 1000);
	})(i)
}
```
在每次迭代都会产生一个新的作用域，延迟函数的回调在新的作用域内访问我们提供的变量。
