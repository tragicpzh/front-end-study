# AOP 面向切面编程

## 简介

将跟核心业务逻辑模块无关的功能抽离出来，再通过“动态织入”的方式参与业务逻辑模块当中去。

## 实现方法

    利用function.prototype实现before,after,around函数：

    // before
    Function.prototype.before=function(beforefn){
      var _self=this;
      return function(){
        var tmp=beforefn.apply(this,arguments);
        //if(tmp...)return ...; 用于阻塞函数
        return _self.apply(this,arguments);//执行原函数
      }
    }

    //after
    Function.prototype.before=function(afterfn){
      var _self=this;
      return function(){
        var tmp=_self.apply(this,arguments)
        //if(tmp...)return ...;用于阻塞函数
        afterfn.apply(this,arguments);
        return tmp;
      }
    }

    //around
    function JoinPoint(obj,args){
      var isapply=false;
      var result=null;
      this.source=obj;
      this.args=args;
      this.invoke=function(thiz){
        if(isapply)return;
        isapply=true;
        result=this.source.apply(thiz||this.source,this.args);
        return result;
      }
      this.getResult=function(){
        return result;
      }
    }
    Function.prototype.around=function(aroundfn){
      var _self=this;
      return function(){
        var args=[new JoinPoint(_self,arguments)];
        return func.apply(this,args);
      }
    }
