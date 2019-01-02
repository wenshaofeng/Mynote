　　　　Lazy Load 是一个用 JavaScript 编写的 jQuery 插件. 它可以延迟加载长页面中的图片. 在浏览器可视区域外的图片不会被载入, 直到用户将页面滚动到它们所在的位置. 这与图片预加载的处理方式正好是相反的.在包含很多大图片长页面中延迟加载图片可以加快页面加载速度. 浏览器将会在加载可见图片之后即进入就绪状态. 在某些情况下还可以帮助降低服务器负担。

　　　　一、下载和引用

　　　　　　官网下载地址：[http://plugins.jquery.com/lazyload/](http://plugins.jquery.com/lazyload/)

　　　　　　Lazy Load 依赖于 jQuery. 所以需要引用2个js
 ```
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="jquery.lazyload.js"></script>
```
　　　　二、简单调用

　　　　　　要使用懒加载，需要改变img的src标签
```

    html代码
      <img alt="" width="640" height="480" data-  original="img/example.jpg" />
    js代码
    $(function() {
        $("img").lazyload();
        });
```

这样设置就会将所有的img的并且拥有data-original标签的图片更改为懒加载。

**备注：这里必须设置图片的`width`和`height`,否则插件可能无法正常工作。**

　　上面是最简单的调用，但是一般而言，我们还有一些特殊的需求，比如想要提前一点点加载，避免网络过慢时加载缓慢，加载隐藏图片等等，lazyload都为我们提供相应的参数。

####1.设置临界点

　　　　默认情况下图片会出现在屏幕时加载. 如果你想提前加载图片, 可以设置`threshold `选项, 如：设置 threshold 为 200 令图片在距离屏幕 200 像素时提前加载.

    $("img").lazyload({
    threshold : 200
    });

####2.使用特效

　　　　默认情况下，图像完全加载并调用`show()`。你可以使用任何你想要的效果。下面的代码使用`fadeIn `（淡入效果）
```
$("img").lazyload({
    effect : "fadeIn"
});
```
####3.当图片不连续时

　　滚动页面的时候, Lazy Load 会循环为加载的图片. 在循环中检测图片是否在可视区域内. 默认情况下在找到第一张不在可见区域的图片时停止循环. 图片被认为是流式分布的, 图片在页面中的次序和 HTML 代码中次序相同. 但是在一些布局中, 这样的假设是不成立的. 不过你可以通过 `failurelimit` 选项来控制加载行为.
```
$("img").lazyload({
    failure_limit : 20
});
```
　　将 failurelimit 设为 20 ，当插件找到 20 个不在可见区域的图片时停止搜索.

####4.加载隐藏图片

　　当界面有很多隐藏图片的时候并希望加载他们的时候则使用`kip_invisible` 属性，将其设置为false
```
$("img").lazyload({ 
    skip_invisible : false
});
```
　　到这里，上面的方法已经基本满足常规的懒加载使用了，还有特殊的使用，可查看官网API。

demo
[基本选项](http://www.w3cways.com/demo/LazyLoad/enabled.html)
[淡人效果](http://www.w3cways.com/demo/LazyLoad/enabled_fadein.html)
[对不支持JavaScript浏览器的降级处理](http://www.w3cways.com/demo/LazyLoad/enabled_noscript.html)
[水平滚动](http://www.w3cways.com/demo/LazyLoad/enabled_wide.html)
[容器内水平滚动](http://www.w3cways.com/demo/LazyLoad/enabled_wide_container.html)
[经过五秒的延迟后加载](http://www.w3cways.com/demo/LazyLoad/enabled_timeout.html)
[用AJAX加载](http://www.w3cways.com/demo/LazyLoad/enabled_ajax.html)
