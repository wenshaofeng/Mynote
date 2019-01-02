###[nvm的安装详解](https://mp.weixin.qq.com/s?__biz=MzA4MTg4MDI5OQ==&mid=2456038545&idx=1&sn=41f4d090c1fa18c10a224eeeeccd8771&chksm=881eb915bf69300368e17f28ef4bd11c8846a44bb07392ae784e19f08f2bed862c255cecd50e&mpshare=1&scene=1&srcid=1212W3pP488gFWMucwBzpvuv&pass_ticket=nh4oRlJ5XQDdW7RkRbYiDfZ7EfL9%2F0qOFWiyYrH%2FYs%2BMeee1WIF1bfHjdI3p86yi#rd)

####[nvm管理node版本，npm管理node包](https://www.jianshu.com/p/a1b797b25bc7)
![](https://upload-images.jianshu.io/upload_images/9249356-ea70f8769fa052bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##npm的使用
###[安装npm及cnpm(Windows)](https://www.cnblogs.com/liaojie970/p/9296177.html)
### [常用的 npm 命令](https://segmentfault.com/a/1190000007683367)

##npm换源


### `nrm`的安装使用
作用：提供了一些最常用的NPM包镜像地址，能够让我们快速的切换安装包时候的服务器地址；
什么是镜像：原来包刚一开始是只存在于国外的NPM服务器，但是由于网络原因，经常访问不到，这时候，我们可以在国内，创建一个和官网完全一样的NPM服务器，只不过，数据都是从人家那里拿过来的，除此之外，使用方式完全一样；
1. 运行`npm i nrm -g`全局安装`nrm`包；
2. 使用`nrm ls`查看当前所有可用的镜像源地址以及当前所使用的镜像源地址；
3. 使用`nrm use npm`或`nrm use taobao`切换不同的镜像源地址；

> 注意： nrm 只是单纯的提供了几个常用的 下载包的 URL地址，并能够让我们在 这几个 地址之间，很方便的进行切换，但是，我们每次装包的时候，使用的 装包工具，都是  npm 
