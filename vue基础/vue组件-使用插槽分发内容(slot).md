## slot--使用插槽分发内容（位置、槽口；作用: 占个位置）

**官网API**： [https://cn.vuejs.org/v2/guide/components.html#使用插槽分发内容](https://cn.vuejs.org/v2/guide/components-slots.html)

使用组件时，有时子组件不知道会收到什么内容，这是由父组件决定的。

![](https://upload-images.jianshu.io/upload_images/9249356-8754d5e5ff9a4cc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###一、单个插槽
```
1.my-component 组件:
<div>
    <h2>我是子组件的标题</h2>
    <slot>
        这段内容只有在没有要分发的内容时才会显示。
    </slot>
</div>

2.父组件：
<div>
    <h1>我是父组件的标题</h1>
    <my-component>
        <p>这是一些初始内容</p>
        <p>这是更多的初始内容</p>
    </my-component>
</div>

3.渲染结果：
<div>
    <h1>我是父组件的标题</h1>
    <div>
        <h2>我是子组件的标题</h2>
        <p>这是一些初始内容</p>
        <p>这是更多的初始内容</p>
    </div>
</div>
```

###二、具名插槽
slot根据不同的name名称分发内容，多个插槽可以有不同的名字。

仍然可以有匿名的默认插槽，为了找不到匹配的内容片段使用，如果没有默认插槽，这些找不到匹配的内容片段将被抛弃。

```
1.my-component 组件:
<div class="container">
    <header>
        <slot name="header"></slot>
    </header>
    <main>
        <slot></slot>
    </main>
    <footer>
        <slot name="footer"></slot>
    </footer>
</div>

2.父组件：

<my-component>
    <h1 slot="header">这里可能是一个页面标题</h1>
    <p>主要内容的一个段落。</p>
    <p>另一个主要段落。</p>
    <p slot="footer">这里有一些联系信息</p>
</my-component>

3.渲染结果：
<div class="container">
    <header>
        <h1>这里可能是一个页面标题</h1>
    </header>
    <main>
        <p>主要内容的一个段落。</p>
        <p>另一个主要段落。</p>
    </main>
    <footer>
        <p>这里有一些联系信息</p>
    </footer>
</div>
```

例子：
![Slot插槽.png](https://upload-images.jianshu.io/upload_images/9249356-bee5a2fa238c2251.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
