# 选择器
## 选择符
    1.id选择器（ # myid）
    2.类选择器（.myclassname）
    3.标签选择器（div, h1, p）
    4.相邻选择器（h1 + p）
    5.子选择器（ul > li），只有是父子关系才能生效
    6.后代选择器（li a），不仅限于父子关系，爷孙也可以
    7.通配符选择器（ * ）
    8.属性选择器（a[rel = "external"]）
    9.伪类选择器（a: hover, li:nth-child）
## 选择符的优先级
    ！important>行内>内嵌>链入
## 伪类选择器
    a标签：
        a:link a:visited a:hover a:active 必须按顺序写
## 选择器权重
    1.内联样式，1000
    2.ID选择器：0100
    3.类、伪类、属性：0010
    4.元素选择器、伪元素选择器（标签选择器）：0001
    5.通配符、子选择器、相邻选择器：0000
    6.！importan的作用提升优先级，为最高
# 引入CSS的四种方式
    1.行内式<div style="">
    2.内嵌式
        <head>
            <style>
            </style>
        </head>
    3.链入外部
        <link type="text/css" rel="stylesheet" href="url">
    4.导入外部
        <style>
            @import url(.css)
        </style>
        link与import的区别
        import只能引用样式文件，link在页面加载时加载，impor在页面加载完成后加载
# 盒子模型
    从外到里：margin border padding content
# css布局
## flex布局
    1.flex模式 display:flex
    2.子级元素的排列方式 flex-direction: colum colum-reverse row(默认) row-reverse
    3.子级元素一行排列不下时，是否换行 flex:wrap nowrap(默认) wrap-reverse(换行，第一行在最下面)
    4.排列方式、是否换行 flex-flow:row nowrap
    5.项目在主轴上的对齐方式 justify-content: center flex-start flex-end space-between space-around
    6.项目在侧轴的对齐方式 align-item: center flex-start flex-end center stretch baseline
    7.多行项目的对齐方式 align-content: space-between flex-start flex-end center stretch space-between
    8.图解：https://www.cnblogs.com/dreamcc/p/10634218.html
## flex-shrink
    主轴溢出部分的分配因子（默认为1），当为0时代表元素不会缩小。
## flex-grow
    主轴剩余部分的扩张因子（默认为0），当为0时代表元素不会扩张
## grid布局
### 父元素
    1.grid模式 display:grid
    2.colum track:grid-template-colums
    3.row track:grid-template-rows
    4.网格区域命名 grid-template-areas: 
    5.gap grid-row-gap grid-column-gap
    6.项目在每个网格中的对齐方式 justify-items align-items
    7.多余内容的处理规则 justify-content align-content
### 子元素
    1.摆位置 grid-row:x/y grid-column:x/y grid-area: x
    2.找对齐 align-self justify-self place-self
### 隐式网格
    1.grid-auto-rows grid-auto-columns
    2.grid-auto-flow: column/row
### 取值
    1.大小 fr:容器剩余空间的百分比
           min-content
           max-content
           min/max都是相对于元素自身内容的大小
    2.函数 minmax(x,y)设置自适应网格的最大最小
           fit-content(x)
           repeat(num,size)
### 参考资料
    https://www.cnblogs.com/scq000/p/11206692.html
## 响应式布局
### 设计核心
    Media Queries，他根据条件告诉浏览器如何为指定视图宽度渲染页面。
## 瀑布流
### 简介
    瀑布流，又称瀑布流式布局。是比较流行的一种网站页面布局，视觉表现为参差不齐的多栏布局，随着页面滚动条向下滚动，这种布局还会不断加载数据块并附加至当前尾部。最早采用此布局的网站是Pinterest，逐渐在国内流行开来。国内大多数清新站基本为这类风格。
### 实现方法
#### flex+js
    1.外层使用row方向的flex
    2.子项目使用column方向的flex
    3.插入单个项目，向最短列插入
    4.使用js选择对应列插入批量项目（背包问题）
#### 多列布局
    1.外层使用样式column-count column-gap column-gap
    2.不能动态插入
