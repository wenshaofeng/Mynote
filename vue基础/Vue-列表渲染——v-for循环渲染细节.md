>1、v-for表达式中推荐使用'item of list'形式
2、每个item使用:key时，它的值不推荐使用item的索引作为唯一值，而是推荐使用从后台返回的唯一值，即id，这样可以提高性能。
3、vue中，直接改变数组下标，数据已更新，但是不会被渲染到页面上，可以用push、pop/shift、unshift/splice/sort/reverse修改数组内容来实现页面的更新，或者修改数组对象的引用。
4、使用template来包裹多个列表，该标签不会被渲染到页面上。
![image.png](https://upload-images.jianshu.io/upload_images/9249356-fb0093a9df778838.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/9249356-33e5007304645457.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 **不能通过 arr[index] 修改数据，进行视图渲染，**
  >有三种方式实现可以数据变化页面也变化
        1、直接改变数组或对象的引用；
        2、使用数组的变异方法；（针对数组）**7个方法（push/shift/pop/unshift/splice/sort/reverse）**
        3、使用Vue.set()或 vm.\$set()方法； Vue.set(obj, key, value)
                                             vue.$set(obj, key, value)
    * vue 提供一个 set 方法，向一个对象中添加数据，当数据改变时，页面也会随之变化.*

vue 提供一个 set 方法，向一个对象中添加数据，当数据改变时，页面也会随之变化。

- 对象：
全局模式下的使用方式：Vue.set(obj, key, value)
vue 实例下实现：vue.$set(obj, key, value)

- 数组：
全局模式下的使用方式：Vue.set(arr, index, value)
vue 实例下实现：vue.$set(arr, index, value)

####遍历对象
![遍历对象](https://upload-images.jianshu.io/upload_images/9249356-83e6f95cc55597d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####循环嵌套
![循环嵌套](https://upload-images.jianshu.io/upload_images/9249356-e8a0223a9676e30a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####迭代数字
```
<div id="app">
    <!-- in 后面我们放过  普通数组，对象数组，对象， 还可以放数字 -->
    <!-- 注意：如果使用 v-for 迭代数字的话，前面的 count 值从 1 开始 -->
    <p v-for="count in 10">这是第 {{ count }} 次循环</p>
  </div>
```
![](https://upload-images.jianshu.io/upload_images/9249356-85ad09de295a934d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####使用:key
#### [为什么使用v-for时必须添加唯一的key?](https://segmentfault.com/a/1190000013810844)

> 1.v-for 循环的时候，key 属性只能使用 number获取string 
>2.key 在使用的时候，必须使用 v-bind 属性绑定的形式，指定 key 的值
>3.在组件中，使用v-for循环的时候，或者在一些特殊情况中，如果 v-for 有问题，必须 在使用 v-for 的同时，指定 唯一的 字符串/数字 类型 :key 值 
