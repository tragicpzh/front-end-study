# react 中使用 echarts

```javascript
    1.npm echarts-for-react
    2.npm echarts
    3.import ReactCharts from 'echarts-for-react'
    4.import echarts from 'echarts/lib/echarts'
    5.import 'echarts/lib/chart/xxx'-按需加载图表
    6.<ReactCharts {props}/>
    7.props:{
      option:echarts配置
      notMerge?:setOption时不合并data
      lazyUpdate?:setOption时懒加载data
      style?:<div {style}>
      className?:<div {className}>
      theme?:echart的theme('dark'|'light'),其他需要echarts.registerTheme(theme,style)
      onChartReady?:echarts加载完毕的回调函数->(echarts)=>{}
      loadingOption?:loading option
      showLoading?:echarts渲染时，展示loading遮罩
      onEvents?:echarts事件:{
        'click':this.onClick()->(echarst)=>{}
        'legendselectchanged':this.legendchange()->(echarst)=>{}
        ...
      }
      opts?:echarts.Instance.opts(echarts初始化的选项)
    }
    8.API:{
      getEchartsInstance:获得echart实例对象
    }
      使用:
        <ReactCharts option={} ref={(e)=>{this.echartRef=e}}>
        let instance=echartRef.getEchartInstance();
```

# option(component)

    series:一组数据以及他们映射成的图{
      type:图
      data:一组数据
      itemStyle:通用样式{
        shadowBlur:阴影大小
        shadowOffsetX:X偏移
        shadowOffsetY:Y偏移
        shadowColor:阴影颜色
        emphasis:hover样式
      }
      seriesLayoutBy:dataset的行列映射，默认为column
      dimensions:指定了维度的顺序，默认第一个维度->X,第二个维度->Y(比dataset优先)
      encode:x y 的对应
      ...:其余参数
    }
    dataset:{
      dimensions:指定了维度的顺序，默认第一个维度->X,第二个维度->Y
      source:等同于series.data的映射
      sourceHeader:表明source第一行是否是维度打野
    }
    坐标系：{
      xAxis:x轴
      yAxis:y轴
      grid:坐标系底板
    }
    data(series.data):number|string|obejct:{
      name:名字
      value:数值
    }
    visualMap：视觉映射{
      type:'continuous'|'piecewise'(连续|分段)
      show:视觉映射组件
      min:最小值
      max:最大值
      inRange:选中范围的视觉配置
      outRange:选中范围外的视觉配置
    }
    color:[...color]调色盘
    dataZoom:对数轴(axis)进行缩放、平移操作{
      type:slider|inside|select(滑动条|内置|选框)
      start/end:百分比范围
      startValue/endValue:数值范围
      xAxisIndex/yAxisIndex:对应的数轴index(默认为xAxisIndex:0)
    }(一个数轴可存在多个dataZoom)
    grahic:图形元素(可拖拽...)

# 定位

    绝大多数组件和系列，基于left/right/top/bottom/height/width来绝对定位。
    每个值可以是：{
      数值
      基于宽高的百分比
    }
    少数组件和系列使用中心半径定位，基于center/radius定位

# 异步数据加载和更新

    1.instance.setOption(option)
    2.react中将option与props|state绑定
    3.loading动画 instance(echarts).hideLodaing()/showLoading();

# echarts event

    echarts.on(type,handle)|(type,query[触发回调的组件类型],handle)
    type:{
      鼠标:'click'|'dbclick'|'mousedown'|'mousemove'|'mouseup'|mouseover'|'mouseover'|'globalout'|'contextmenu'
      组件交互:'legendselectchanged'|...
    }
    handle:(params)=>{}
    params:{
      componetType:组件名称(series|markline|...)
      seriesType:series类型
      seriesIndex
      seriesName
      name:数据名|类目名
      dataIndex:data在数组中的index
      data:data对象
      dataType:data类型(node|edge)
      value:数据值
      color"数据图形颜色
    }
    query:string|object:{
      <mainType>Index
      <mainType>Name
      <mainType>Id
      dataIndex
      name
      dataType
      element
      <mainType>:series|...
    }

# echarts action

    echarts.dispatchAction({
      type:动作类型(highlight|downplay|...)
    })