#### 绝对定位
    1.外层为relative
    2.子元素为absolute
    3.计算固定宽度，子元素的left=索引*宽度
    4.从第二行开始，将图片放到最短的一列下面，然后增加此列高度
## 圣杯布局
### 简介
    两侧宽度固定，中间宽度自适应
### 实现方法
    1.flex
    2.float
    3.position
# position
## 分类
    absolute relative flexed static sitcky
## static
    不脱离文档流 遵循基本定位
## relative
    参考static位置top bottom left right进行调整，原有的位置依旧占有
## abosolute 
    脱离文档流，通过top bottom left right调整，选择最近一个有定位设置的父级元素（static relative）来绝对定位
## flexd
    脱离文档流，参考窗口位置
## sticky
    在屏幕范围内不受影响 在将要离开时,定位会变为flexd
## 参考资料
    https://www.cnblogs.com/ning123/p/11050487.html
# 透明度
    opacity:x x为透明度0-1：对所有内容有效
    background:rgba(x,y,c,z) z为透明度0-1 ：对对应内容有效（background）
# css预处理
## 作用
    CSS预处理器是一种专门的编程语言，用来为CSS增加一些编程特性（CSS本身不是编程语言）。不需要考虑浏览器兼容问题，因为CSS预处理器最终编译和输出的仍是标准的CSS样式。可以在CSS预处理器中：使用变量、简单逻辑判断、函数等基本编程技巧。
## less
    https://www.cnblogs.com/V587Chinese/p/11419587.html
## sass
    http://www.ruanyifeng.com/blog/2012/06/sass.html
    https://www.sass.hk/
# 高度塌陷
     父元素高度自适应，子元素 float 后，造成父元素高度为0，称为高度塌陷问题。
## 解决办法
    1.父元素固定高度
    2.父元素添加overflow:hidden
    3.在子元素的末尾添加高度为0的空div
    4.伪类
        父元素:after{
            content: "";
            height: 0;
            clear: both;
            overflow: hidden;
            display: block;
            visibility: hidden;
        }
# 页面元素滚动的原理
   容器元素的 clientWidth 小于 scrollWidth 时，在容器元素上会出现滚动条。
    容器元素的 scrollWidth 等于内部元素的 clientWidth
    由于 clientWidth 不包含滚动条，所以当滚动条已存在时。即使容器的宽度能完全展示内部元素，滚动条依然会存在。即只有当内部元素的宽度 = 容器 clientWidth + 滚动条宽度时滚动条才消失。
# 页面懒加载的实现
    <script>
        // 获取所有的图片标签
        const imgs = document.getElementsByTagName('img')
        // 获取可视区域的高度
        const viewHeight = window.innerHeight || document.documentElement.clientHeight
        // num用于统计当前显示到了哪一张图片，避免每次都从第一张图片开始检查是否露出
        let num = 0
        function lazyload(){
            for(let i=num; i<imgs.length; i++) {
                // 用可视区域高度减去元素顶部距离可视区域顶部的高度
                let distance = viewHeight - imgs[i].getBoundingClientRect().top
                // 如果可视区域高度大于等于元素顶部距离可视区域顶部的高度，说明元素露出
                if(distance >= 0 ){
                    // 给元素写入真实的src，展示图片
                    imgs[i].src = imgs[i].getAttribute('data-src')
                    // 前i张图片已经加载完毕，下次从第i+1张开始检查是否露出
                    num = i + 1
                }
            }
        }
        // 监听Scroll事件
        window.addEventListener('scroll', lazyload, false);
    </script>
## getBoundingClientRect()
    返回矩形的集合，与该元素相关的css边框集合
# overflow
    如何处理元素内容溢出
    hidden,scroll,visible,auto
## scroll和auto的区别
    scroll在需要有拖动条的时候会出现，不需要时会隐藏
    auto在需要有拖动条的时候会出现，不需要也会存在但是不可用
# 后台管理项目参考
    https://www.zhihu.com/answer/1017020768
# 图标字体库
    awesome


