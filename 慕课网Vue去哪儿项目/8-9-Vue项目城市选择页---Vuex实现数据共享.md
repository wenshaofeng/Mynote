![](https://upload-images.jianshu.io/upload_images/9249356-33cab6d86da1c4fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>state:存放共用数据
actions:异步方法
mutations



- 项目中引入router插件

```
import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/pages/home/Home'
import City from '@/pages/city/City'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Home',
      component: Home
    },
    {
      path:'/city',
      name :'City',
      component: City
    }

  ]
})
```
- 项目中引入Vuex插件
```
import Vuex from 'vuex'
import Vue from 'vue'
 Vue.use(Vuex)
  export default new Vuex.Store({
    state:{
      city : '深圳'
    }
  })

```
>$store 指点是Vuex.Store 

![](https://upload-images.jianshu.io/upload_images/9249356-53569532ec09c87f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-ae5dd111c9e3f072.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####动态改变数据
![](https://upload-images.jianshu.io/upload_images/9249356-a8c5932fbe7c5123.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
当异步操作要更改的数据比较简单不用进行太多处理时，可以直接跳过Actions到Mutations操作

####额外小点（路由跳转）
>编程式导航

![](https://upload-images.jianshu.io/upload_images/9249356-3b97ff9a54f2a127.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-99ba6171dfdf437d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


