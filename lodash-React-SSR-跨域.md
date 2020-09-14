# 1.JS工具库lodash
# 2.函数式组件使用refs
## 1.useRef(initstate)返回一个ref对象，.current属性=initstate
## 2.forwardRef(compenents:(props,ref)=>{})让函数式子组件获得ref
## 3.useImperativeHandle(ref,createHandle,[deps])让子组件暴露父组件需要的值
## 4.useCallback(fn,[deps])让父组件可以获取到子组件实时的值。fn:(node)=>{}node等价于ref.current属性
# 3.React Fragments
## 当组件需要渲染的节点不能被包含在一个标签内时（如多个<td>）,使用<React.Fragment>或<>
# 4.Portals传送门
## 当子节点需要渲染到父组件之外的DOM节点时使用Portals。createPortals(child,container)
# 5.高阶组件（HOC）
## 1.高阶组件时参数为组件，返回值为组件的函数
## 2.function fuc(WrappedComponent,selectData){
  class xxx extends React.compenent{
    ...
    render(){
      return <WrappedComponent...>
    }
  }
  hoistnonreactstatics(XXX,WrappedComponent)复制静态方法(import hoistnonreactstatics from 'hoist-non-react-statics')
}
# 6.SSR服务器端渲染
## Sever-Side Rendering 将SPA应用打包到服务器上，在服务器端渲染HTML并发送给浏览器，与SPA框架配合生成应用程序。
  能够解决首屏慢的问题
  占用更多CPU和内存。
# 7.SPA单页应用
## Single-page-application,在一个页面中动态地重写页面部分与用户交互。
  页面切换快；前后端分离
  首屏打开速度慢，因为用户需要下载SPA框架及应用程序代码；不利于SEO
# 8.SEO搜索引擎优化
## 利用搜索引擎的规则提高网站在有关搜索引擎内的自然排名。
# 9.同源
## 两个页面的协议、端口、域名相同
# 10.同源策略
## 一个源加载的文档或脚本默认不能访问另一个源的资源。（链接、重定向、表单提交不受限制）
#11.解决跨域的两种方法
## 1.CORS
### Cross-Origin Resource Sharing跨域资源共享。在服务器端设置一系列的HTTP头，在请求和响应时加上这些HTTP头。
    请求分为简单请求和复杂请求。
    1.简单请求：
      浏览器在HTTP请求头部加入origin字段说明来自哪个源（如:http://api.bob.com）,服务器根据这个值决定是否同意。
      如果Origin指定的源，不被许可，服务器返回正常的HTTP回应，但是不包含Access-Control-Allow-Origin字段。浏览器会根据
      该字段抛出错误。
      如果Origin指定的源，被许可。则在HTTP回应中附加Access-Control-Allow-Origin(origin或*)/~-Allow-Credentials(是否允许发送Cookie)/~-Expose-Headers(CORS返回的额外字段)
      如果想要发送cookie，1.Access-Control-Allow-Credentials=true,2.发送AJAX请求时，设置withCredentials=true(xhr.withCredentials=true)
    2.复杂请求：请求方法是PUT或DELETE，Content-type=application/json
      正式通信前，增加一次HTTP查询请求，称为预检请求，该请求为OPTIONS请求包括三个特殊字段：1.Origin 2.Access-Control-Request-Method(CORS请求涉及哪些HTTP方法) 
      3.Access-Control-Request-Headers(CORS请求会额外发送的头信息字段)。
      服务器端检查了这三个字段后，发送HTTP回应，如果没有任何CORS相关头信息字段，那么认定服务器不同意预检请求。
      如果服务器端同意，则会发送多个CORS相关字段，关键字段为Access-Control-Allow-Origin，其他字段有~-Method(支持的所有方法),~-Headers,~-Credentials,~-Max-Age(有效期)。
      预检请求通过后，之后的CORS请求都为简单请求。
## 2.代理解决跨域
      正向代理：本机通过代理服务器访问目标主机（隐藏客户端）
      反向代理：本机访问代理服务器，代理服务器转发请求至服务器（隐藏服务端）
      原理：发送请求时将本机域名转为目标主机的域名，通过中间层的转换来发送同源的请求。
      react反向代理：
      npm install http-proxy-middleware --save
      const {createProxyMiddleware}=require('http-proxy-middleware);
      module.exports=function(app){
          app.use(createProxyMiddleware('/api',{
              target:,
              secure, //https接口
              changeOrigin,
              pathRewrite:{
                "^/api":"/"
              }
          }))
      }
      umi反向代理:
        proxy:{
          '/api':{
            target:
            secure:
            changeOrigin:
            pathRewrite:
          }
        }



