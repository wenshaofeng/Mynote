## 新闻资讯 页面 制作
1. 绘制界面， 使用 MUI 中的 media-list.html
2. 使用 axios 获取数据
3. 渲染真实数据
## 实现 新闻资讯列表 点击跳转到新闻详情
1. 把列表中的每一项改造为 router-link,同时，在跳转的时候应该提供唯一的Id标识符
2. 创建新闻详情的组件页面  NewsInfo.vue
3. 在 路由模块中，将 新闻详情的 路由地址 和 组件页面对应起来
4. 使用了better-scroll 实现新闻详情页面滚动
 - (踩的坑)样式穿透 
  **由于scoped的影响**
![](https://upload-images.jianshu.io/upload_images/9249356-10c526aa40ecd293.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-15b335e029261490.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 单独封装一个 comment.vue 评论子组件
用到了Mint-ui的Toast、Button组件

# [Vue中的scoped及穿透方法](https://www.cnblogs.com/karthuslorin/p/9038854.html)

# [使用vue-cli时引入mui.js时取消严格模式](https://www.cnblogs.com/Richard-Tang/p/9963563.html)
# [mui在vue_cli上使用](https://www.cnblogs.com/hss-blog/p/9482392.html)

**vue-preview插件使用的坑**
![image.png](https://upload-images.jianshu.io/upload_images/9249356-d050ee8a6affbd06.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

scoped 属性的影响，导致该组件的样式无法设置
![](https://upload-images.jianshu.io/upload_images/9249356-03d4eb8842c1073f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
