
   ###作用域
#####到目前为止所学的知识：
- 如果标识符在全局作用域内声明，则可以到处访问。
- 如果标识符在函数作用域内声明，则可以在所声明的函数内访问（甚至可以在函数中声明的函数内访问）。
 - 尝试访问标识符时，JavaScript 引擎将首先查看当前函数。如果没找到任何内容，则继续查看上一级外部函数，看看能否找到该标识符。将继续这么寻找，直到到达全局作用域。
- 全局作用域不是很好的做法，可能会导致糟糕的变量名称，产生冲突的变量名称和很乱的代码。

###作用域:使用范围
   
  >  * 全局变量:声明的变量是使用var声明的,那么这个变量就是全局变量,全局变量可以在页面的任何位置使用
    > * 除了函数以外,其他的任何位置定义的变量都是全局变量
    > * 局部变量:在函数内部定义的变量,是局部变量,外面不能使用
   >  * 全局变量,如果页面不关闭,那么就不会释放,就会占空间,消耗内存
 >
  >   * 全局作用域:全局变量的使用范围
  >   * 局部作用域:局部变量的使用范围
 >
  >   * 块级作用域:一对大括号就可以看成是一块,在这块区域中定义的变量,只能在这个区域中使用,但是在js中在这个块级作用域中定义的变量,外面也能使用;
  >   * 说明:js没有块级作用域,只有函数除外
    > * 隐式全局变量:声明的变量没有var,就叫隐式全局变量
    > * 全局变量是不能被删除的,隐式全局变量是可以被删除的
   >  * 定义变量使用var是不会被删除的,没有var是可以删除的

    

###提升
- JavaScript 会将函数声明和变量声明提升到当前作用域的顶部。
- 变量赋值不会提升。
- 在脚本的顶部声明函数和变量，这样语法和行为就会相互保持一致。

####函数表达式和提升
何时使用函数表达式及何时使用函数声明取决于几项内容，你将在下个部分看到几种使用方法。但是，需要注意的一点是提升。

所有函数声明提升和加载后，脚本才会实际地运行。函数表达式不会提升，因为它们涉及变量赋值，只有变量声明会提升。在解析器在脚本中到达该表达式之前，函数表达式不会加载。

函数提升例子：https://s3.cn-north-1.amazonaws.com.cn/u-vid-hd/tjLDNvyhDM8.mp4

####作为参数的函数
可以将函数存储在变量中使我们能够轻松地将函数传递到另一个函数中。传递到另一个函数中的函数叫做 回调。假设有个 helloCat() 函数，你希望它返回 "Hello"，后面跟着字符串“meows”，就像 catSays 一样。你可以使 helloCat() 接受回调函数，并传入 catSays，而不用手动操作。
```
// 函数表达式 catSays
var catSays = function(max) {
  var catMessage = "";
  for (var i = 0; i < max; i++) {
    catMessage += "meow ";
  }
  return catMessage;
};

// 函数声明 helloCat 接受一个回调
function helloCat(callbackFunc) {
  return "Hello " + callbackFunc(3);
}

// catSays 作为回调函数传入
helloCat(catSays);
```

#####内嵌函数表达式
函数表达式是指将函数赋为变量值。在 JavaScript 中，当你将函数作为参数内嵌传递给其他函数时，也会发生这种情况。例如下面的 favoriteMovie 示例：
```
// 将函数 displayFavorite 分配给变量 favoriteMovie 的函数表达式
var favoriteMovie = function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
};

// 函数声明有两个参数：一个显示消息函数和一个电影名称
function movies(messageFunction, name) {
  messageFunction(name);
}

// 调用 movies 函数，传入 favoriteMovie 函数和电影名称
movies(favoriteMovie, "Finding Nemo");
```
返回：My favorite movie is Finding Nemo

但是你可以通过将函数内嵌传递给 movies() 函数，绕过第一个函数赋值。
```
// 函数声明需要两个参数：一个显示消息的函数，以及一个电影名称
function movies(messageFunction, name) {
  messageFunction(name);
}

// 调用 movies 函数，传入一个函数和电影名称
movies(function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
}, "Finding Nemo");
```
Returns: My favorite movie is Finding Nemo

这种函数表达式，即将函数内嵌传递给其他函数的语法在 JavaScript 中很常见。一开始可能比较难懂，但是请保持耐心，不断练习，渐渐的就熟练了

---

##对象
对象字面值记法
var sister = {
  name: "Sarah", 
  age: 23,
  parents: [ "alice", "andy" ],
  siblings: ["julia"],
  favoriteColor: "purple",
  pets: true
};
你在上面看到的语法叫做对象字面值记法。在构建对象字面值时需要注意几个重要事项：

#####“键”（表示属性或方法名称）和它的“值”用冒号隔开了
#####键值对用逗号隔开
#####整个对象包含在花括号 { } 里。
和在字典中查找单词的定义一样，通过键值对中的键可以查找关于对象的信息。下面这几个示例展示了可以如何使用你所创建的对象获取我姐姐父母的信息。

// 两种等价的方法来使用 key(键) 来返回它的 value(值)
sister["parents"] // 返回 [ "alice", "andy" ]
sister.parents // 仍然返回 ["alice", "andy"]
sister["parents"] 叫做括号记法（因为使用了括号！），sister.parents 叫做点记法（因为使用了点！）。



#####对象是 JavaScript 中最重要的数据结构之一。你将到处看到它们！

它们具有属性（关于对象的信息）和方法（对象具有的函数或功能）。对象是非常强大的数据类型，当你使用 JavaScript 或任何其他面向对象编程语言时，将经常看到对象类型。

##对象字面值、方法和属性
你可以使用对象字面值记法定义对象：
```
var myObj = { 
  color: "orange",
  shape: "sphere",
  type: "food",
  eat: function() { return "yummy" }
};

myObj.eat(); // 方法
myObj.color; // 属性
```
##命名规则
可以随便使用大小写字母和数字，但是属性名称不要以数字开始。 字符串不需要放在引号里！如果是多个单词构成的属性，则采用驼峰式大小写形式。 属性名称里不要使用连字符
```
var richard = {
  "1stSon": true;
  "loves-snow": true;
};

richard.1stSon // 错误
richard.loves-snow // 错误
```

自定义构造函数创建对象,我要自己定义一个构造函数,自定义构造函数,创建对象
 ####函数和构造函数的区别；名字是不是大写(首字母是大写)
    function Person(name,age) {
      this.name=name;
      this.age=age;
      this.sayHi=function () {
        console.log("我叫:"+this.name+",年龄是:"+this.age);
      };
    }

    //自定义构造函数创建对象:先自定义一个构造函数,创建对象
    var obj=new Person("小明",10);
    console.log(obj.name);
    console.log(obj.age);
    obj.sayHi();

jsson也是一个对象,数据都是成对的,一般json格式的数据无论是键还是值都是用双引号括起来的

        var obj={
          name:"小明"
        };
      

        var json = {
          "name": "小明",
          "age": "10",
          "sex": "男"
    };
