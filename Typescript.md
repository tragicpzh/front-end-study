# Typescript
## 接口 interface
   ```
   对象接口
   interface xx{
       color:string;        //必需属性
       number?:number;      //可选属性
   }
   函数接口
   interface func{
       (name:string,age?:number):boolean; //不要求函数参数名相同
                                          //可选参数必需接在必需参数之后
   }
   数组接口 
   interface arr{
       [index:number]:string; //index:number|string
   }
   拓展接口
   interface xx{

   }
   interface yy extends xx{

   }
   混合接口
   interface xx{
       (name:string):boolean;
       interval:number;
       reset():void
   }
   ```
## 类类型
    类有两个类型：静态和实例
    静态是这个类（函数）本身（constructor(),static）
    实例是类实例化的对象
## 实现，继承（扩展）
    实现:implements
    继承:extends
## 有状态组件
interface Props{
    
}
interface State{

}
class App extends React.Commponent<Props,State>{
    public render(){

    }
}
## 无状态组件
import {SFC} from 'React'
interface Props{

}
const App:SFC<Props>=()=>{

}
## 事件处理
function handleEvent(event:xxxEventHandler<HTMLDivElement>)
## Promise<T>
interface Response<T>{
    xx
}
async function getResult(): Promise<Response<T>>{
    return{
        xx
    }
}
getResult()
    .then(result=>{})
## 工具泛型使用技巧
    1.typeof
    const options={
        a:1
    }
    2.字符串字面量
    interface Props{
        color:'red'|'blue'
    }
    3.数字字面量
    interface Props{
        num:0|1
    }
    4.Partial 转为可选项
    const APP:SFC<Partial<Props>>
    5.Required 转为必需项
    const APP:SFC<Required<Props>>
