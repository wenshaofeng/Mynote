

### [vue和react区别](https://www.cnblogs.com/yf-html/p/9102931.html)
### [整理下react中常见的坑](https://www.cnblogs.com/jinzhou/p/9179340.html)

## 开发环境搭建
### [基于create-react-app的再配置](https://www.cnblogs.com/xiaohuochai/p/8491055.html)

报错
```
PS C:\Users\lijiawei\Desktop> npx create-react-app my-app
npm ERR! code ENOLOCAL
npm ERR! Could not install from "Files\nodejs\node_cache\_npx\68292" as it does not contain a package.json file.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Program Files\nodejs\node_cache\_logs\2018-12-17T07_15_39_571Z-debug.log
```
#### 解决方法
```
npm install -g create-react-app 
create-react-app myApp
```
## React中组件的语法
**函数式组件和类组件**
- 函数式
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
- 类组件
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
两种写法
![](https://upload-images.jianshu.io/upload_images/9249356-9f7dd88246af09c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### JSX语法
![](https://upload-images.jianshu.io/upload_images/9249356-2a0953123dab1bb4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
自定义的组件开头要大写

#### 代码优化
1、在构造函数中做好this指向的改变
下面就不用.bind(this)
可以改变代码的执行性能
![](https://upload-images.jianshu.io/upload_images/9249356-2efa0c1e22a62910.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、解决render函数中代码过长
![image](http://upload-images.jianshu.io/upload_images/9249356-da37b65f25267abe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### Fragment（片段）
![](https://upload-images.jianshu.io/upload_images/9249356-faf44b1235278647.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-c244e66e67caf919.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### react 的特点
![](https://upload-images.jianshu.io/upload_images/9249356-3055cf0996b1a63d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### React设计思想

* 声明式开发
  * 对应的就是命令式的开发，例如jQuery就是一个操作DOM的命令式开发。而React这是好比我们在设计一张大楼的图纸，我们只管图纸设计，怎么施工就交给React。
* 可以与其他框架并存
* 组件化
* 单项数据流
  * 例如父组件中有5个子组件共同引用了一个数据源，当5个子组件都有修改数据源的操作后，如果出现bug，要精确定位bug很困难，必须一个一个组件找
  * 如果真要改就统一在父组件中改
* 视图层框架
* 函数式编程
  * React代码基本上都是一个个函数的写法
  * 优势1：易于维护，当一个函数比较大时，可以拆分，每个函数各司其职
  * 优势2：面试测试的开发流程，如果项目代码都是些函数，我们就可以很方便的测试其输出是不是符合我们预期的值
