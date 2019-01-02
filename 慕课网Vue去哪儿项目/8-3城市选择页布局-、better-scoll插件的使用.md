布局
BFC的使用
![image.png](https://upload-images.jianshu.io/upload_images/9249356-40aa510aeb018ec7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
伪类元素的使用（stylus语法
&符号表示和当前class同级的元素，否则指下级元素）
![image.png](https://upload-images.jianshu.io/upload_images/9249356-d894468c76be407c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 

 ####Better-scoll 的使用
1. 安装` npm i better-scroll --save`
2. 组件中引入 ` import bscroll from 'better-scroll'`
3. 使用 `const wrapper = document.querySelector('.wrapper')`
            `const scroll = new BScroll(wrapper)`

![image.png](https://upload-images.jianshu.io/upload_images/9249356-5e1445d33aad9a78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-c7d0ef2c7ad53291.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> **注意DOM的结构要符合插件所提供的结构**
基本语法：var myscroll = new BScroll('.wrapper');
这里的  '.wrapper'是容器的class 
基本结构是 
```
<div class='wrapper'>
      <ul class='content'>
          <li></li>
      </ul>
</div>
```
**BScroll的挂载点 必须在父元素  且父元素的高度要低于子元素高度**

####ref属性的使用
![image.png](https://upload-images.jianshu.io/upload_images/9249356-3f8c756a0ea398b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/9249356-ac813f3b657d47a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

