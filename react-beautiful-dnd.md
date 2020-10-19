# 简介

拖放列表组件

# 主要结构

<DragDropContext>拖放功能的应用程序部分
<Droppable> 可以放入拖放项目的区域
<Draggable> 可以拖放的项目

# `<DragDropContext>`

onBeforeCapture

    用途：添加drop drap/修改元素大小(决定了虚拟拖动模型的大小)
    参数：before:{draggableId,mode}

onBeforeDragStart

    用途：修改元素以锁定其大小(不能添加或删除元素,不能改变元素大小)
    参数：start:{draggableId,type,source:{droppableId,index},mode}

onDragStart

    用途：用来阻止拖动期间的组件更新
    参数：start,provided:{announce:(msg)=>void}

onDragUpdate

    触发条件：Draggable位置变化/Draggable移动到不同的Droppable/Draggable不在Droppable上
    注意：过多的操作会导致拖动慢
    参数:update:{...start,destination:{droppableId,index},combine:{draggableId,droppableId}},provided

onDragEnd (不可缺少)

    用途：拖动结束，修改对应项目的排序
    参数：result:{...update,reason},provided

# `<Droppable>`

    Props:
      droppableId
      type:string | 'DEFAULT' （drop与drag的对应关系）
      mode:'horizontal'|'vertical'
      isDropDisabled
      isCombineEnable
      direction:'horizontal'|'vertical'
      ignoreContainerClipping:是否允许拖动至滚动区域隐藏部分
      renderClone
      getContainerForClone
      children:(
        DroppableProvided,
        DroppableStateSnapshot
        )=>Node
    DroppableProvided:{
      innerRef,
      droppableProps:{
        'data-rbd-droppable-context-id',
        'data-rbd-droppable-id'
      },
      placeholder
    }
    DroppableStateSnapshot:{
      isDraggingOver
      draggingOverWith
      draggingFromThisWith
      isUsingPlaceholder
    }

# `<Draggable>`

    props:
      draggabledId,
      index:匹配排序顺序(不重复且递增),
      isDragDisabled,
      disableInteractiveElementBlocking(设置交互式元素是否可以被拖动，交互可能失效),
      shouldRespectForcePress,
      children:(
        DraggableProvided,
        DraggableStateSnapshot,
        DraggableRubric
        )=>Node
    DraggableProvided:{
      innerRef,
      draggableProps:{
          style,
          onTransitionEnd,
          'data-rbd-draggable-context-id',
          'data-rbd-draggable-id'
      }
      dragHandleProps:用于控制拖动的句柄参数
    }
    DraggableStateSnapshot:{
      isDragging,
      isDropAnimating,
      dropAnimation,
      draggingOver,
      combineWith,
      combineTargetFor,
      mode
    }
    DraggableRubric = {
      draggableId
      type
      source
    };
