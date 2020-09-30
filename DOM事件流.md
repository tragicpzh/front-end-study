# 事件的阶段

## 捕获阶段

事件从顶层元素一直传递到目标元素的父元素

## 目标阶段

事件到达目标元素

## 冒泡阶段

事件从目标元素父元素向上逐级传递到最顶层元素

# 事件的监听

```javascript
EventTarget.addEventListener(type,handle,useCapture)
type:监听事件类型
listener:回调函数
useCapture:默认为false，false:事件仅在冒泡时触发,true:事件在捕获和冒泡时触发
```

当触发目标元素上的事件时，是无视 useCapture,因为处于目标阶段。

# 事件的优先级

element.onClick>addEventListener
标签中的 on 函数会被 JS 中的 on 函数覆盖（如：onClick）

# 事件的委托（事件代理）

将同一类型元素的事件，委托给一个父元素

## 原理

利用 DOM 事件流来实现，通过 handle 的参数来对特定元素执行事件。

## 例子

为 ul 内的所有 li 元素添加事件。

```Javascript
 <ul id="ul">
    <li/>
    <li/>
  </ul>

  <script>
    var ul=document.getElementById("ul");
    ul.addEventListener('click',function(e){
      var event=event||window.event;
      var node=event.target||event.srcElement;
      if(node.nodeName.toLowerCase()=='li'){
        /* 事件内容 */
      }
    })
  <script/>
```

## 优点

减少不必要的重复的事件添加，减少内存消耗。
能够监听到新添加的元素触发的事件。

## JQuery 实现

```javascript
  $(selector1).on(selector2,type,handle)
  type:触发的事件类型
  selector1:事件委托的父元素
  selector2:事件委托的目标元素
  handle：回调函数
```
