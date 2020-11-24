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

# react 深度剖析

## state

    state的更新：
        合并多次多个处于batchUpdate的state,然后一次性更新
    useState:
        为每个组件创建一个_state和index，使用一个state数组来存储一个函数式组件创建的所有state，并将_state和index放在虚拟节点对象上(Fiber,避免命名冲突)
    state与useState的差别:
        1.类组件中使用this.state来读取state，能够保证读到的是最新的state引用（解决方法:创造闭包环境）
        2.函数式组件使用useState产生的state，会受闭包环境影响，导致不能拿到最新的state引用（解决方法:useRef）
        3.useState默认使用浅比较：只比较第一层的数据(基本数据类型比较值，复杂类型比较引用,解决方法:useReducer实现深比较)
        4.setState可以保存函数(记录函数的引用)，useState不能保存函数(传入的函数会被立刻执行(类似于setState(function),用于获得最新的state),解决方法:使用useCallback作为替代)
    batchUpdate:
        能命中batchUpdate的函数:{
            生命周期函数
            react注册的事件
            可以管理的入口(render)
        }
        不能命中的函数{
            setTimeout setInterval等宏任务
            自定义dom事件
            管不到的入口
        }
        在命中batchupdate的函数中:
            setState会被合并(异步)，useState同理
        不能命中的函数中:
            setState会被立即执行(同步)
    Hook对象:{
        baseState
        next(记录下一次useState对应的hook对象，类似于链表的下一个节点)
        baseUpdate
        queue
        memoizedState(记录useState返回的结果)
    }

## Fiber

    解决react同步更新导致的性能问题(函数调用栈过深->同步任务执行过久->不能执行其他任务->界面卡顿)

### 算法

    分片，将一个耗时的算法分为小片，每个小片运行时间很短，使得在其中可以插入其他任务。(更新过程碎片化)

### 影响

    componentWillMount和componentWillUpdate这两个函数有可能会被调用多次。
    因为生命周期函数有可能会被优先级更高的任务打断，而造成多次执行。

### FiberNode

    fiber:单链表的属性结构
    FiberRoot:链表根节点
    current:FiberNode,fiber节点的根
    fiber:{
        stateNode:节点实例
        child:下一个fiber节点
        sibling:兄弟fiber节点
        return：父节点
    }

## Hook

    在不编写class的情况下使用state以及其他的react特性

### 现有的 hook

    useState
        1.等价于类组件的state
        2.setState可以传入函数，参数为最新的3.3。state,返回值为更新的state
        4.setState不会合并更新对象
        5.initialState只在`组件初始渲染`中起作用，可以是函数
    useEffect:
        1.副作用操作->实现生命周期函数(多个effect实现关注点分离)
        2.在组件渲染到屏幕之后执行
        3.如果不添加依赖项，那么effect中的数据始终引用先前渲染中的旧数据
    useContent:
        1.接收一个context对象并返回context的当前值，当context变化时触发重渲染
        2.context为react的上下文，创建上下文:createContext(initialContext)
    useReducer:
        1.useState的替代方案，返回[state,dispatch],参数为(reducer,initState,init)
        2.reducer:(state,action)=>newState
        3.适用场景：更新复杂的状态/依赖于上一次state/触发深更新做性能优化
    useCallback:
        1.返回一个memoized回调函数
        2.参数为(callback,deps)
        3.等价于useMemo(()=>callback,deps)
    useMemo:
        1.返回一个memoized值
        2.参数为(func,deps),func的返回值为memoized值
        3.作用：优化性能
    useRef:
        1.useRef(initialValue)返回一个可变的ref对象
        2.ref.current初始值为initialValue
        3.ref可以保存任何值，它在每次渲染时都会返回同一个对象(引用地址不会变化)
        4.当ref对象内容发生变化时，useRef不会通知你
        5.ref的更改不会引发重新渲染，不会被重新声明
    useImperativeHandle:
        1.参数为(ref,createHandle,[deps])
        2.用于自定义暴露给父组件的实例值，实例值为createHandle返回值
    useLayoutEffect:
        1.与useEffect相同
        2.在所有dom变更之后,渲染到屏幕之前同步调用effect

### Hook 使用规则

    在react函数的最顶层调用他们
    原因：hook节点是一个链表->每次渲染时，需要保证hook调用的顺序一致->不一致，会导致下一个hook节点与需要的节点不同，从而产生bug

### 自定义 hook

    1.以use开头的函数，函数内部可以调用hook。
    2.自定义hook是一种重用状态逻辑的机制，其中的所有state和副作用都是完全隔离的。
