
# [vue 监听路由变化](https://www.cnblogs.com/crazycode2/p/8727410.html)
![](https://upload-images.jianshu.io/upload_images/9249356-4235b68986013972.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##[vue-router 由hash向history模式变迁](https://www.jianshu.com/p/250022c96035)


## 什么是路由
![](https://upload-images.jianshu.io/upload_images/9249356-e95cd438ebec193f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-58a44dfe9d913853.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1. **后端路由：**对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源；

2. **前端路由：**对于单页面应用程序来说，主要通过URL中的hash(#号)来实现不同页面之间的切换，同时，hash有一个特点：HTTP请求中不会包含hash相关的内容；所以，单页面程序中的页面跳转主要用hash实现；
![image.png](https://upload-images.jianshu.io/upload_images/9249356-85068c2ec75f7b61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 在单页面应用程序中，这种通过hash改变来切换页面的方式（不会刷新页面），称作前端路由（区别于后端路由）；
### [URL中的hash（井号）](https://www.cnblogs.com/joyho/articles/4430148.html)



![](https://upload-images.jianshu.io/upload_images/9249356-ce00e4620ad675eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![路由.png](https://upload-images.jianshu.io/upload_images/9249356-8a1e585ccf893812.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###router标签
![image.png](https://upload-images.jianshu.io/upload_images/9249356-10bff719067bf20d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###路由切换
![image.png](https://upload-images.jianshu.io/upload_images/9249356-36509e093eef57f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###路由传参
1. 通过query传参
2. 通过params传参  （需要配置path参数）

###路由嵌套
![](https://upload-images.jianshu.io/upload_images/9249356-2f16fc595e02bf77.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###多个路由组件（components）
![](https://upload-images.jianshu.io/upload_images/9249356-29abd2b5e2a10988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###webpack中使用路由
一: 下载包 `npm install vue-router`
二: 导入
```
import Vue from 'vue'
1. 导入 vue-router 包
import VueRouter from 'vue-router'
2. 手动安装 VueRouter 
Vue.use(VueRouter)
// 导入 app 组件
import app from './App.vue'
// 导入 Account 组件 (路由子组件)
import account from './main/Account.vue'
import goodslist from './main/GoodsList.vue'


```
三：创建路由对象
```
var router = new VueRouter({
  routes: [
    // account  goodslist
    { path: '/account', component: account },
    { path: '/goodslist', component: goodslist }
  ]
})
```
四：挂载
```
var vm = new Vue({
el : '#app',
render: c => c(app),
router
  }
)
```
**注意**
>render 会把 el 指定的容器中，所有的内容都清空覆盖，
所以不要把路由的 router-view 和 router-link 直接写到 el 所控制的元素中

##动态路由
![](https://upload-images.jianshu.io/upload_images/9249356-cac5ad527250b0eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
设置路由模式
mode
- history
- hash
![](https://upload-images.jianshu.io/upload_images/9249356-1ed854a28751751d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##编程式导航

注意区分 this.\$route 和 this.\$router 这两个对象，
 - 其中： this.\$route 是路由【参数对象】，所有路由中的参数， params, query 都属于它
 - this.\$router 是一个路由【导航对象】，用它 可以方便的 使用 JS 代码，实现路由的 前进、后退、 跳转到新的 URL 地址
