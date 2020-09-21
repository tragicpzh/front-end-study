# 简介

webpack 是一个现代 js 应用程序的`静态打包模块(module bundler)`

# 核心概念

入口 entry
输出 output
loader
插件 plugins

# 入口

指示从哪个模块开始建构`依赖图`，可以有多个入口

## 用法

```javascript
entry: {
  xxx: xxx;
  yyy: yyy;
}
entry: ["xxx", "yyy"];
```

# 出口

指示在哪里输出创建的`bundler`，以及如何命名，默认为'./dist'

## 用法

```javascript
一个入口
output:{
  filename:'xxx.js',
  path:'yyy'
}
多个入口
output:{
  filename:'[name].js',
  path:_dirname+'/dist'
}
CDN
output:{
  path:'xxx/[hash]'
  publicPath:'xxx/[hash]/'
}
```

# loader

转译器，让 webpack 能够去处理那些非 js 文件

```javascript
module: {
  rules: [
    {
      test: /\.txt$/,
      use: "raw-loader",
    },
  ];
}
```

## 配置

允许使用多个 loader

## 特性

loader 支持链式传递，对资源使用 pipeline,执行顺序为相反的顺序
loader 可同步可异步
loader 运行在 Node.js 中
loader 接收查询参数
loader 能使用 options 配置

## 解析 loader

loader 从模块路径开始解析(node_module)

# 插件

```javascript
plugins: [new xxxx()];
```

## 剖析

插件是一个具有 apply 属性的 js 对象，会被 webpack compiler 调用

# 模式

mode:'production' or 'development'

# 模块 module

在模块化编程中，开发者将程序分解成离散功能块，称之为模块

## 引入

import require define require @import

## 支持的模块类型

通过 loader 可以支持各类语言和预处理编写模块。

# 模块解析

webpack 使用`enhanced-resolve`来解析路径

## 解析规则

绝对路径
相对路径-添加上下文路径，以产生模块的绝对路径
模块路径

### 模块路径

```
import "module"
```

模块将在`resolve.module`中指定的所有目录内搜索
初始模块路径可以使用`resolve.alias`来配置别名

## loader 解析

`resolveLoader`可以为 Loader 提供独立的解析规则

# 依赖图

从 entry 开始，递归地构建一个依赖图，这个依赖图包含着应用程序所需的每个模块。然后将这些模块打包为少量的 bundle

# Runtime

runtime,以及伴随的 mainfest 数据，是 webpack 用来连接模块化的应用程序的所有代码。

# Mainfest

当编译器开始执行、解析、映射程序时，所有模块的详细要点会被存储在 mainfest 中。
完成打包后发送至浏览器，会在运行时通过 mainfest 来解析和加载模块。

# targets

webpack提供了多种构建目标(target)，浏览器和服务器均可

# hot module replacement 模块热替换

1.保留在完成重新加载页面时丢失的应用程序状态
2.只更新变更内容，以节省宝贵的开发时间
3.调整样式更加快速，几乎相当于在浏览器调试器中更改样式
```javascript
    const webpack=require('webpack');
    module.export={
        enrty:{
            app:'./src/index.js'
        },
        devServer:{
            hot:true
        },
        plugins:[
            new webpack.NameModulesPlugin(),
            new webpack.HotModuleReplacementPlugin(),
        ]          
    } 
//css的模块热替换
    module.exports={
        module:[
            {
                test:/\.css$/,
                use:['style-loader','css-loader']
            }   
        ]
    }   
```
# 模块的四种规范
## CommonJS
    1.模块的导入require()
    2.模块的定义module.exports={}
    3.浏览器不兼容，缺少环境变量如module,global
    4.循环加载
    
## AMD
## CMD
## ES6

