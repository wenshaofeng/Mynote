####[MongoDB自学笔记12---4.4 更新文档](https://blog.csdn.net/mengxiangyue/article/details/18560357)

![](https://upload-images.jianshu.io/upload_images/9249356-8574f6333af8b23e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##windows平台下MonggoDB安装和环境搭建
- 下载安装包或者压缩包
- 添加db存储和日志存储文件夹
- 添加服务、配置环境变量、启动Mongo

# [MongoDB+MongoVUE安装及入门](http://blog.csdn.net/lupengfei1009/article/details/50832996)
#[windows平台mongoDB安装配置](https://www.cnblogs.com/ymwangel/p/5859453.html)

启动服务
`mongod -dbpath "F:\MongoDB\data\db"`
>若启动成功，会显示mongoDB默认的监听端口：27017，mysql的是3306
在浏览器中输入[http://localhost:27017/](http://localhost:27017/)。会出现：
　　It looks like you are trying to access MongoDB over HTTP on the native driver port.
表明服务已经启动。

连接`mongo`
退出` exit`

基本命令
- show abs
  - 查看所有数据库
- db
  - 查看当前操作的数据库
- use 数据库名称
  - 创建数据库

![](https://upload-images.jianshu.io/upload_images/9249356-c59e84fa24bd48a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-a1086b84e727ebe9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
![](https://upload-images.jianshu.io/upload_images/9249356-ebb9cb06b24c9d30.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##Mongoose与Node
- 增删改查
- 改写学生信息增删改查


  ###MongoDB创建用户
![](https://upload-images.jianshu.io/upload_images/9249356-6706278817fa8721.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# [MongoDB的导入导出](https://www.cnblogs.com/jiyukai/p/6980104.html)

###MongoDB导入文档
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
![](https://upload-images.jianshu.io/upload_images/9249356-25fc9fb809593cce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###无法给数据库中的数据添加自定义属性的坑
解决方案：在定义数据模板Schema的时候，定义自定义属性的字段
![](https://upload-images.jianshu.io/upload_images/9249356-d74c5269569a87e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**mongoose的update方法**
![](https://upload-images.jianshu.io/upload_images/9249356-e44f2637d01a46e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-9042153d33e3f257.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/9249356-35adfb605b3a456e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


