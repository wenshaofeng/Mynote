##简单动画
```
  将要实现动画效果的 DOM 节点用 transition 标签包裹起来，可添加 name 属性；
  若没有 name 属性，则默认的 class 前缀为 v
    <style>
        .fa-enter,.fa-leave-to{
           opacity: 0;
        }
        .fa-enter-active,.fa-leave-active{
            transition:  opacity 3s;
        }
    </style>
  <div id="root">
           <transition name="fa">
                <div v-if="show">hello world </div>
            </transition>

        <button @click="handleClick">{{change}}</button>
  </div>
```
**transition动画过渡原理**
```
  transition动画过度原理
        v-enter{ opacity： 0}    v-enter-active{transition:opacity 3s}
        动画执行之前vue会在被<transition>包裹的组件上添加两个类
          <div class="v-enter v-enter-active"></div>

          显示：开始：v-enter v-enter-active（o=0）
               →第二帧 v-enter-to v-enter-active(o=1) 
               →两个类消失
            v-enter-active存在于整个动画执行的过程中
            v-enter在动画开始时存在，动画执行到第二帧v-enter类被移除
            v-enter-to出现，opacity变成1, v-enter-active监听到这个变化，并用三秒完成
          隐藏：开始：v-leave v-leave-active（o=1）
           →第二帧 v-leave-to v-leave-active(o=0) 
            →两个类消失
            v-leave-active存在于整个动画执行的过程中
            v-leave在动画开始时存在，动画执行到第二帧v-leave类被移除
            v-leave-to出现，opacity变成0, v-enter-active监听到这个变化，并用三秒完成
            -->
```
##引用animate.css 库
> 使用自定义的 类名，将 transition 标签中，添加，enter-active-class 属性，
        值为自定义的名字，
        使用 animation库 填写 ‘animated xxx’
        进入时设 enter-active-class = ''
        离开时设 leave-active-class = ''
         刷新页面时有入场效果需要加入appear 属性和
        自定义class：appear-active-class="自定义类名"
      使用  :duration="{ enter: 200, leave: 400 }"  来分别设置 入场的时长 和 离场的时长 
        :duration="1000"统一设置

![](https://upload-images.jianshu.io/upload_images/9249356-9029953a8cf843a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##使用钩子函数和列表动画
**钩子函数**
> Vue 把一个完整的动画，使用钩子函数，拆分为了两部分：
  我们使用 flag 标识符，来表示动画的切换；
  刚以开始，flag = false  ->   true   ->   false

![vue动画.png](https://upload-images.jianshu.io/upload_images/9249356-030902fe80030e67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


