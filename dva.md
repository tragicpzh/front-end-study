# effect API

## call

- 并行执行：

```javascript
  yield all([call(),call()])
```

- 竞争执行:

```javascript
  yield race({action1:call(),action2:call()})
  if(action1)xxx
  else yyy
```

## put

不阻塞，一般用于触发 reducer(因为 reducer 是立即执行的)

## put.resolve

阻塞，可用于触发 effect

## select

不阻塞，用于从 state 中获取数据。

## take

阻塞，用于监听 action 的开始和结束阶段，直到监听到事件触发才会进行下一步

```javascript
  yield take(`${action}//@@start`)
  yield take(`${action}//@@end`)
  yield take([action1,action2]),满足一个就触发
```

## takeLatest

不阻塞,使用 takeLatest 来启动一个新的 action，并取消了所有之前启动且未完成的任务。

```javascript
action: [function* ({}, {}) {}, { type: "takeLatest" }];
```

## throttle

不阻塞，派生一次任务之后，仍然将新传入的 action 接受到底层的 buffer 中，但是在 ms 后将暂停派生新的任务。

```javascript
action: [function* ({}, {}) {}, { type: "throttle", ms: xx }];
```

## watcher

监听事件，不过只能执行一次

```javascript
action: [function* ({}, {}) {}, { type: "watcher" }];
```

## poll

轮询

```javascript
  action:[
    function*({},{}){

    },
    {type:'poll',delay:xx}
  ]

  dispatch({type:`${namespace}/${action}-${start or end}`},payload);
  /*
  start:轮询开始
  end:轮询结束
  */
```
