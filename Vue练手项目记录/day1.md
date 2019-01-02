## 制作首页APP组件

1. 完成header区域，使用mint-UI组件
2. 完成底部tabbar区域，使用的是MUI。
 + MUI的图标在example文件夹中找，火狐对本地HTML支持不好，使用edge或Chrome打开
 + 需要拷贝扩展图标的样式库与字体库。
  ![](https://upload-images.jianshu.io/upload_images/9249356-1a973f693e63fcf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 + 为购物车图标添加类名。
mui-icon mui-icon-extra mui-icon-extra-cart
3. 要在中间区域放置一个router-view来展示路由组件

## 改造tabbar为router-link

##设置路由高亮
```
  linkActiveClass: 'mui-active'
```
##点击路由展示组件

## 制作首页轮播图
Swiper组件使用，踩坑
- 无法显示底部swiper-pagination
- 无法无限轮播
  1. 配置错误，swiper4.0配置更新
  2. DOM动态渲染导致计算问题



## 加载轮播图数据

[轮播图API地址](https://github.com/xCss/bing)（原地址已经失效，使用公开的bing每日图片的api）

**使用axios加proxytable代理（踩坑)**
![](https://upload-images.jianshu.io/upload_images/9249356-cec54758701b059d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-d640ab99fcc14636.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


遇到奇怪的bug
修改了proxyTable 的配置后，跨域还是不成功，最后删了node_modules重新下载了一次，解决了
## 改造九宫格区域的样式

##切换组件的动画
![](https://upload-images.jianshu.io/upload_images/9249356-5985c3c9cf5d73aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 时间的格式的处理
  
moment.js
1.npm install moment.js

`删掉依赖后重新 npm i 后报错`
（解决）
![image.png](https://upload-images.jianshu.io/upload_images/9249356-0c9a0c1f82389900.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
