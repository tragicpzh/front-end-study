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

## 原理

```javascript
<TriggerContext.Provider value={{ onPopupMouseDown: this.onPopupMouseDown }}>
  {trigger}//触发元素(如下拉输入框)
  {portal}//弹出层(如下拉框)
</TriggerContext.Provider>
```

    trigger为传入的children,附加一些props
      props:
        1.强化回调事件:在原有的回调加入trigger组件本身的回调函数
        2.强化class:children+trrigger
        3.尝试传入children+trigger的ref
    portal:react.createPortal创建，默认创建于body下
      trigger.props.popup来渲染弹出层内容
      Popup组件来渲染弹出层
    Popup:由Mask PopupInner两个组件组成
      Mask:附加css动画特效的遮罩层(rc-motion),默认没有mask
      PopupInner:弹出层内容+CSS动画+用于对齐的组件

# rc-cascader

## 作用

    实现弹出层的级联效果

## 关键的 props

    fieldNames:options字段映射
    popupPlacement:弹出层位置
    dropdownMenuColumnStyle:下拉框每一列的样式
    changeOnSelect:是否在选择过程中提交选择内容
    options:级联项
    value:选中项（数组类型，每一级选中的级联项）
    dropdownRender:下拉菜单自定义渲染函数，参数为menu(根据value处理后的options)

## 基本组件

    trigger

## 核心结构

    children:触发级联弹出框的元素
    popupNode:弹出层的内容

## children

    附加了两个props:
      handleKeyDown:实现级联框的键盘操作，
      tabIndex:级联标签Index

## popupNode

    <Menus>或dropdownRender(<Menus>)

## <Menus>

    实现级联效果的菜单组件

### 关键的 props

    filedNames:{value,label,children}的映射字段
    defaultfiledNames:默认映射
    activeValue:被选中的级联项 对应option元素的value字段。数组类型，从1级开始的该级联项的每个value值。
    onSelect:选中级联项的回调
    onItemDoubleClick:双击级联项的回调
    visible:弹出层内容的显示/隐藏

# Upload

## 核心

```javascript
    xhr+FormData+promise
    上传触发：<input type="file">
```
