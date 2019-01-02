# 父子组件间传值
>- 父组件—>子组件：
        1.父组件使用 v-bind 绑定变量并赋值给变量。
        2.在子组件里使用 props 来接收父组件传递过来的值。
     >-   子组件—>父组件：
  1.子组件通过\$emit()方法向外派发事件，传递参数。
    this.\$emit('事件名',传递的参数);
  2.父组件通过监听子组件派发的事件来获得参数。
监听 @事件名="方法名" 方法名（value）{ .... //value=传递来的参数 }
 父组件取到值以后改变数据

```
 
<div id="root">
    <div>
        <input type="text" v-model="todoValue"/>
        <button @click="handleBtnClick">提交</button>
    </div>
    <ul>
        <todo-item v-bind:content="item"
                   v-bind:index="index"
                   v-for="(item,index) in list"
                   @delete="DeleteItem">

        </todo-item>
    </ul>
</div>

<script>

    var TodoItem = {
        props: ['content' ,"index"],
        template: "<li @click='Clickde'>{{content}}</li>",
        methods:{
            Clickde:function () {
                this.$emit("delete",this.index);
            }
        }
    }

    var app = new Vue({
        el: "#root",
        components: {
            TodoItem: TodoItem
        },
        data: {
            todoValue: "",
            list: []
        },
        methods: {
            handleBtnClick: function() {
                this.list.push(this.todoValue);
                this.todoValue = ""
            },
            DeleteItem:function (index) {
                this.list.splice(index,1);
            }
        }
    })
</script>
```

>- 父—>子： 父组件v-bind：变量名=“js表达式”  子组件：props获取
 **单项数据流:** 子组件不能直接修改父组件传递来的参数
>#####例
>![**错误示范**](https://upload-images.jianshu.io/upload_images/9249356-ee7b59563d76b68a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


>修改Object的值会导致别的引用了该对象的子组件内数据的变化，
用在子组件内复制一份该对象，修改子组件内自己的data来代替
![image.png](https://upload-images.jianshu.io/upload_images/9249356-111402ba3201adce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



#非父子组件间传值

