###1.1. PHP 标记
- <?php 可以让代码进入“PHP 模式”
- ?> 可以让代码退出“PHP 模式”
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF‐8">
<title>这是一个包含 PHP 脚本的网页</title>
</head>
<body>
<h1>这是一个包含 PHP 脚本的网页</h1>
<p>这里原封不动的输出</p>
<?php
// 这里是 PHP 代码，必须满足 PHP 语法
$foo = 'bar';
echo $foo;
?>
<p>这里也不变</p>
<p><?php echo '<b>这还是 PHP 输出的</b>'; ?></p>
</body>
</html>
```
类似于在 HTML 中使用 JavaScript，但是不同的是 JavaScript 运行在客户端，而 PHP 运行在服务端。
**只有处于 PHP 标记内部的代码才是 PHP 代码，PHP 标记以外都原封不动。**

1.1.1. 省略结束标记
如果 PHP 代码段处于整个文件的末尾，建议（必须）删除结束标记，这样不会有额外的空行产生。

###1.2. 输出内容方式
echo （不能输出数组）
>echo 'hello php';
echo 'hello', 'world'; // 'helloworld' 

print：
>// print 与 echo 唯一区别就是只能有一个参数
print 'hello php';
// print 'hello', 'world';
// => Parse error: syntax error ...

var_dump：
><?php
// var_dump 是一个函数，必须跟上 () 调用
// 可以将数据以及数据的类型打印为特定格式
var_dump('hello php');
// => 'string(9) "hello php"'
###1.3. 与 HTML 混编

![](https://upload-images.jianshu.io/upload_images/9249356-5b4af1f480d3dade.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###2.1变量
![](https://upload-images.jianshu.io/upload_images/9249356-b20c50159fe55257.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###数组
![](https://upload-images.jianshu.io/upload_images/9249356-b295228b8dcd2b7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###字符串 
拼接字符串 用 点"."操作符
![](https://upload-images.jianshu.io/upload_images/9249356-058f067e99e937cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-e162c6240219dd49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###3.1. 变量作用域
关于变量作用域这一点，PHP 与绝大多数语言也都不同：默认函数内不能访问函数所在作用域的成员。
在 JavaScript 中，我们可以在函数作用域中使用父级作用域中的成员：
```
var top = 'top variable'
function foo () {
var sub = 'sub variable'
console.log(top)
// => `top variable`
function bar () {
console.log(top)
// => `top variable`
console.log(sub)
// => `sub variable`
}
bar()
}
foo()
```
在PHP中
```
<?php
$top = 'top variable';
function foo () {
$sub = 'sub variable';
echo $top;
// => 无法拿到
function bar () {
echo $top;
// => 无法拿到
echo $sub;
// => 无法拿到
}
bar();
}
foo();
```
如果需要访问全局变量，可以通过**global**关键字声明：
```
<?php
$top = 'top variable';
function foo () {
// 声明在当前作用域中获取全局作用域中的 `$top`
global $top;
$sub = 'sub variable';
echo $top;
// => `top variable`
function bar () {
// 声明在当前作用域中获取全局作用域中的 `$top` 和 `$bar`
global $top, $bar;
echo $top;
// => `top variable`
echo $sub;
// => 任然无法拿到，因为 `$sub` 不再全局范围，而是在 `foo` 函数中定义
}
bar();
}
foo();
```
###常量
![image.png](https://upload-images.jianshu.io/upload_images/9249356-ecfaa834219a18bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###载入文件
![](https://upload-images.jianshu.io/upload_images/9249356-65c9fd4b707b9f42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
使用层面：
- include 一般用于载入公共文件，这个文件的存在与否不能影响程序后面的运行
- require 用于载入不可缺失的文件
- 至于是否采用一次载入（once）这种方式取决于被载入的文件

