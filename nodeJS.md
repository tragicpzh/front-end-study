# 模块

## 规范

### CommonJS

Node.js 是 commonJS 规范的主要实践者，它有四个重要的环境变量为模块化的实现提供支持：module exports require global
同步加载模块，在服务端读取很快

### AMD(require.js)

异步加载模块。依赖前置，提前执行（有可能加载没用到的模块，浪费资源）
require.config()指定引用路径
define()定义模块
require()加载模块

### CMD(sea.js)

异步加载模块。依赖就近，延迟执行（使用时才加载，性能差）
define()定义模块
require()加载模块

### ES6

exports 定义模块
import 加载模块

## CommonJS vs ES6

1.CommonJS 输出一个值的拷贝
ES6 输出一个值的引用
2.CommonJS 模块运行时加载：加载模块-生成对象-读取方法
ES6 模块编译时输出：加载输出值而不是模块-静态解析阶段就会生成

## 作用

1.不需要命名空间，不需要全局变量，解决了命名冲突的问题
2.require 引入依赖，让开发者只需关心当前模块的依赖 3.提高可维护性 4.异步加载模块，提高前端性能

# 多线程与异步 I/O

## 多线程

创建多个线程（线程池），来处理区别于主线程的事件

## 异步 I/O

    实现的核心为：事件循环、观察者、请求对象、I/O 线程池
    事件循环：提供一种机制，能够在有事件时执行事件并执行回调函数，没有事件时退出
    观察者：判断是否有事件需要执行
    请求对象：保存了回调函数和等待执行的状态
    I/O 线程池：多个线程来处理 I/O，管理线程的分配

## 异步 I/O 的优点

    1.利用单线程来避免多线程死锁、状态同步等问题
    2.利用异步I/O远离阻塞，高效利用CPU

# 异步编程

## 难点

    1.异常处理:难以确定异常发生的阶段
    2.函数嵌套过深:函数嵌套过深(回调地狱),node中经常会有多个嵌套的回调函数
    3.阻塞代码:没有sleep()这样的阻塞函数
    4.多线程编程:node为单线程编程,虽然提供了child_process、cluster,但没有广泛应用
    5.异步转同步:只能依靠库、编译或者良好的流程控制

## 解决方案

### 事件发布/订阅者模式

      1.node提供了events模块，不存在事件传递的机制，它具有addListener/on,once,removeListener,removeAllListeners,emit等基本事件监听模式的方法
      2.利用钩子(hook)来导出内部数据或状态给外部调用者，以使编程者不用关注组件时如何启动和执行的

### Promise/Deferred

    1.Promise/A
      三种状态：pending resolved rejected
      提供then() 接受完成、错误及可选的progress
      then()只接受function
      then()返回promise实现链式调用
      Deferred来触发执行这些回调函数，用于维护异步模型的状态
    2.promise多异步协作
      使用all()方法抽象多个异步操作，只有异步操作都成功时，才算成功
    3.Promise进阶知识
      让promise支持链式执行：
          回调存入队列
          promise完成时，逐个执行回调，监测到返回了promise则停止执行并改写原promise，并转交回调函数

### 流程控制库

#### 尾触发与 next

尾触发的关键字为 next,类似于中间件模式

#### async

callback 的参数均为(err,data)
1.series()实现任务串行
2.parallel()实现任务并行
3.waterfall()实现任务的依赖串行
4.auto()实现自动依赖处理

#### step

callback 的参数均为(err,data)
Step(task1,task2...)串行处理任务
callback 为 this:串行处理
callback 为 this.parallel:并行处理
var group=this.group(); callback 为 group：并行处理

#### wind
