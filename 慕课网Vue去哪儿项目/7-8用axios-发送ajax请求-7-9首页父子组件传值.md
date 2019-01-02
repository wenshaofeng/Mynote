
#7-8
axios:可以发送跨平台的请求：XHR、HTTP.
安装axios : npm install axios --save 
导入 axios 
挂载到mouted函数
在mouted函数中发送请求
用json文件模拟后台数据（存放到static目录下，只有该目录下的文件能被外部访问;其余的路径的文件会被定位回首页）
###### proxyTable可以配置接口地址代理，解决跨域问题
       
     proxyTable: {
      "/api":{
        target:'http://localhost:8080',
          pathRewrite:{
          '^/api':'/static/mock'
          }
      }
    },

###7-9
axios接收的res值有两个data键值

this.city中的this 指向本组件
接口取值：
ajax接收的city→父组件Home.vue传给子组件home-header (用city属性接收)→子组件中用props接收后，显示在template模板上
![image](http://upload-images.jianshu.io/upload_images/9249356-7a9cc18f9cf3676f?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

![image](https://upload-images.jianshu.io/upload_images/9249356-04e687bb62537073.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/9249356-68279c213e30ef55.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

轮播图获取数据时，解决图片从最后一张开始播放
![image](https://upload-images.jianshu.io/upload_images/9249356-d4c8dd944df7297b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


