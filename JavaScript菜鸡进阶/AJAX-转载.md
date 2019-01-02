# 伪ajax教程

​	能大致学会ajax是什么,怎么用,项目中常用ajax插件以及如何mock数据等技巧.这里只讲前端

### ajax是什么?

​	传统的网页就好像两个人在填一张表(网页),服务器端提供了一个空白的表格给客户端,客户端看见之后在上面填写内容,并将整张表发回服务器,服务器查看之后没有问题,再将整张表格返回给客户端.

​	有了ajax就不一样了,用户可以在填写表格时选择发送或接受哪些数据.因为ajax可以让网页的局部数据更新,例在百度搜索时弹出的搜索建议列表就是ajax加载出来的.

​	最新的一些前端框架vue等,能做到前后端分离也是基于ajax,

### 怎么用?

> 前置知识:

- 什么是数据接口?

  我们管有一堆数据的链接地址叫接口

  e.g. https://www.easy-mock.com/mock/5b319ab2a776703db5dff938/test/home

- 常见名词request和response

  request是请求(客户端发给服务器的)

  response是回答(服务器返回给客户端的)

  中间省略HTTP请求细节(自行百度)

- 请求接口的类型

  大致分为POST和GET两种类型的接口

- 请求接口方式

  传参请求和不传参请求

  get和post在请求时有区别,get会把参数放在url里post不会

  e.g.登录过程就是传参请求,将用户名和密码发给后台

- 查看接口请求技巧,浏览器f12开控制台有个network,name里是请求,可以点开看response就是这个接口返回给我们的内容


> 主题

​	原生的js提供了XMLHttpRequest这个对象,对象的方法都在这个链接里面.

https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest

​	工作的时候基本很少用到原生的方法,一般都是使用第三方的轮子,常用的ajax轮子有 jq的ajax方法,axios,具体怎么用都在他们相应的官方文档里了.

### 重点!!

> 模拟数据

这个网站

https://www.easy-mock.com/ 注册登录

https://www.easy-mock.com/docs 教程

跟着教程做就有自己的数据接口了,就可以测试用了

