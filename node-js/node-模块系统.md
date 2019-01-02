### [nodejs模块中exports和module.exports的区别](https://www.cnblogs.com/ooooevan/p/5897586.html)
### [module.exports与exports，export与export default之间的关系和区别](https://www.cnblogs.com/fayin/p/6831071.html)


###加载`require`
语法：
`var 自定义变量名称 = require('模块') `
>作用
- 执行被加载模块中的代码 
-  得到被加载模块中的`exports`导出接口对象 

###导出`exports`
- Node中是模块作用域，默认文件中所有的成员只在当前文件模块有效
- 对于希望可以被其它模块访问的成员，我们就需要把这些公开的成员都挂载到`exports`接口对象中就可以了

**1. 导出多个成员(必须在对象中)**
```
//foo.js
var foo = 'bar'
function add(x, y) {
  return x + y
}
exports.foo = foo 
exports.a = "科比"
exports.b= "詹姆斯"
exports.c = add 

//main.js 
var fooExports = require('./foo')
console.log(fooExports)

//结果
E:\14.nodejs(共140多集)\nodejs资料（7天）\03\code\01-node中的模块系统> node main
{ foo: 'bar', a: '科比', b: '詹姆斯', c: [Function: add] }

```


**2. 导出单个成员**

错误写法1
```
//foo.js
var foo = 'bar'

function add(x, y) {
  return x + y
}
exports = foo 
exports.a = "科比"
exports.b= "詹姆斯"
exports.c = add 

//main.js 
var fooExports = require('./foo')
console.log(fooExports)

结果为空对象 {}

```
错误写法2 
```
//foo.js
var foo = 'bar'

function add(x, y) {
  return x + y
}

exports.a = "科比"
exports.b= "詹姆斯"
exports.c = add 
exports = foo 

//main.js 
var fooExports = require('./foo')
console.log(fooExports)

结果为{ a: '科比', b: '詹姆斯', c: [Function: add] }

```
 >如果一个模块需要直接导出某个成员，而非挂载的方式
 那这个时候必须使用下面这种方式

```
//foo.js
var foo = 'bar'

function add(x, y) {
  return x + y
}
module.exports = foo  //位置一
exports.a = "科比"
exports.b= "詹姆斯"
exports.c = add 
//module.exports = foo  位置二

/* module.exports = {  位置三
  add: function () {
    return x + y
  },
  str: 'hello'
} */

//main.js
var fooExports = require('./foo')
console.log(fooExports)

```
结果：
- 只有一个module.exports时，不管是在位置一还是位置二，都为 bar
- 当有两个module.exports 时，比如一个在位置一，另一个在位置三，会导出位置三的对象(**module.exports会被后者覆盖**)

###上面的结果出现的原因:exports 和module.exports的区别

在 Node 中，每个模块内部都有一个自己的 module 对象,该 module 对象中，有一个成员叫：exports 也是一个对象
类似这样:
```
var module = {
  exports: {
    foo: 'bar',
    add: function
  }
}
```
**每次导出的对象是module.exports**，也就是说如果你需要对外导出成员，只需要把导出的成员挂载到 module.exports 中
node中有一句代码，来简化输入
`var exports = module.exports`
exports 相当于是 一个引用，指向module.exports对象
所以有
```
console.log(module.exports === exports)   ///true 
```
而当给 exports 赋值会断开和 module.exports 之间的引用
同理，给 module.exports 重新赋值也会断开

但是这里又重新建立两者的引用关系
`exports = module.exports`

最后，一定要记得return 的module.exports，
如果给exports 赋值，断开了两个引用之间的联系，就不管用了

```
module.exports.foo = 'bar'
 exports.a = 'abc'

 exports = {}
 exports.b = '123'  //断开连接后，就没联系了，需重新联系起来


 exports = module.exports
 
 exports.foo = 'haha'
 module.exports.a = 'cba' 

结果  { foo: 'haha', a: 'cba' }
```

###requirie加载规则
  + 优先从缓存加载
![](https://upload-images.jianshu.io/upload_images/9249356-9bec8155c682c80c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 结果是
![](https://upload-images.jianshu.io/upload_images/9249356-572a8537f08f75e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
优先从缓存加载
 由于 在 a 中已经加载过 b 了
 所以这里不会重复加载
可以拿到其中的接口对象，但是不会重复执行里面的代码
这样做的目的是为了避免重复加载，提高模块加载效率
  + 核心模块
>核心模块的本质也是文件
核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了
如：
`require('fs')`
`require('http')`
  + 路径形式的模块

  + 第三方模块
    顺序：

 一：先找到当前文件所处目录中的 node_modules 目录
   node_modules/art-template
   node_modules/art-template/package.json 文件
   node_modules/art-template/package.json 文件中的 main 属性
   main 属性中就记录了 art-template 的入口模块
   然后加载使用这个第三方包
   实际上最终加载的还是文件

  二：如果 package.json 文件不存在或者 main 指定的入口模块是也没有
   则 node 会自动找该目录下的 index.js
   也就是说 index.js 会作为一个默认备选项

  三：如果以上所有任何一个条件都不成立，则会进入上一级目录中的 node_modules 目录查找
   如果上一级还没有，则继续往上上一级查找
   。。。
   如果直到当前磁盘根目录还找不到，最后报错：
     can not find module xxx

##文件操作路径和模块标识路径
![](https://upload-images.jianshu.io/upload_images/9249356-e7bf6811c760c23c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
