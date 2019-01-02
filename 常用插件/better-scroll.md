###[中文文档](https://ustbhuangyi.github.io/better-scroll/doc/zh-hans/#better-scroll%20%E6%98%AF%E4%BB%80%E4%B9%88)
##[当 better-scroll 遇见 Vue](https://www.imooc.com/article/18232)
基本结构
```
<div class="wrapper">
    <ul class="content">
      <li>...</li>
      <li>...</li>
    ...
    </ul>
</div>
```
![](https://upload-images.jianshu.io/upload_images/9249356-e6ef94e253edca2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1. 检查HTML的结构
2. 检查better-scroll是否初始化时机太早（dom没有完全生成，已经初始化了），可以使用vue的$nextTick来异步初始化better-scroll
3. better-scroll在使用的时候，滚动只作用于第一层元素，因此在使用better-scroll时，better要加上一层div**(div下面再放其他东西，better里不能有同级的2及以上div）**

