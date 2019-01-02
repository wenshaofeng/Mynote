>1、is属性：解决标签规范造成的bug（如table、ul、select内）
   2、**非根组件中data必须是函数**，返回一个对象（为了保证每一个子组件数据的唯一性，避免多个子组件数据共享）
    3、操作dom：通过在标签上加ref属性，可通过**this.$refs.xxx**取得该dom节点，如果是在组件上添加了ref属性，则取得的是该组件的引用
![ref](https://upload-images.jianshu.io/upload_images/9249356-51edda65919b5cb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-7b90c9df1926f499.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![$refs](https://upload-images.jianshu.io/upload_images/9249356-92ca1fcd57791be6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-20ac6b542a1ffaa4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

