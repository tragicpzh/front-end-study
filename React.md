# 搭建

## react 脚手架 CRA

    npm i -g create-react-app

## 创建项目

    npm create-react-app xx

## 启动项目

    npm start

# 目录

## 结构

    public:公共资源，只能在public/index.html中使用
    src:Webpack只处理src中的文件，需要将相关的js、css文件放入

# 辅助开发工具

    Storybook Styleguidist
    用于查看UI组件的不同状态

# react 全家桶

状态管理：redux
路由：react router
异步操作:redux-observable redux-saga
前后台交互：axios
UI 组件库：antd

# antd

    npm install antd
    import {UI组件} from 'antd'
    import 'antd/dist/antd.css'
    参考文档：https://ant.design/components/overview-cn/

# axios

## 安装

    npm install axios

## 原理

    基于Promise的HTTP库

## 引入

    import axios from 'axios';

## 参考文档

    http://www.axios-js.com/zh-cn/docs/

# react router

## 作用

    保持UI和URL的同步

## 安装

    npm install react-router-dom

## 参考文档

    官方文档：http://react-guide.github.io/react-router-cn/docs/API.html
    掘金文章：https://juejin.im/post/6844904157833347079

# redux 与 react-redux

## 安装

    npm install --save redux

## 参考文档

    https://www.redux.org.cn/
    https://www.cnblogs.com/bax-life/p/8440326.html

# react 组件

## 函数组件与 class 组件

    function func(props){}
    class xx extends xx{}

## 渲染组件

    组件接收的props包括接受的属性和子组件（children）的单个对象
    组件名称必须开头大写

## 组件的可读性

    组件的props不能被更改

## state（状态）

### 作用

        组件的私有属性

### 赋初值

        在class构造函数中赋予
        constructor(props){
            super(props);  //赋予构造函数this，且this中包含props
            this.state={

            }
        }

### 组件内使用

        this.state.xxx

### 修改 State

        使用setState而不是直接修改State
        this.setState(state:{});

### 更新异步

        error: counter:this.state.counter+this.props.increment
        true:(state,props)=>{
            counter:state.counter+props.increment
        }

## 生命周期

### 三个状态

        Mounting Updating Unmounting

### 方法

        https://www.jianshu.com/p/b331d0e4b398

## 受控和非受控

    受控：state初始值受父组件props控制
    非受控：反之

## 事件处理函数

### 使用

    与传统的htnl不同
    <button onClick={handleClick}></button>

### 绑定 this

    当事件处理函数需要使用this时(如：this.state)，需要在constructor中绑定this
    this.handleClick=this.handleClick.bind(this);

### 传递参数

    <button onClick={(e)=>this.deleteRow(id,e)}>
    <button onClick{this.deleteRow.bind(this,id)}>

## 条件渲染

### 传统的 if 语句

    1.根据条件返回不同的JSX
    2.根据条件保存不同的元素，在JSX中使用

### 与运算符&&

    在JSX中可以这样写
    { xxxxx &&
        <h2>
            Hello
        </h2>
    }
    当xxxx为true时，返回对应JSX，否则返回false

### 三目运算符

    { xxxxx
        ?<button>
        :<input>
    }
    与xxxx?:e1:e2同样的意思

## 阻止渲染

    render 返回null

## 列表和 Key

### 渲染多个组件

    使用{}在JSX中构建一个元素集合
    <ul>{listItems}<ul>
    listItems是一个标签数组

### 传递参数

    <NumberList numbers={numbers}>

### Key

    帮助React识别哪些元素改变了，一般为id或者index

## 表单

### 实现方法

    受控组件

### 受控组件

    组件只能通过setState来更新，state是组件的唯一数据源

## 组件的生命周期

### 挂载

    constructor()
    getDerviedStateFromProps(nextprops,prestate) //props变化带动state变化
    render()
    componentDidMount()

### 更新

    getDerviedStateFromProps()
    shouldComponentUpdate(nextprops,prestate)
    render()
    getSnapshotBeforeUpdate(preprops,prestate) //在渲染输出到DOM之前调用，返回值会传给componentDidUpdate()
    componentDidUpdate()

### 卸载

    componentWillUnmount()

### 其他 API

    setState:更新state与组件，会与其他setState合并为一次更新
    forceUpdate:强制让组件重新渲染，会跳过shouldComponentUpdate()

# react Ref

    1.回调函数，入参为组件实例或dom节点
        <xxx ref={(node)=>{}}>
    2.createRef,forwardRef(转发ref)
        ref=react.createRef();
        <Son ref={ref}>
        const Son=forwardRef((props,ref)=>{
            return <Grandson xxx={ref}>
        })
    3.函数式组件:useRef.forwardRef
    4.useuseImperativeHandle(ref,handle,[deps])
        用于暴露特定的值和方法给ref
