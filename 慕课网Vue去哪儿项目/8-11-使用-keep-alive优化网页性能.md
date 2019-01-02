##keep-alive标签
![](https://upload-images.jianshu.io/upload_images/9249356-307dc0f2ad1f3f50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>keep-alive会把包裹的页面缓存起来，可以避免多次请求重复数据。activated钩子函数会在keep-alive组件激活时调用。 当引入keep-alive的时候： 
>1. 页面第一次进入，钩子的触发顺序created-> mounted-> activated 
> 2. 再次进入（前进或者后退）时，只触发activate
 >3. 每一次退出时触发deactivated

######取消缓存某个组件
![](https://upload-images.jianshu.io/upload_images/9249356-ae8b7c59a7448ff3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-67f3cd42b9f8fa44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





###城市改变时重新发送ajax请求
![](https://upload-images.jianshu.io/upload_images/9249356-3e54ddc1b8a4e566.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


>1、全局事件解绑 window全局事件，无论哪个页面都会监听这个事件，会影响到其它页面，所以要解绑。
 2、在有keep-alive时会出现两个生命周期函数: activated和deactivated activated 在页面被显示时执行 deactivated 在页面即将被隐藏或页面被替换的时候执行
 3、所以为了使全局事件不影响其它页面，我们在activated中绑定(addEventListener)，然后在deactivated中解绑(removeEventListener)
