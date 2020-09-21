# react-router-dom

## 容器 Router

    将UI与URL联系在一起
    BrowserRouter HashRouter MemoryRouter StaticRouter
    相关参数：basename forceRefresh keyLength

## 历史 history

    主要属性和方法：
    length action location
    push replace go(n) goBack()(go(-1)) goForward()(go(1)) block
    location:{
        pathname:URL
        search:查询字符串
        hash：hash片段
        state:location状态
    }
    如何创建：
    history=createBrowserHistory()

## 链接 Link

    属性和方法：
    to:string/object
    replace:bool,true时替换history栈而不是新添加，默认为false
    others:className ID style

## 导航链接 NavLink

    新添加的属性：
    activeClassName:活动状态的样式
    activeStyle:活动状态的样式

## 重定向 Redirect

    属性和方法：
    to:string/object
    push:bool true时重定向推入history栈而不是替换，默认为false
    from:识别from中的path并将参数传递给to，但是to中未使用的参数会被忽略

## 匹配 Route

    当path与URL匹配时，显示对应的组件
    属性和方法：
    props:match location history，作为props传入组件
    component:组件，加载时会创建新组件，所以有卸载安装的过程
    render:渲染同一个组件，默认传入的参数为props,便于包裹和内联渲染
    children:与render相同，但是可以访问match(判断路径是否匹配位置)

## 选择 Switch

    只渲染匹配的第一个Route
    属性和方法：
    location:用于匹配子元素，而不是当前位置URL

## match

    属性：
    params:以key/value的形式记录传入URL的参数
    isExact：判断是否完全匹配path
    path:<Route>
    url:<Link>

## matchPath()

    参数(pathname,props)
    生成一个和<Route>相同的代码

## withRouter

    高阶组件

## 什么是路由

    用户想去哪，就带到哪

## 路由的切换

    不同url-不同页面-不同组件

## window.location.pathname 与 window.location.hash 的区别

    前者跳转时页面会刷新，后者不会
    作为替代是H5中的window.history.pushState()

## 原理

    window.history对象操作，当旧版服务器不能使用时，router内置了polyfill来兼容

## hash 与 browser 区别

    hash实现了渲染不同的视图，并产生历史访问的数据，不会刷新页面，对后端发送的请求只有hash（#）前的url
    browser模式中url变化，会导致页面刷新，但是H5的history对象解决了这个问题，但是对后端发送的请求是和前端的URL一致的
