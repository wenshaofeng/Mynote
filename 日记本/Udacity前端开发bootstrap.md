![媒体查询](https://upload-images.jianshu.io/upload_images/9249356-93b3ee50343a6fd6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1480)

![栅格参数](https://upload-images.jianshu.io/upload_images/9249356-0c4ca0293e08fdff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![实例](https://upload-images.jianshu.io/upload_images/9249356-1b7b329810ea2b3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

要在你的实战项目中使用 Bootstrap 文件，只需将 css 和 js 文件夹复制到你的实战项目文件夹即可。不要忘了将文件加入到你的 head 元素中。

`<link rel="stylesheet" href="css/bootstrap.min.css">`

`<script src="js/bootstrap.min.js"></script>`

**注**： CSS 缩小默认不会自动发生，因此，如果你编辑了你的未缩小的 CSS 文件，但却将缩小版本加入了你的 HTML，则页面不会默认使用更新的 CSS。

你可以通过 [http://cssminifier.com/](http://cssminifier.com/) 这样的网站手动缩小你的 CSS。

也可以采用更为高级的自动工作流程来自动缩小 CSS 文件，例如，可采用你的代码编辑器的插件或采用 [Gruntjs](http://gruntjs.com/) 这样的构建系统。

