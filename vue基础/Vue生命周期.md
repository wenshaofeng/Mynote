![实现生命周期钩子](https://upload-images.jianshu.io/upload_images/9249356-34954043b0e9fd97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##注意
![image.png](https://upload-images.jianshu.io/upload_images/9249356-f799f35e9d19ff68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##生命周期图示
![图示](http://upload-images.jianshu.io/upload_images/9249356-4ed38466209b78ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>Vue 实例的生命周期函数（官方11个）：
beforeCreate：在实例部分（事件/生命周期）初始化完成之后调用。
created：在完成外部的注入/双向的绑定等的初始化之后调用。
beforeMount：在页面渲染之前执行。
mounted：dom 元素在挂载到页面之后执行。

>首次加载页面时，不会走这两个钩子，只有当数据发生改变时才会执行：
beforeUpdate：数据改变，还没重新渲染之前执行。
updated：渲染数据完成之后执行。

>执行销毁需要调用：vm.$destroy()
beforeDestroy：实例销毁之前执行。
destroyed：实例销毁之后执行。

![](https://upload-images.jianshu.io/upload_images/9249356-42e62f0c65d0e8c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
