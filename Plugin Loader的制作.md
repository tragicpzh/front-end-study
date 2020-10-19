# Loader

## 基本结构

    loader是一个js函数(暴露为模块)，参数为
      content:源文件字符串
      map：sourcemap  错误位置的映射
      meta:元数据
    第一个loader只有content
    最后一个loader应输出content(js代码,输出应为模块),map(可选)
    loader的顺序为从右到左输入数据

```javascript
  //同步loader
  export default function(content,map,meta){
    /*loader相关操作*/
    //中间loader
    this.callback(err,values...)//values:[content,map,meta]
    return;
    //最后的loader
    return `export defalut ${content}`;
  }
  //异步loader
  必须使用callback //callback=this.async()
```

    loader的原则：
        简单易用
        链式传递
        模块化输出
        无状态(独立于其他编译模块)

## loader 配置

```javascript
  //umirc.ts
  ...
  chainWebpack(config){
    config.module
      .rule('规则名')
      .test('文件匹配')
      .use('loader名')
      .loader('loader具体位置') //path.join(__dirname,'xx')
  }
  ...
```

# Plugin

## 基本结构

     插件是一个js函数(暴露为模块)
     umi:
      参数为api:umi暴露的api接口
     webpack:
      complier:webpack环境配置，原型方法apply可获得
      compliation:webpack的资源版本构建,提供了一些钩子函数(hooks)，complier.plugin可获得

仅展示 umi-plugin

```javascript
export default function (api: IApi) {
  /*api相关操作*/
}
```

## 配置

```javascript
//umirc.ts
...
plugins:[...plugins]//每个plugin的地址
...
```
