踩坑：
![image.png](https://upload-images.jianshu.io/upload_images/9249356-085651a56aabca7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-c254c4cea06f09af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
原因：
this.scroll创建的时刻不对
![image.png](https://upload-images.jianshu.io/upload_images/9249356-8265e95b92261b9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-1d98d6e959992dbe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-3e80721998ec8b59.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加两个功能：
1.点击字母表，左侧城市选择切换
2.滑动字母表，左侧城市选择切换

都是字母表组件外派事件，父组件接收后再传给城市列表组件
**点击字母表和滑动字母表外派的事件是相同的，关键是确定传递的参数字母**

