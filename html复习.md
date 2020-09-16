# 综述
## html的作用
    html是一个标识性语言，所以它包含一系列标签，但是不负责网页主要内容的呈现。作为网页的结构层。
## html的相关标准
    html1.0~5.0，超文本标记语言，目前主流为html5
    xml，可扩展标记语言
    xhtml,基于xml的html语言,html的扩展，语法上更严格
    sgml，标准通用标记语言，描述文档结构，在web出现前就存在
## html的元素分类
    1.块元素
        <div> <p> <h1> <ol> <ul> <dl> <table> <address> <blockquote> 
    2.行内元素
        <a> 链接
        <span> 行内标签
        <i>（引用） <em> <strong> <lable> <q>(短引用) <var> <cite> <code> 跟文本相关的标签
    3.行内块元素
        <img>
        <input>
    
    块元素：独占一行，可指定宽、高
    行内元素：与其他元素在一行内，宽高由内容决定
    行内块元素：与其他元素在一行内，可指定宽高
## html5新特性
### 新元素
    1.结构性元素 
    上下文结构的定义
    <section> <header> <footer> <nav> <article>
    2.级块性元素
    web页面的划分
    <aside> <figure> <code> <dialog>
    3.行内语义性元素
    web页面具体内容的引用和描述
    <meter> <time> <progress> <video> <audio>
    4.交互性元素
    功能性的内容表达
    <details> <datagrid> <menu> <command>
### `<canvas>`
    1.只有两个可选属性，height,width，作为画布的大小
    2.js操作
        var canvas=document.getElementByTagname('canvas')
        var ctx=canvas.getContext('2d')//canvas的接口实例
        绘制矩形、绘制路径、绘制圆弧等各类操作
### 拖放API
    标签属性：draggable=true/false,ondragstart等drag生命周期属性，属性值为执行的脚本。
### web worker 
    加载一个脚本文件，进而创建一个独立工作的线程
    数据的交换：postMessage、onmessage
### websocket
    为web应用程序和服务端之间提供全双工通信机制
### webStorage
    分为localstorage、sessionstorage
## webStorage
    sessionStorage:每个页面会话期间存储,页面刷新不会消除，window.open,location.href都可以获取sessionStorage
    localStorage:浏览器关闭后仍会存储
    接口：
    Window.sessionStorage、Window.localStorage
    方法：
    setItem,getItem,removeItem,clear,key
    与cookie的不同:
    1.webstorage有封装好的方法。cookie没有
    2.cookie的作用是和服务器交互，webstorage只是为了存储数据
## webSocket
    WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议
    var socket=new WebSocket(url,[protocol])
    只读属性：
    readyState:0,1,2,3
    bufferedAmount:在队列中没发出的文本字节数
    时间：
    onopen、onmessage、onerror、onclose
    方法:
    send(),close()
## webWorker
    javascript采用的是单线程模型
    webWorker就是为了javascript创造多线程环境，将一些任务分配给后者运行。
    限制：
    1.同源限制
    2.DOM限制，只能使用naigator,location
    3.通信联系
    4.worker不能执行alert(),confirm()
    var worker=new Worker('.js')
    方法
    postMessage，terminate
    事件
    onmessage
##  doctype
    <!doctype>声明必须处于头部，不是一个html标签
    html5  <!doctype html>
## 自定义属性
    data-* 为html5新加的自定义属性
    js中可以使用dom.dataset.*来获取属性值
## 从url到渲染页面
    1.判断是否有缓存
    2.通过DNS将URL解析出服务器的主机名，并将主机名转为IP地址
    3.从url中解析出端口号
    4.建立TCP连接
    5.发送HTTP请求，并等待服务器响应
    6.服务器返回200，浏览器接受并且可能关掉tcp
    7.解码响应，可以缓存则存入缓存
    8.显示HTML页面
    9.发送请求获取嵌入在HTML中的资源
    10.发送异步请求
## 浏览器渲染页面
    1.根据html构件DOM树、CSSOM树，构建期间优先加载JS文件。
    2.构建渲染树
    3.页面的重绘和重排（回流）
    重绘：渲染树节点发生改变，但不影响空间位置和大小，如宽高
    重排：渲染树节点发生改变，影响了节点的几何属性，导致节点位置发生变化。
    重排必定引起重绘
    重排影响手机浏览器的渲染速度
# 事件流
    捕获阶段 目标阶段 冒泡阶段
# webpack
# 事件循环Event loop
## 单线程
    1.js是单线程的
    2.ajax实现的异步任务是在浏览器处理网络的模块中执行
## 事件循环机制
    1.主要部分：stack heap queue
    2.宏任务、微任务
        微任务执行完，才会执行宏任务
        微任务：process.nextTick promise.then catch finally
## 参考资料
    https://www.cnblogs.com/formercoding/p/12906640.html