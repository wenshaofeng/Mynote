### 类型检查
* `defaultProps` 默认属性值
* `propTypes`    限制接收的属性类别(**仅在开发模式中检测**)

**基本写法**
```javascript
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

- 使用 `isRequired' 链接上述任何一个，以确保在没有提供 prop 的情况下显示警告。

- defaultProps 设置默认属性

```javascript
//类型检测
TodoItem.propTypes = {
    content: PropTypes.string,
    deleteItem: PropTypes.func,
    index: PropTypes.number,
    // 你可以使用 `isRequired' 链接上述任何一个，以确保在没有提供 prop 的情况下显示警告。
    test: PropTypes.string.isRequired
}

//设置默认值
TodoItem.defaultProps = {
    test: '科比布莱恩特'
}
```


![](https://upload-images.jianshu.io/upload_images/9249356-60a0586e532bffaf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 某种类型之一
```javascript
 // 一个对象可以是多种类型其中之一
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),
```
### props，state与render函数的关系
- 当组件的state或者props发生改变时，render函数就会重新执行（自身）
- 当父组件的render函数执行时，它的子组件的render都将被重新执行
