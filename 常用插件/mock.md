

- mock数据

###mock数据
>此次开发过程需要去本地数据地址进行请求，而原版配置在 dev-server.js 中，新版 vue-webpack-template 已经删除 dev-server.js，改用webpack.dev.conf.js代替，所以配置本地访问在 webpack.dev.conf.js 里配置即可。这里使用 express 框架去写一个 nodeserver，也可以用 express-router 来编写这些接口请求

1. express mock
```
// ** mock data start
// 加载数据
const appData = require('../src/mock/data.json')
const seller = appData.seller
const goods = appData.goods
const ratings = appData
....

 devServer: {
    before(app) {
      app.get('/api/seller',(req,res)=>{
          res.json({
            //这里是你的json内容
            errno:0,
            data :seller
          })
      }),

      app.get('/api/goods',(req,res)=>{
        res.json({
          //这里是你的json内容
          errno:0,
          data :goods
    
        })
      }), 

      app.get('/api/ratings',(req,res)=>{
        res.json({
          //这里是你的json内容
          errno:0,
          data :ratings   
        })
      })
    }
```
2. mock.js
>1. npm install mockjs -D
>2. import './mock/mockServer' // 引入加载模块 
>3.  新建一个mockServer.js 
 ```
/**
 * 使用mockjs来mock数据, 提供mock数据API接口
 */
import Mock from 'mockjs'
import data from './data.json'

//注册接口
Mock.mock('/api2/goods', {
  code: 0,
  data: data.goods
})
Mock.mock('/api2/ratings', {
  code: 0,
  data: data.ratings
})
Mock.mock('/api2/seller', {
  code: 0,
  data: data.seller
})

// 不用export
```
