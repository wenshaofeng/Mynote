>使用nodemon工具自动重启应用

- 安装及使用
全局安装 nodemon ，这样新创建的 Node.js 应用都能使用 Nodemon运行
`npm install -g nodemon`
使用时，只需把node 改为nodemon即可,如:
`node main.js` → `nodemon main.js`
　　通过 Nodemon 启动应用之后，不管是修改了代码，还是安装了新的 npm 包，Nodemon 都会重新启动应用

#express
####静态资源服务
- 例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：
`app.use(express.static('public'))`
现在，你就可以访问 public 目录中的所有文件了：
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
Express 在静态目录查找文件，因此，存放静态文件的目录名不会出现在 URL 中。
 
- 现在，你就可以通过带有 /static 前缀地址来访问 public 目录中的文件了。
`app.use('/static', express.static('public'))`
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html

####在express中配置使用art-template
- 安装
`npm install --save art-template`
`npm install --save express-art-template`
- 配置

```
var express = require('express');
var app = express();
app.engine('art', require('express-art-template'));
```
>第一个参数，表示，当渲染以 .art 结尾的文件的时候，使用 art-template 模板引擎
express-art-template 是专门用来在 Express 中把 art-template 整合到 Express 中
虽然外面这里不需要记载 art-template 但是也必须安装
原因就在于 express-art-template 依赖了 art-template
- 使用（渲染页面）
```
app.get('/', function (req, res) {
    res.render('index.html', {
       comments : comments
    })
})
```
>Express 为 Response 相应对象提供了一个方法：render
render 方法默认是不可以使用，但是如果配置了模板引擎就可以使用了
`res.render('html模板名', {模板数据})`
第一个参数不能写路径，默认会去项目中的 views 目录查找该模板文件
也就是说 Express 有一个约定：开发人员把所有的视图文件都放到 **views** 目录中

- 修改默认默认的views视图渲染存储目录
```
app.set('views','目录路径')
```
##在Express中获取表单请求参数
- GET
Express内置了一个API，可以直接通过req.query来获取
- POST
在Express中没有内置获取表单POST请求体的API，这里我们需要使用一个第三方包`body-parser`
1. 安装 ` npm install  body-parser -S  `
2. 配置 
```
引包
var bodyParser = require('body-parser')

 配置 body-parser 中间件（插件，专门用来解析表单 POST 请求体）
  只要加入这个配置，则在 req 请求对象上会多出来一个属性 ： body
  也就是说我们可以直接通过req.body 来获取表单 POST 请求体数据了
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())
```
3. 使用
```
app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
//可以通过 req.body来获取表单 POST 请求体数据
  res.end(JSON.stringify(req.body, null, 2))
})
```
![](https://upload-images.jianshu.io/upload_images/9249356-50fb14a28553f2c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



###处理404页面
```
// 挂载路由，代码略...
 
app.use((req, res, next) => {
  res.render('404.html')
})
 
// 其它代码...
```
或者使用通配符
```
app.get('*', function(req, res){
    res.sendfile('./views/404.html');
  })
```
**注意**：上面代码一定要放在所有路由中间件之后，原理就是当前面没有任何一个路由可以处理的时候，程序就会走到最后这个中间件，然后就可以当作 404 来处理了。                                                                                                                                                  

