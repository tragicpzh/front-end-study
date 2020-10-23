# Checkbox

## 底层组件

rc-checkbox:

```
  <span>
    <input/>
    <span>
    </span>
  </span>
```

## Checkbox.Group

    options:
      指定可选项，并对选择项进行排序，同时会过滤不在可选项中的checkbox，甚至可以通过该属性添加新的checkbox，options的原理为创建对应的checkbox而不是隐藏不符合的checkbox
    values:
      指定选中项，如果存在不合法的项(没有对应的checkbox、不在options当中)会被自动过滤

# trigger

## 参数

```javascript
    action?:控制弹出层显示/隐藏的动作(click 等等)
    showAction?:控制弹出层显示的动作
    hideAction?:控制弹出层隐藏的动作
    getPopupClassNameFromAlign?:计算弹出层对齐的样式
    onPopupVisibleChange?:弹出层显示/隐藏的回调函数
    afterPopupVisibleChange?:potral 创建时的回调函数(potral 用于创建弹出层，使用了 react.createPotral)
    popup:弹出层的渲染
    popupStyle?:弹出层的内联样式
    prefixCls?:通用样式的前缀(如 ant)
    popupClassName?:弹出层的 class
    className?:弹出层内容的 class
    popupPlacement?:弹出层的位置
    builtinPlacements?:控制弹出层位置的配置信息(如 xy 偏移量)
    mouseEnterDelay?:onMouseEnter事件的延迟
    mouseLeaveDelay?:onMouseLeave事件的延迟
    zIndex?:弹出层的zIndex
    focusDelay?:onFocus的延迟
    blurDelay?:onBlur的延迟
    getPopupContainer?:弹出层的父节点
    getDocument?:获得当前文档对象
    forceRender?:是否强制渲染弹出层
    destroyPopupOnHide?:隐藏时是否破坏弹出层内容
    mask?:是否启用遮罩层
    maskClosable?:是否支持点击关闭遮罩层
    onPopupAlign?:弹出层对齐时的回调
    popupAlign?:弹出层对齐相关信息
    popupVisible?:弹出层的显示/隐藏
    defaultPopupVisible?:弹出层的默认显示/隐藏
    autoDestroy?:弹出层隐藏后是否销毁
    stretch?:某个宽高属性的拉伸
    alignPoint?:是否对齐
    popupMotion?:弹出层动画
    maskMotion?:遮罩层动画

```
