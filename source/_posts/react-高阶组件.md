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
