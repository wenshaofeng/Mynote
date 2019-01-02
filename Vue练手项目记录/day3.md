##图片分享分类导航（还没做）

##顶部返回导航的实现




##商品详情
- 卡片视图
使用 mui 的mui-card
- 轮播图
swiper 
- 商品购买
自建一个numbox 组件
初始化
![](https://upload-images.jianshu.io/upload_images/9249356-dba0fc9dfd8d5774.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 商品参数 
**问题：路由跳转后，滚动条记录**
解决 :

- 购物车
     -  购物车小球动画
    getBoundingClientRec()方法获取位置
    ####[JavaScript中getBoundingClientRect()方法详解](https://www.cnblogs.com/leejersey/p/4127714.html)
    - 当商品数量改变时实时接收购买数量 (子传父)
      细节：传值转化为数字
![](https://upload-images.jianshu.io/upload_images/9249356-0461e254c995d64a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    - 根据父组件中的商品存储量改变数字选择框最大值（父传子）
mui 自带API
![](https://upload-images.jianshu.io/upload_images/9249356-8e8a63dc28a9cbcc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    - ###vuex的使用
      - 点击后商品加入购物车功能
      - 购物车徽标数量的相加
      - 购物车的本地化存储
       localStorage
      - 购物车页布局 元素渲染
      - 初始化购物车页面的各个商品数量值（从vuex里获取）
      - 在购物车中改变数量时 同步数据到store中
      - 购物车中删除商品
        1. 页面中删除
        2. store中删除
      - 同步store中的选择状态到页面
      - 商品勾选件数和勾选的总价计算
      - 打包部署至Apache
      -  使用ngrok把本机的网站端口映射到外网
