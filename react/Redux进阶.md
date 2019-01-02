### [redux和react-redux小记](https://www.cnblogs.com/bax-life/p/8440326.html)

### UI组件和容器组件
>一个react组件最基本的基本上就是完成两大功能
　　1、读取store的状态，用于初始化组件的两大状态，监听store的状态变化
　　2、根据当前的props和state，渲染出用户的界面

![](https://upload-images.jianshu.io/upload_images/9249356-59f35d10cecf4952.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以将render部分拆分成一个UI组件出去，只负责渲染而不作任何业务逻辑处理
```
render() {
        return (
           <TodoListUI 
           inputVal={this.state.inputVal}
           handleInputChange = {this.handleInputChange}
           hangdleBtnClick = {this.hangdleBtnClick}
           list = {this.state.list}
           handleDeleteItem = {this.handleDeleteItem}
           />
        );
    }
```
一种箭头函数写法
![](https://upload-images.jianshu.io/upload_images/9249356-9e119f991ae6fcb0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 无状态组件

当一个普通组件中只有render函数的时候，可以把它改写成无状态组件，这样能提高性能
> 无状态组件只是一个函数，而普通组件是一个类 class ，这个class 还会带有一些生命周期函数，所以当普通组件执行起来，还会执行别的生命周期的函数，远比无状态组件要执行的东西要多得多

![](https://upload-images.jianshu.io/upload_images/9249356-808c400af1174875.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Redux中间件

#### Redux-thunk

`安装和使用redux-thunk`
- 安装、在index.js中引入和配置
- 将异步操作的函数抽离到action里（使用中间件后action可以是一个函数）
- store.dispatch(action)这一行代码在action是函数的时候，会执行该函数

```javascript
//index.js

import { createStore, applyMiddleware, compose } from 'redux' //引入方法
import reducer from './reducer'
import thunk from 'redux-thunk';  //引入中间件

//使用redux-thunk 的同时 使用devtools
const composeEnhancers =
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?
        window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({
        }) : compose;

const enhancer = composeEnhancers(
    applyMiddleware(thunk),
);

const store = createStore(reducer, enhancer);
```
`使用了redux-thunk`以后，action可以是一个函数
```javascript
//使用了redux-thunk以后，可以返回函数
export const getTodoList = () => {
    return (dispatch) => {
        axios.get('/api/todolist.json')
            .then((res) => {
                const data = res.data
                const action = initListAction(data)
                dispatch(action)
            }).catch(() => {
                console.log('err');
            })
    }
}

******************************
 componentDidMount() {
        //使用了 redux-thunk 以后 action 可以是一个函数
       const action = getTodoList()
       store.dispatch(action)
    }
```
>当store.dispatch(action)执行时，如果action是一个函数，那么会执行这个函数,并且dispatch会自动地派发给函数内部

**中间件指的是Action 和 store 的中间**
![](https://upload-images.jianshu.io/upload_images/9249356-99e200a0a1ba8375.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>中间件相当于`Dispatch`的封装，升级了`Dispatch`

#### Redux-saga

#### React-redux
