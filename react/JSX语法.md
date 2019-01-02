从本质上讲，JSX 只是为 React.createElement(component, props, ...children) 函数提供的语法糖。JSX代码:

```
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```
编译为：
```
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)
```
* 组件写样式，不要直接用class，会和es6关键字同名，得用 `className`
* 组件属性：`dangerousSetInnerHTML` 危险的转换html
![](https://upload-images.jianshu.io/upload_images/9249356-8453b3041a837ff0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
