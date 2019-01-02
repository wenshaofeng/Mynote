
```
<body>
  <div id="app">
    <p>444444</p>
  </div>

  <script>

    var login = {
      template: '<h1>这是登录组件</h1>'
    }

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      // createElements 是一个 方法，调用它，能够把指定的组件模板，渲染为 html 结构
      render: function (createElements) { 
        return createElements(login)
        // 注意：这里 return 的结果，会 替换页面中 el 指定的那个 容器
      }
    });
  </script>
</body>
```
渲染结果
![](https://upload-images.jianshu.io/upload_images/9249356-fdcae7af17d6a35b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
