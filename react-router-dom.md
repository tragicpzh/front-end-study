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


