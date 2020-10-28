# 防抖和节流

## 防抖

    持续触发事件时，当一段时间没有触发后才执行函数。如果期间再次触发则重新计时。

## 节流

    持续触发事件时，保证一定时间内只调用一次函数。

## 函数实现

    防抖：
        function debounce(fn,wait){
            var timeout=null;
            return function(){
                if(timeout!==null)clearTimeout(timeout);
                timeout=setTimeout(fn,wait);
            }
        }
    节流:
        function throttle(fn,wait){
            var now=Date.now();
            var timer=null;
            return function(){
                var cur=Date.now();
                var remain=wait-(cur-now);
                var content=this;
                var args=arguments;
                clearTimeout(timer);
                if(remain<=0){
                    fn.apply(content,args);
                    now=cur;
                }
                else {
                    timer=setTimeout(fn,wait);
                }
            }
        }

# map 和 foreach()

    map返回新数组，foreach返回undefined

# 箭头函数和普通函数的差别

    1.更简洁
    2.没有this
    3.不能使用new
    4.不绑定arguments,使用rest参数（rest参数是真正意义上的数组）
    5.捕获其所在的上下文this，作为自己的this
    6.使用call和apply调用
    7.箭头函数没有原型
    8.不能简单返回对象字面量
    9.不能当做generator函数，不能使用yield
    10.不能换行

# setTimeout 丢帧

    1.setTimeout的执行时间并不是确定的，因为它被放入了异步队列，只有主线程执行完以后，才会去检查该队列任务是否需要执行，因此setTimeout的实际时间比设定时间晚一些
    2.刷新频率受屏幕分辨率和屏幕尺寸的影响，不同设备不同，而setTimeout只能设置固定时间间隔，这两个时间不一定相同。

# 判断数组的方法

    1.instanceof 运算符
    2.constructor
    3.Array.isArray()
    4.Object.prototype.toString.call(data)==='[object Array]'

# 判断字符串类型

    1.Object.prototype.toString.call(data)==='[object String]'
    2.constructor

# this

## 概念

    指的是函数运行时的上下文环境，this被谁执行了，this就是执行谁的。

## 默认执行

    this执行了window

## 隐式执行

    1.改变函数引用
    2.函数传参
    3.定时器传参
    4.Dom对象事件

## 显示执行

    bind call apply

# date 相关操作

```
   new Date(year,month,day) month为0-11
   date.getMonth()
   date.getFullYear()
   date.getDate() 返回几号
   date.getDay()  返回星期几 0-6 0-星期天
   date.getHours()
   date.setDate()
   其余对应
   date.parse(string)将“月/日/年”转为date类型，可以传参前对 string进行正则替换
```

# Map 和 Set

## Set

```javascript
    //创建
    var s=new Set();
    //添加
    s.add(x);
    //遍历
    for(let i for s){
        console.log(i)
    }
    //大小
    s.size
    //删除
    s.delete(x)
    //判断
    s.has(x)
    //清空
    s.clear()
    //转数组
    [...set]
```

## Map

```javascript
//创建
var m = new Map();
//添加
m.set(key, value);
//取值
value = m.get(key);
//大小
m.size;
//判断
m.has(key);
//删除
m.delete(key);
//清空
m.clear();
//遍历
for (let [key, value] of map) {
  console.log(key, value);
}
//转数组
[...map];
```

# 窗口和视口的相关函数与属性

## 属性

```javascript
    event:{
        screenX/Y:距离电脑屏幕的距离
        clientX/Y:距离页面边界距离(受滚动影响)
        pageX/Y:距离页面边界距离(不受滚动影响)
        offsetX/Y:距离当前元素的边界距离(行内元素无效),除safari不包含边框
    }
    element:{
        clientHeight/Width:content+padding-滚动条
        clientLeft:元素左边框宽度(border-left),如果有左侧滚动条则包含滚动条宽度
        clientTop:元素顶部边框宽度(border-top)
        offsetWidth/Height:content+padding+border(包含滚动条)
        offsetParent:最近的定位父元素|table|tabel cell|根元素(html body)
        offsetTop/Left:与offsetParent内边距边界的距离
        getClientRects:获取元素占据的所有矩形区域(每个inline元素),返回textRectangle集合
        getBoundingClientRect:获取元素的盒子模型,返回textRectangle对象
        scrollTop/Left:元素滚动的距离(可用此属性来实现滚动变化)
        scrollHeight/Width:max(内容区域,元素宽度),包含被滚动隐藏的内容
    }
    window:{
        innerWidth/Height:视口宽度/高度，不包括侧边栏
        outerWidth/Height:视口宽度/高度，包括侧边栏/浏览器顶部栏
        scrollX/Y(pageX/YOffset):页面滚动的距离
        screenX/Y(screenLeft/Top):浏览器左边框到屏幕边缘
        scroll(x,y,option)/scrollTo(x,y)|(option):滚动到(x,y),option:{top,left,behavior(smooth,instant)}
    }
    计算一个元素的位置:{
        x:element.getBoundingClientRect.left+document.documentElement.scrollLeft
        y:element.getBoundingClientRect.top+document.documentElement.scrollTop
    }
```
