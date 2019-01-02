## Babel安装与说明

在webpack中只能处理一部分ES6语法，一些更高级的ES6或ES7语法不能处理，这是就需要第三方的loader来处理这些语法。

通过Babel，可以帮我们完成这一转换。

###安装

+ 在webpack，通过运行如下两套命令，安装两套包，安装Babel相应的loader功能；

	- 第一套包：`npm i babel-core babel-loader babel-plugin-transform-runtime -D`

	- 第二套包：`npm i babel-preset-env babel-preset-stage-0 -D`

###配置
**webpack配置文件中**
```
{test: /\.js$/ , use : 'babel-loader' ,exclude: /node_modules/ }
```
- 注意：在配置babel的loader规则时，必须把node_modules目录通过，exclude选项排除掉，原因有两个:

	- 避免无意义的转换 否则 Babel 会把 node_modules 中所有的 第三方 JS 文件，都打包编译

	- 转换完毕，项目也无法正常运行

**.babelrc配置**
>.babelrc属于JSON格式，在写配置的时候，必须符合JSON语法规范： 不能写注释，字符串必须用双引号
```
{
   "presets": ["env", "stage-0"],
   "plugins": ["transform-runtime"]
}
```
>bug
![](https://upload-images.jianshu.io/upload_images/9249356-da878e3b52b77b28.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解决方案 
`npm uninstall -D babel-loader`卸载babel-loader，指定`npm install -D babel-loader@7`的版本安装。

## 几点说明

+ 第一套包：`npm i babel-core babel-loader babel-plugin-transform-runtime -D` 第一套包为babel的转换工具

+  第二套包：`npm i babel-preset-env babel-preset-stage-0 -D`第二套包为babel的语法

+  第一套包只负责转换，是转换器，但不知道对应关系

+  第二套包只负责对应关系

+ babel-preset-env是比较新的ES语法插件，之前我们安装的是babel-preset-se2015，但我们安装的这个babel-preset-env包含了所有ES相关的语法。
