**内容转自以下博文**
>#### [深入理解this机制系列第一篇——this的4种绑定规则](https://www.cnblogs.com/xiaohuochai/p/5735901.html)
>#### [深入理解this机制系列第二篇——this绑定优先级](https://www.cnblogs.com/xiaohuochai/p/5737435.html)
>#### [深入理解this机制系列第三篇——箭头函数](https://www.cnblogs.com/xiaohuochai/p/5737876.html)
>###[函数的几种调用方式](https://www.cnblogs.com/lisha-better/p/5684844.html)
>### [彻底理解js中this的指向，不必硬背。](https://www.cnblogs.com/pssp/p/5216085.html)

# this的取值
在函数中this到底取何值，是在**函数真正被调用执行**的时候确定的，函数定义的时候确定不了。因为this的取值是执行上下文环境的一部分，每次调用函数，都会产生一个新的执行上下文环境。
>图解

![](https://upload-images.jianshu.io/upload_images/9249356-e785eae1f1a10643.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# this的4种绑定规则
>默认绑定
- 全局环境中，this默认绑定到window
- 函数独立调用时，this默认绑定到window
- 被嵌套的函数独立调用时，this默认绑定到window
- **[IIFE](http://www.cnblogs.com/xiaohuochai/p/5731016.html)立即执行函数实际上是函数声明后直接调用执行**
- 闭包（类似地，test()函数是独立调用，而不是方法调用，所以this默认绑定到window）
>**由于闭包的this默认绑定到window对象，但又常常需要访问嵌套函数的this，所以常常在嵌套函数中使用var that = this，然后在闭包中使用that替代this，使用作用域查找的方法来找到嵌套函数的this值**
```
var a = 0;
function foo(){
    var that = this;
    function test(){
        console.log(that.a);
    }
    return test;
};
var obj = {
    a : 2,
    foo:foo
}
obj.foo()();//2
```
>隐式绑定

一般地，被直接对象所包含的函数调用时，也称为方法调用，this隐式绑定到该直接对象
>隐式丢失

隐式丢失是指被隐式绑定的函数丢失绑定对象，从而默认绑定到window。这种情况容易出错却又常见

>显式绑定

通过call()、apply()、bind()方法把对象绑定到this上，叫做显式绑定。对于被调用的函数来说，叫做间接调用

# this绑定的优先级
![](https://upload-images.jianshu.io/upload_images/9249356-9583cb4fbc015995.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 对象
####[深入理解javascript原型和闭包](https://www.kancloud.cn/kancloud/javascript-prototype-closure)
![](https://upload-images.jianshu.io/upload_images/9249356-8d52db042c81c7ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


>创建对象的几种方式

#### 1.工厂模式
 ```
function createPerson(name , age , job ){
  var o = new Object()
  o.name = name
  o.age = age 
  o.job = job
o.sayName = function() {
      alert(this.name)
    }
  return o 
}
var person1 = createPerson('John' , 21, 'doctor' )
var person2 =createPerson('Greg' , 27 , 'worker' )
```
#### 2.构造函数模式
```
function Person(name , age , job ){
 this.name = name
  this.age = age 
  this.job = job
this.sayName = function() {
      alert(this.name)
    }
}
var person1 = new Person('John' , 21, 'doctor' )
var person2 = new Person('Greg' , 27 , 'worker' )
```


构造函数创建与工厂模式相比:
>1.没有显式创建对象
>2.直接将属性和方法赋给了this对象  
>3.没有return 语句

new一个对象的过程
>创建一个新对象
>将构造函数的作用域赋给新对象（this指向了这个新对象）
>给对象添加属性
>return新对象

####3.原型模式创建
```
 function Person () {}
    Person.prototype.name = 'John'
    Person.prototype.age = 24
    Person.prototype.job = 'Doctor'
    Person.prototype.sayName = function () {
      alert(this.name)
    }
    var person1 = new Person()
    person1.sayName()//'John'

    var person2 = new Person()
    person2.sayName()  //'John'
    
    alert(person1.sayName == person2.sayName)  //true
```
# 理解原型
![](https://upload-images.jianshu.io/upload_images/9249356-a397f751c59db8cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


- prototype
![](https://upload-images.jianshu.io/upload_images/9249356-74c546163c9ca476.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-1364e3470bbb15b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 隐式原型\_\_proto__
![](https://upload-images.jianshu.io/upload_images/9249356-8222023c4e488b9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
##### 实例对象增加/删除属性
![](https://upload-images.jianshu.io/upload_images/9249356-00fef99fdcdf60fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##### 重写原型对象
![](https://upload-images.jianshu.io/upload_images/9249356-f3bb5bf802cc6f3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##### 函数也是对象
如果把函数Foo当成实例对象的话，其构造函数是Function()，其原型对象是Function.prototype；类似地，函数Object的构造函数也是Function()，其原型对象是Function.prototype
```
function Foo(){};
var f1 = new Foo;
console.log(Foo.__proto__ === Function.prototype);//true
console.log(Object.__proto__ === Function.prototype);//true
```

![](https://upload-images.jianshu.io/upload_images/9249356-6fe91ad094da6ebd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-1c61f0204834436a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### instanceof 关键字
>Instanceof运算符的第一个变量是一个对象，暂时称为A；第二个变量一般是一个函数，暂时称为B。
Instanceof的判断队则是：沿着A的__proto__这条线来找，同时沿着B的prototype这条线来找，如果两条线能找到同一个引用，即同一个对象，那么就返回true。如果找到终点还未重合，则返回false。

![image](http://upload-images.jianshu.io/upload_images/9249356-e37013930162ac1a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过上面的图片，可以解释以下情况
```
  console.log(Object instanceof Function)  // true
   console.log(Function instanceof Function) // true
   console.log(Function instanceof Object )   // true
```

