
##计算属性


#####计算属性，以及其和方法、侦听器的对比
>- computed（计算属性）性能相对较高，计算属性的结果会被缓存，
  除非依赖的响应式属性变化才会重新计算。
 > - watch（监听属性），一个对象，键是需要观察的表达式，值是对应回调函数，跟computed 类似，有缓存机制，但代码冗余。
> - methods（方法属性），没有缓存机制，当数据发生变化，重新渲染页面时,会重新执行页面调用的方法。
```
    <div id="app">
        <input type="text" v-model="name">
        <input type="text" v-model="age" >
        <div>
            {{fullMessage}}
        </div>
    </div>
    <script>

        var app = new Vue({
            el:"#app",
            data:{
                name : "Li",
                cla: "three",
                age: 21,
                fullMessage:"Li three"
            },
            /*  一：计算属性*/
            computed:{
                fullMessage :function () {
                    console.log("计算了一次");
                    return this.name+ " "+ this.cla ;
                }
            }
         /*  二：方法*/
            methods:{
                fullMessage :function () {
                    console.log("计算了一次");
                    return this.name+ " "+ this.cla ;
                }
            }
          /*三：监听器*/
            watch:{
                name: function () {
                    console.log("计算了一次");
                    this.fullMessage = this.name + " "+ this.cla;
                },
                cla: function () {
                    console.log("计算了一次");
                    this.fullMessage = this.name + " "+ this.cla;
                }
            }
        });
    </script>
```

##watch
- 监听路由变化
![image.png](https://upload-images.jianshu.io/upload_images/9249356-561974b518a0df2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
