##步骤 
   * 安装mongoose链接数据库mongodb
   * 导入数据到MongoDB数据库中
   * 创建model,mongoose创建的model就是一个实体，可以跟mongodb进行关联。
   * 创建路由。
   * 基于mongoose,实现商品列表的查询功能。


###MongoDB导入resource中的数据dumall-goods
>导入数据可以使用命令：
　　　　`mongoimport -h dbhost -d dbname -c collectionname input`
　　　　参数说明:
　　　　-h 数据库地址
　　　　-d 指明使用的库
　　　　-c 指明要导入的集合（mongodb本身支持隐式创建，故事先无需创建集合）
　　　　input 文件的地址
例子:
```
mongoimport -h localhost:27017 -d dumall -c goods F:/Project/Project_shopmall/shopmall/resource/dumall-goods
```
![](https://upload-images.jianshu.io/upload_images/9249356-c39c3f710015507d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

创建model
![](https://upload-images.jianshu.io/upload_images/9249356-75d30a05afaf7f52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

创建路由
![](https://upload-images.jianshu.io/upload_images/9249356-4020f1967e852314.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-5fd0ecce8bcb86bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

实现接口以后，就可以不用再mock数据了，要在config文件夹中的index.js做开发时的代理转发（接口跨域）
![](https://upload-images.jianshu.io/upload_images/9249356-ba9869e9fcdcd762.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
同时注释掉webpack.dev.conf.js 中的相应mock代码

实现页面商品列表数据是从数据库接口得到
![](https://upload-images.jianshu.io/upload_images/9249356-00512563964faece.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





