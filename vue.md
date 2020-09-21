# Vue

## vue3.0 新特性

    1.代码结构
        将一些内部功能分解为单独的包，代码库改为使用Typescript编写
    2.监测机制
        使用proxy来监听数据，带来了初始化速度加倍的同时内存占用减半的效果。
    3.vue-cli 3.0
        改变了命令，增加了图形化界面以及管理vue项目的功能
    4.slot
        使用lazy函数，由子组件控制slot,精确依赖手机，避免不必要的组件渲染。
    5.option API到Compisition API
        Composition API根据逻辑功能来组织，一个功能所定义的所有API会放在一起，达到高内聚低耦合的效果。
        Composition API提供的函数：
        reactive(将对象变为响应式数据),watchEffect(检测状态的变化)，computed(计算属性),ref(将数值转为响应式数据),toRefs(将reative的值处理为ref，将reactive对象转为普通对象，但每个节点都是ref对象)，生命周期的hook(基本和option api一致)

## 生命周期函数

    beforeCreate ->setup() //组件刚被创建、组件属性计算之前
    created ->setup() //组件实例创建，属性已绑定，DOM未生成
    beforeMount -> onBeforeMount //模板编译、挂载之前
    mounted -> onMounted    //编译挂载
    beforeUpdate -> onBeforeUpdate//更新之前
    updated -> onUpdated    //更新
    beforeDestroy -> onBeforeUnmount    //销毁之前
    destroyed -> onUnmounted //销毁
    errorCaptured -> onErrorCaptured //错误捕获
    前者为2.x后者为3.x

## 双向绑定的原理

    使用proxy作为其观察者机制，取代之前的Object.defineProperty。通过对数据添加getter/setter方法，来监听数据的变化。

## 数据监听、响应式原理简析

    https://www.jianshu.com/p/2052403d991b

## watch、computed

    watch(数据源，回调函数,函数设置（lazy,deep...）)
    computed(计算函数)
    两者都会监听响应式数据。
    区别：
    1.功能：watch是监听，computed是计算
    2.使用场景：
        watch:1影响n
        computed:n影响1
    作用:computed中的属性只会在被使用时才会计算，这能够大大提升性能（计算属性是依靠依赖缓存来计算的，方法不能依靠依赖）

## Render 函数

### 定义

    编程式的渲染
    render(h,context){
        return Vnode类型
    }

### context

    context为渲染时的上下文
    context: props,children,slots,data,parent

### h

    Vnode通过h(html元素,html属性,子节点)创建
    html元素可以是标签名(String)，Object({template:``}),function()
    html属性只能是对象，包括class,style,on,scopedSlots
        scopedSlots:{
            name:props=>Vnode||Array<Vnode>
        }
    子节点可以是Vnode数组或者字符串
        this.$slots获取Vnode列表中的静态内容//子组件中的阵列
        this.$scopedSlots中获得能用作函数的作用域插槽

### 与其他渲染属性的优先级

    render>template>el
    el可以使用很多vue模板
    render需要用js代码来实现模板的效果（使用map）

### 相关链接

    https://www.cnblogs.com/tugenhua0707/p/7528621.html

## slot 插槽

### 不具名插槽

    <slot></slot>隐含的name属性default

### 具名插槽

    子组件：<slot name=""></slot>
    父组件  <template v-slot:(name)></template> 3.0中只能使用template来分发内容

### 作用域插槽

    作用：为父组件提供子组件的prop
    子组件 <slot v-bind:(name)="(prop)">name是插槽的名字，prop是绑定的参数
    父组件<template v-slot:(name)="(newprop)">name是插槽的名字，newprop是绑定参数的新命名
    prop可以是任何能够作为函数参数的js表达式

### 子组件的默认值

    <slot>默认内容</slot>

### 缩写

    v-slot -> #

### 插槽的作用

    插槽可作为可复用的模板，这些模板可以根据输入的prop渲染出不同的内容

## 父组件与子组件

    父组件向子组件传递：prop
    子组件向父组件传递: emit事件

## 虚拟 DOM

### 原理

    1.建立虚拟dom树并生成真实dom树
    2.建立修改后的虚拟dom树
    3.新旧虚拟dom树进行diff比较，将差异保存补丁集合中去
    4.根据补丁来更新真实dom树

### diff 算法

    https://www.cnblogs.com/wind-lanyan/p/9061684.html

### 相关链接

    https://www.jianshu.com/p/af0b398602bc

## vuex

### 作用

    Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

### 基本状态

    state,getters,mutations,actions
    state:需要的属性
    getters:将定义的数组输出
    mutations:对后台传来的数据做处理，并赋值给state里的数组
    actions:与后台交互并获取数据传给mutations

## 模板语法

### v-if 和 v-show

    v-if：生成或溢出
    v-show：显示或隐藏

## 父组件和子组件之间的生命周期执行顺序

    加载渲染：
    父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted
    子组件更新： 是先父后子
    销毁过程：先父后子

## element-ui

## vue 相关组件库

    https://www.cnblogs.com/zdz8207/p/vue-ui-framework.html
