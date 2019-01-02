##起步、初始化

##路由设计
| 请求方法 |     请求路径     | get 参数 |           post 参数            |       备注       |
|----------|------------------|----------|--------------------------------|------------------|
| GET      | /studens         |          |                                | 渲染首页         |
| GET      | /students/new    |          |                                | 渲染添加学生页面 |
| POST     | /studens/new     |          | name、age、gender、hobbies     | 处理添加学生请求 |
| GET      | /students/edit   | id       |                                | 渲染编辑页面     |
| POST     | /studens/edit    |          | id、name、age、gender、hobbies | 处理编辑请求     |
| GET      | /students/delete | id       |                                | 处理删除请求     |
|          |                  |          |                                |                  |


##提取路由
①导出一个函数调用 ![](https://upload-images.jianshu.io/upload_images/9249356-4c97b06f68124658.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
②使用Express提供的express.Router()路由容器
```
//router.js中
var express = require('express')
var router = express.Router()
... //路由配置

导出路由容器
module.exports = router  

//app.js中
var router = require('./router.js')
var express = require('express')
var app = express()
...
挂载路由
app.use(router)
```
![](https://upload-images.jianshu.io/upload_images/9249356-46a66065f8b31f97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##封装处理学生数据的操作（增删改查操作）
![](https://upload-images.jianshu.io/upload_images/9249356-a214828c167c06a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

总结：学会模块化，功能尽量单一并抽取成一个文件!

![关于回调函数](https://upload-images.jianshu.io/upload_images/9249356-93417accd52bfae3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
