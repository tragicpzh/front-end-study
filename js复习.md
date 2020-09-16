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
# map和foreach()
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