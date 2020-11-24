# SSR 的出现原因

    客户端渲染，依靠js代码拉取来完成界面渲染
    1.速度慢，需要运行js代码进行大量dom操作
    2.seo不友好，爬虫无法识别JS文件

# CSR 的好处和弊端

## 好处

    1.直接返回html字符串、JS文件、css文件，首屏加载快
    2.网页能够有清晰的html结构，便于爬虫获取数据，提高搜索引擎排名

## 弊端

    1.前后端耦合，不利于分工协作
    2.加大服务端压力

# 如何实现 React 的 SSR

    1.react组件转化为html语言---react-dom(renderToString:react组件->html字符串)
    2.同构，当页面渲染涉及事件绑定时，需要额外的js文件---(ReactDom.hydrate:取出react组件的事件绑定)
    3.解决路由问题，对组件进行路由组件包装后转换为html字符串---StaticRouter/renderRoutes
    4.引入redux,创建全局store->与客户端/服务端store连接---Provider组件
    5.异步数据的服务端渲染方案：数据注水与脱水
        注水：将服务端store数据注入到全局作用域
        脱水：把全局作用域绑定的数据返回给客户端
    6.CSS服务端渲染：定义css文件->webpack进行转译->放入StaticRouter的context

# 使用 node 作中间层

    代替客户端处理数据，替前端接管了对数据的操作,减轻前端计算压力
