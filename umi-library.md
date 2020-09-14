# 1.简介

基于 rollup 的打包工具
将模块化的组件内容打包为一个文件

# 2.打包选项

## cjs --ES5(node)

commonJS
module.exports=xxx;

## esm --ES6(浏览器)

export xxx;

## babel

转为 ES5 语法

## target

node 或 browser，转为对应适用的格式

## umd

前后端均适用的打包模式
判断顺序为:node(module.exports)
AMD(define)
window||global

## 配置文件

umirc.library.js .fatherrc.js .fatherrc.ts
语法为 ES6
配置项
esm:{
type:'rollup',
mjs:true //将依赖导入，默认为 false
}
cjs:{
type:'rollup'
}
entry://入口文件
file://npm 输出文件
cssModules://是否开启 cssModules
doc://docz 配置
