# [Vue.js双向绑定的实现原理](https://www.cnblogs.com/kidney/p/6052935.html)


###MVC和MVVM模式
![MVC和MVVM的关系图解](https://upload-images.jianshu.io/upload_images/9249356-aea17a0e02c14d3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/9249356-b463bee03d732cd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#####最简单的Vue应用

![image.png](https://upload-images.jianshu.io/upload_images/9249356-56cb54a4a81ed111.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##v-cloak
![](https://upload-images.jianshu.io/upload_images/9249356-4aa12cd5afcea748.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##v-bind 、v-on、v-model

>属性绑定  v-bind:    <div v-bind:title="dataTitle"></div>
简写为“:”<div :title="dataTitle"></div>
“dataTitle”引号内是JS表达式，“‘xxx’+dataTitle”
双向数据绑定  v-model="dataCont"

>- v-on（事件）的缩写是@
>- v-bind（绑定属性）的缩写是：
v-bind 只能实现数据的单向绑定，从 M 自动绑定到 V， 无法实现数据的双向绑定
>- v-model（数据双向绑定）
  注意： v-model 只能运用在 表单元素中

####事件修饰符
```
     <!--使用  .stop  阻止冒泡 -->
     <div class="inner" @click="div1Handler">
      <input type="button" value="戳他" @click.stop="btnHandler">
    </div>

     <!--使用 .prevent 阻止默认行为 -->
     <a href="http://www.baidu.com" @click.prevent="linkClick">有问题，先去百度</a>

     <!--使用  .capture 实现捕获触发事件的机制 -->
     <div class="inner" @click.capture="div1Handler">
      <input type="button" value="戳他" @click="btnHandler">
    </div>

     <!--使用 .self 实现只有点击当前元素时候，才会触发事件处理函数 -->
     <div class="inner" @click.self="div1Handler">
      <input type="button" value="戳他" @click="btnHandler">
    </div>

    <!-- 使用 .once 只触发一次事件处理函数 -->
     <a href="http://www.baidu.com" @click.prevent.once="linkClick">有问题，先去百度</a>


    <!-- 演示： .stop 和 .self 的区别 -->
     <div class="outer" @click="div2Handler">
      <div class="inner" @click="div1Handler">
        <input type="button" value="戳他" @click.stop="btnHandler">
      </div>
    </div>

    <!-- .self 只会阻止自己身上冒泡行为的触发，并不会真正阻止 冒泡的行为 -->
     <div class="outer" @click="div2Handler">
      <div class="inner" @click.self="div1Handler">
        <input type="button" value="戳他" @click="btnHandler">
      </div>
    </div>
```

>- 计算属性，计算data内属性
> ```  
  >computed:{
   >     fullName : function(){
    >              xxxxxxxx
     >               return something ;
     >         }
  >  }

>- 侦听器，监测某一数据或计算属性发生变化时执行function
watch:{}
## v-if 、v-show 、v-for
>v-if  控制dom存在与否
v-show 控制dom显示与否
v-for 控制一组数据，循环显示
<li v-for="(item , index) of list" :key="index">{{item}}<li>
加 key 值提升渲染效率，渲染性能
key 值要求唯一性

>1: v-if和v-show的不同之处，就是v-show只是将dom元素用了display隐藏显示起来了，
  >而v-if则是通过判定是佛满足属性需求确定挂不挂在dom元素，性能上v-show是比v-if高的，
        但是v-if有v-else-if和v-else可以用，可用性高些；
        2:关乎于input中的例子，当元素改变时候，vue会尝试去复用已经存在的dom,
        而这样就可能会导致一些小bug,比如一个文本框的值在另一个还是会被复用
        ，这时候就加上一个key值，问题就能解决。由此后续需要深入理解vue中的虚拟dom机制。
**v-for循环的是使用其的DOM元素对象本身，注意使用v-for的位置**



###组件可以分为全局组件和局部组件

>+ 全局组件定义之后可以在模板里的任何地方调用
>+ 局部组件需要通过components在实例里进行注册才能使用，vue模板里的属性使用必须要通过props来接收
![image.png](https://upload-images.jianshu.io/upload_images/9249356-d62e7bf8dcef907a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
  /* 第二部分 组件化 */
     /*
    父组件的数据通过 props :[] 来向子组件传递，每一次list里的item通过v-bind 向子组件传递，
        子组件通过props 接收。
    template 模板里要用插值表达式{{}} 会替换掉组件的内容
    局部组件需要注册
   */
    <div id="app">
        <input type="text" v-model="inputValue">
        <button @click="submit">提交</button>
        <ul>
            <todo-item  :content = "item"
                        v-for="item in list">
            </todo-item>
        </ul>
    </div>

    <script>
         /*全局组件*/
    /*    Vue.component("todo-item",{
            props:['content'],
           template: "<li> {{content}}</li>"
        });*/

        var TodoItem ={
            props:['content'],
            template: "<li> {{content}}</li>"
        };
        var app = new Vue({
            el:"#app",
            data:{
                inputValue:"",
                list : []
            },
            components:{
                TodoItem:TodoItem
            },
            methods:{
                submit:function () {
                        this.list.push(this.inputValue);
                        this.inputValue="";
                }
            }

        })

    </script>
```
###创建组件的方式
![](https://upload-images.jianshu.io/upload_images/9249356-786652c31a72cf3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###切换组件
**1. v-if和v-else**
**2. :is属性切换**
![](https://upload-images.jianshu.io/upload_images/9249356-7d06427b03e8dfe7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
