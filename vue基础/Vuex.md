####State
- 唯一数据源
- 单一状态树
####Getters
- 通过Getters可以派生出一些新的状态
####Mutations
- 更改Vuex的store中的状态的唯一方法是提交mutation
![](https://upload-images.jianshu.io/upload_images/9249356-aea01fde0d78eb75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####Actions
- Action 提交的是mutation，而不是直接变更状态
- Action 可以包含任意异步操作
####Modules
- 面对复杂的应用程序，当管理的状态比较多时，我们需要将Vuex的store对象分割成模块（modules）
