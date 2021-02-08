# 简介

    RxJs是使用overvables的响应式编程的库，它使编写异步或基于回调的代码更容易。
    它提供核心类型Oberservable,附属类型Observer,Schedulers,Subjects,操作符map,filter,reduce等

# 基本概念

- Observable:可观察者对象，一个可调用的未来(值或事件)的集合
- Observer:观察者，监听 Observable 的回调函数集合
- Subscription:订阅，主要用于 Observable 的执行取消
- Operators:操作符，函数式编程风格的纯函数(仅依赖于参数，且无副作用),用于处理集合
- Subject:主题,EventEmitter(事件触发与监听),将(值|事件)多路推送给多个 Observer 的唯一方式
- Schedulers:调度器，控制并发且中央集权的调度员，允许我们在发生计算时进行协调。

# Observables

- 创建

```javascript
    observable=Rx.Oberservable.create(function(observer{next,error,complete}))
```

- 订阅

```javascript
    observable.subscribe(function|{next,error,complete})
```

- 执行
  observable 被创建后，只有当创建了对应的订阅后才会执行。会以同步或异步的方式产生多个值(与 function 的不同,function 仅同步地返回一个值)。
- 清理

```javascript
    observable=Rx.Oberservable.create(function(observer{next,error,complete})=>{
      return function unsubscribe(){
        //清理操作，一般为清理类似于timeout的定时器
      }
    })
    const subscription=observable.subscribe();
    subscription.unsubscribe();//该函数执行清理操作
```

# Observer 观察者

- 构造
  observer:{
  next:function,
  error:function,
  complete:function,
  }
- 生效
  observable.subscribe(oberserver|(next,error,complete))
- 调用
  Rx.Observable.create(function(observer){
  observer.next();
  observer.error();
  observer.complete();
  })

# Subscription

- 执行 observable
  const subscription=observable.subscribe();
- 清理 observable
  subscription.unscribe();
- 子 subscription
  添加：subscription.add(childSubscription)
  移除：subscription.remove(childSubscription)
  一同清理 observable：subscription

# Subject

- 概念
  特殊的 observable,允许将值多播给观察者
- 地位
  既是 observable,又是 observer
  observable:

```javascript
const subject = new Rx.subject();
subject.subscribe(observer1);
subject.subscribe(observer2);
```

    observer:

```javascript
    observable.subscribe(function(observer)|subject);
    subject.next|error|complete;
```

# Scheduler

- 调用
  Rx.Observable.create(funciton(observer)).observeOn(scheduler)
- 原理
  将 observer 使用 scheduler 重新创建
- 类型
  null:同步方式
  queue:当前事件帧的队列调度
  asap:微任务的队列调度
  async:使用 setInterval 的调度
- 使用调度器
  1.observeOn 2.静态创建操作符可以接受调度器 3.最小并发原则：没有提供调度器，则使用该原则
  有限、少量：null
  大量、无限：queue,
  含有定时器: async

# 常用的操作符

详见文档[RxJs 中文文档](https://cn.rx.js.org/manual/overview.html#h213)

# RxJs vs Promise

| 比较点       | RxJs       | Promise  |
| ------------ | ---------- | -------- |
| 返回值       | 多值       | 单值     |
| 订阅         | 可多次订阅 | 单个订阅 |
| 惰性运算     | 是         | 否       |
| 是否允许终止 | 是         | 否       |
| 异步         | 可能是     | 永远是   |

# RxJs 的应用场景

- 异步、同步逻辑复杂(websocket 等实时性要求)
- 时序控制要求高，页面逻辑复杂
- Promise 难以解决问题
- 持续事件(拖拽、动态加载页面、虚拟列表等)

# RxJs 应用于 React

    RxJs结合react-hook，实现局部应用场景的RxJs使用
    npm install rxjs-hooks

## rxjs-hooks

    useObservable,useEventCallback

### useObservable

```javascript
const state = useObservable(
  (inputFactory: (state$, input$) => observable),
  initialState,
  (inputs: any[])
);
```

| 变量         | 意义                                                                  |
| ------------ | --------------------------------------------------------------------- |
| state        | 产出的变量，不能被外部直接改变                                        |
| inputFactory | observable,使用 state$与inputs$产生异步流程，监听到的值作为新的 state |
| state$       | BehaviorSubjec,inputFactory 监听到的值会作为 state$新的上下文         |
| inputs$      | BehaviorSubject，外部传入新的 inputs 会作为 inputs$新的上下文         |
| initialState | state$初始值                                                          |
| inputs       | inputs$值                                                             |

### useEventCallback

```javascript
const [returnCallback, state] = useEventCallback(
  (callback: (event$, state$, inputs$) => observable),
  initialState,
  inputs
);
```

| 变量           | 意义                                                                           |
| -------------- | ------------------------------------------------------------------------------ |
| returnCallback | 控制 event$产出的值                                                            |
| state          | 产出的变量，不能被外部直接改变                                                 |
| callback       | observable,使用 event$、state$与 inputs$产生异步流程，监听到的值作为新的 state |
| state$         | BehaviorSubjec,inputFactory 监听到的值会作为 state$新的上下文                  |
| inputs$        | BehaviorSubject，外部传入新的 inputs 会作为 inputs$新的上下文                  |
| initialState   | state$初始值                                                                   |
| inputs         | inputs$值                                                                      |

## 两者的差别

    useObeservable产出变量完全由初始定义的异步流程与input影响，适合自适应数据。
    useEventCallback产出变量同上，但是受returnCallback影响，适合受控数据。
