>绑定样式的几种方法：
1、v-bind:class和对象（通过true或false）
2、v-bind:class和数组（可设置多个值,数组内的每一项都是对象）
3、v-bind:style="一个对象"
4、v-bind:style="数组"(数组内的每一项都是对象）
即：
1、class绑定对象
2、class绑定数组
3、style绑定对象
4、style绑定数组

>在Vue对象中，样式的类名要用驼峰写法fontSize，不能用font-size
v-bind:style 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。
CSS 属性名可以用驼峰式 (camelCase)或短横线分隔 (kebab-case，记得用单引号括起来) 来命名

```
 <div id="vm">
       一： class 数组写法
        <!-- <div :class="[activeCl,fontSizeCl] "
              @click="DivClick"   >
            Hello World
        </div>-->
        二： style数组写法
      <div :style="[fontCl,activeCl,{backgroundColor:'red'} ]"
             @click="DivClick" >
            Hello World
        </div>
    </div>


    <script>
        var vm =new Vue({
            el: "#vm",
            data:{
                activeCl:{
                        color:"blue"
                },
                fontCl:{
                     fontSize:'40px'
                }
            },
            methods:{
                DivClick:function () {

                    this.activeCl.color=this.activeCl.color==="blue"?"black":"blue"
                }
            }
        })
    </script>
```
