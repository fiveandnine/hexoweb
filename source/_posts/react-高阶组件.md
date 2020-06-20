---
title: react 高阶组件
date: 2020-03-02 14:35:29
tags:
  - react
---

## 高阶函数
传参为函数，返回也是函数，返回的函数会触发传入的函数
```aidl
function heighterFun(callback){
  return function(){
    callback && callback()
  }
}
```

### 高阶组件
传参为组件，返回也是一个组件，返回的组件会渲染我们之前传入的组件
```aidl
function Wrap(Component){
  return class extends React.Component {
      render() {
        return <Component />
      }
  }
}
```
#### 实现方式
1. 属性代理
2. 反向继承

1
```aidl

const Contain = WrapComponent =>{
  
  return class extends Component{
    render(){
      return <WrapComponent ...props/>
    }
  }
}
```
```aidl
class MyComponent extends Component{}

const NewComponent = Contain(MyComonent)

```
```aidl
//修饰器
@Contain
class MyComponent extends Component{} 

```
高阶组件的功能
1.控制props
```aidl
const Contain = WrapComponent => class extends Component{
  const newProps = {
    newText: "newText"
  }
  render(){
    return <WrapComponent ...props ...newProps/>
  }
}
```
