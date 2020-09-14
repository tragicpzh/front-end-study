# Redux
## 简介
    JS状态容器，可以适用于任意框架
    单一的store和根级别的reducer
## 用途
    用于管理不同组件共用的状态
## 核心概念
    1.state不能直接修改
    2.通过action来描述发生的事件，action为简单的对象（{type: text:}）
    3.使用reducer来联系state和action,对应每个action返回新的state
## action
    1.可以用单独的模块来存储action type
    2.在action使用index来表示引用的数据
    3.使用action创建函数来创建action
    4.创建action后立即dispatch的方法：
        dispatch(addTodo(text))
        boundeAddTodo=text=>dispatch(addTodo(text));
## reducer
    1.设计state结构，减少数据间相互的引用
    2.action处理：
        1.使用默认值 todoAPP(state=initialState,action)
        2.判断action 可以使用switch语法(default返回旧state)
        3.combineReducers({A:reducerA,B:reducerB,...})用来合并每个子reducer
        4.state={A:,B:,...}
## Store
    方法：
    getState()获取state
    dispatch(action)更新state
    subscribe(listener)注册监听器
    subscribe(listener)返回值为注销监听器函数
    createStore(reducer,initialState)创建store
## react-redux
    展示组件 表现样式，骨架
    容器组件 描述运行 数据获取 状态更新
    实现容器组件：
        Provider+connect
        Provider作为最外层组件传递state
        connect(mapStateToProps,
                mapDispatchToProps,
                mergeProps,
                options)(Comp)
         mapStateToProps(state,ownProps)返回值为对象，对象中是传递给展示组件的props(与state相关)，state为store中的数据，ownProps为传递给容器组件的props
         mapDispatchToProps(dispatch,ownProps)返回值为对象，对象中是传递给展示组件的props(与action相关),dispatch为redux的dispatch方法，ownProps为传递给容器组件的props
         mergeProps 如何合并stateProps dispatchProps ownProps
         option 选项
         
        