# [NPM install -save 和 -save-dev 傻傻分不清](https://www.cnblogs.com/limitcode/p/7906447.html)


`npm install module_name -S `   即    `npm install module_name --save`    写入dependencies

`npm install module_name -D `   即   ` npm install module_name --save-dev` 写入devDependencies

`npm install module_name -g` 全局安装(命令行使用)

`npm install module_name` 本地安装(将安装包放在 ./node_modules 下)



dependencies与devDependencies有什么区别呢？

devDependencies 里面的插件只用于开发环境，不用于生产环境

dependencies 是需要发布到生产环境的

有点儿不好理解，别怕，举个例子就好：

你开发一个前端项目，在项目中你需要使用gulp构建你的开发和本地运行环境,这时你就要放到dependencies里。gulp是你用来压缩代码，打包等需要的工具，程序实际运行的时候并不需要，所以放到dev里就ok了。

你写程序要用element-ui,生产环境运行项目时肯定要用到element-ui,这时element-ui就应该安装到dependencies中去。

