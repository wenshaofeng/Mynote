###[大白话讲解Promise（一）](https://www.cnblogs.com/lvdabao/p/es6-promise-1.html)
###[在线流程图与测试](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
## 封装一个读取文件的函数(回调的演示)
- 没有回调时 
```
const fs = require('fs')
const path = require('path')

 封装  目的：给定文件路径，返回读取的内容
 结果：返回undefined 因为 读取文件是异步操作
 被放入异步操作队列，函数执行到最后
function getFile(fpath){

    fs.readFile(fpath,'utf-8',(err,dataStr)=> {
        if(err) throw err 
        return dataStr
    })
    //函数执行到此，没有return默认返回undefined
}

var result = getFile(path.join(__dirname,'./files/3.txt'))
console.log(result); //undefined
```
- 添加回调
```
使用回调函数,拿到返回的值
我们可以规定一下， callback 中，有两个参数，第一个参数，是 失败的结果；
第二个参数是成功的结果；
同时，我们规定了： 如果成功后，返回的结果，应该位于 callback 参数的第二个位置，此时，
 第一个位置 由于没有出错，所以，放一个 null；  
如果失败了，则 第一个位置放 Error对象，第二个位置防止一个 undefined
function getFile(fpath,callback){

    fs.readFile(fpath,'utf-8',(err,dataStr)=> {
        if(err) return callback(err)        
        callback(null,dataStr)             
    })    
}
    // (callback)=>{} = function(callback) {}
var result = getFile(path.join(__dirname,'./files/3.txt'),(err,data)=>{
     if(err) return console.log(err)
     console.log(data);       
})
```
- 返回两个回调函数
```
function getFile(fpath,handleerr,handlesuc) {
    fs.readFile(fpath,'utf-8',(err,dataStr)=>{
        if(err) return handleerr(err)

         handlesuc(dataStr)
    })
}

var result = getFile(path.join(__dirname,'./files/3.txt'),function handleerr (err) {
    
    console.log(err+'失败了亲')
      
},function handlesuc(data){
    console.log(data+'哈哈哈成功了')

})
```
需求：按顺序读取三个文件：此时将会出现嵌套的回调即**回调地狱**
```
getFileByPath(path.join(__dirname, './files/1.txt'), function (data) {
    console.log(data)
  
    getFileByPath(path.join(__dirname, './files/2.txt'), function (data) {
      console.log(data)
  
      getFileByPath(path.join(__dirname, './files/3.txt'), function (data) {
        console.log(data)
      })
    })
  })
```

因此，我们将用ES6中的promise对象解决这一问题
promise的本质：单纯的解决回调地狱问题，并不能解决代码量。

## Promise概念介绍
1. Promise 是一个构造函数，可以new 得到一个实例，他有
	+ resolve：成功之后的回调函数
	+ reject ：失败之后的回调函数

2. 在Promise的构造函数的prototype属性，有.then()方法，只要是 Promise 构造函数创建的实例，都可以访问到 .then() 方法
3. Promise表示一个异步操作，每当我们new一个Promise对象，就表示了一个具体的异步操作
4. 异步操作有两种状态：
	+ 异步执行成功，内部调用resolve
	+ 异步执行失败，内部调用reject
5. 由于Promise是一个异步的实例，因此无法return（会得到 undefined），只能通过回调函数的形式返回给调用者
6. 我们可以在new出来的Promise实例对象上，调用.then方法，**【预先】**为这个Promise指定成功和失败的回调函数

## Promise的写法

- 形式上的异步操作 `var promise = new Promise()`

> 什么是形式上的异步操作：就是说，我们只知道它是一个异步操作，但是做什么具体的异步事情，目前还不清楚
- 具体的异步操作
```
 var promise = new Promise(function(){
  // 这个 function 内部写的就是具体的异步操作！！！
}) 
```
>每当 new 一个 Promise 实例的时候，就会**立即执行**这个 异步操作中的代码
 也就是说，new 的时候，除了能够得到 一个 promise 实例之外，还会立即调用我们为Promise 
 构造函数传递的那个 function，执行这个 function 中的 异步操作代码；

```
var promise = new Promise(function (){
    fs.readFile('./files/1.txt','utf-8',(err,data)=>{
        if(err) throw err
        console.log(data); 
    })
})
```
####Promise 解决回调地狱
>在上一个 .then 中，返回一个新的 promise 实例，可以继续用下一个 .then 来处理
**注意： 通过 .then 指定 回调函数的时候，成功的 回调函数，必须传，但是，失败的回调，可以省略不传**

![](https://upload-images.jianshu.io/upload_images/9249356-7fc85130fa3f2246.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
const fs = require('fs')
function getFlie (fpath){
    return  new Promise(function (resolve,reject){
        fs.readFile(fpath,'utf-8',(err,data)=>{
            if(err) return reject(err)
            resolve(data)
        })       
   })
}

getFlie('./files/2.txt')
.then(function(data){
    console.log(data+'----');
      
    return getFlie('./files/1.txt')
}).then(function(data){
    console.log(data+'----');
    
    return getFlie('./files/3.txt')
}).then(function(data){
    console.log(data )
})
 
console.log("hahaha");
//输出 hahaha
       //  222----
       //  111----
       //  333
```
###捕获异常的两种方式
1.  如果前面的 Promise 执行失败，我们不想让后续的Promise 操作被终止，可以为 每个 promise 指定 失败的回调
2. 如果前面有任何的 Promise 执行失败，则可以使用**catch**立即终止所有 promise 的执行，并 马上进入 catch 去处理 Promise中 抛出的异常；

- 指定失败的回调
```
getFlie('./files/22.txt')
.then(function(data){
    console.log(data+'----');

    return getFlie('./files/1.txt')
},function(err){
    console.log((err+'读取出错了'));
    
    return getFlie('./files/1.txt')
}).then(function(data){
    console.log(data+'----');
    
    return getFlie('./files/3.txt')
}).then(function(data){
    console.log(data )
})
 
console.log("hahaha");
```
- catch
```
getFlie('./files/22.txt')
.then(function(data){
    console.log(data+'----');

    return getFlie('./files/1.txt')
},function(err){
    console.log((err+'读取出错了'));
    
    return getFlie('./files/11.txt')
}).then(function(data){
    console.log(data+'----');
    
    return getFlie('./files/3.txt')
}).then(function(data){
    console.log(data )
}).catch(function(err){

    console.log(err);
    

})
 
console.log("hahaha");
//输出
  hahaha
Error: ENOENT: no such file or directory, open 'E:\vuejs资料\day8\代码\code\files\22.txt'读取出错了
  { [Error: ENOENT: no such file or directory, open 'E:\vuejs资料\day8\代码\code\files\11.txt']
  errno: -4058,
  code: 'ENOENT',
  syscall: 'open',
  path: 'E:\\vuejs资料\\day8\\代码\\code\\files\\11.txt' }

 ```
+ resolve和reject只会执行一个，如果在promise构造时内部没有定义，则都不会执行

