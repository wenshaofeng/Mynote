# [使用vue-axios和vue-resource解决vue中调用网易云接口跨域的问题](https://segmentfault.com/a/1190000011072725)
# [vue.js学习之 跨域请求代理与axios传参](https://www.cnblogs.com/momozjm/p/7993236.html)

##[vue中proxyTable反向代理进行跨域](https://blog.csdn.net/gao_xu_520/article/details/80407049)

###[奇怪的bug:解决 vue-cli中 proxyTable 配置无效](https://www.jianshu.com/p/3e4a04b4f5d8)
参考文档https://vuejs-templates.github.io/webpack/proxy.html

本地开发服务下是 http://localhost:8080 这样的访问页面，但是我们的接口地址是 http://xxxx.com/save/index 这样的接口地址，我们这样直接使用会存在跨域的请求，导致接口请求不成功，因此我们需要在打包的时候配置一下，我们进入 config/index.js 代码下如下配置即可：

```
dev: {

    // 静态资源文件夹
    assetsSubDirectory: 'static',

    // 发布路径
    assetsPublicPath: '/',
    // 代理配置表，在这里可以配置特定的请求代理到对应的API接口
    // 例如将'localhost:8080/api/xxx'代理到'www.example.com/api/xxx'
    // 使用方法：https://vuejs-templates.github.io/webpack/proxy.html
    proxyTable: {
      '/api': {
        target: 'http://xxxxxx.com', // 接口的域名
        // secure: false,  // 如果是https接口，需要配置这个参数
        changeOrigin: true, // 如果接口跨域，需要进行这个参数配置
        pathRewrite: {
          '^/api': ''
        }
      }
    },
```

注意： '/api' 为匹配项，target 为被请求的地址，因为在 ajax 的 url 中加了前缀 '/api'，而原本的接口是没有这个前缀的，所以需要通过 pathRewrite 来重写地址，将前缀 '/api' 转为 '/'。如果本身的接口地址就有 '/api' 这种通用前缀，就可以把 pathRewrite 删掉。

##配置多个路径
# [proxyTable如何配置匹配所有路径？](https://segmentfault.com/q/1010000008769620)


config中
![](https://upload-images.jianshu.io/upload_images/9249356-f4e100f07371c7ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
发送请求时
![](https://upload-images.jianshu.io/upload_images/9249356-fd0291942b2a1aa9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**注意！** proxyTable 这个插件只限于开发模式下，后面一定要将前端代码和服务器代码部署到一起，否则需要要通过Nginx进行跨域的转发配置

