---
title: 异步编程 promise async Generator
date: 2020-03-25 20:52:47
tags:
---

## Promise
```aidl
cons p = new Promise((resolve, reject) => {
  setTimeOut(()=>{
    resolve('resolve value')
  }, 2000)
  
  setTimeOut(()=>{
    reject('reject value')
  }, 3000)
})
p.then(resolveValue => console.log(resolveValue), rejectValue => console.log(rejectValue))

```
执行流程：
1 Promise接受一个executor函数，new Promise()时立即执行
2 executor函数里面的异步任务被放到宏/微任务队列，等待执行
3 then被执行，收集成功回调和失败回调
4 executor函数里面的异步任务被执行，触发resolve/reject，从成功/失败队列中取出回调依次执行

```aidl
class MyPromise {

}
```

### promise A+规范
1. promise本质是状态机，只能从padding-->Fulfilled-->Rejected，只能单项状态不可逆
2. then方法接受两个参数，分别对应状态该改变的回调，then返回一个promise，then方法可以被一个promise调用多次。
```aidl
class MyPromise {
  constructor(executor){
    this._status = 'PADDING'
    this._resolveQueue = []
    this._rejectQueue = []
    const _resolve = (value) => {
      if(this._state !== 'PADDING') return false
      this._state = 'FULFILLED'
      while(this._resolveQueue.length){
        const cb = this._resolveQueue.shift()
        cb(value)
      }
    }
    const _reject = (value) => {
      if(this._state !== 'PADDING') return false
      this._state = 'REJUSED'
      while(this._rejectQueue.length){
        const cb = this._rejectQueue.shift()
        cb(value)
      }
    }
    executor(_resolve, _reject)
  }
  then(_resolveFn, _rejectFn){
    this._resolveQueue.push(_resolveFn)
    this._rejectQueue.push(_resolveFn)
  }
}
```

then方法修改，返回promise(链式调用)
```aidl

then(resolveFn, rejectFn){
  return new MyPromise((resolve, reject)=>{
    const FulFilledFn = value => {
      try{
        const x = resolveFn(value)
        x instandof MyPromise ? x.then(resolve, reject) : resolve(x)
      } catch(err){
        reject(err)
      }
    }
    this._resolveQueue.push(fulfilledFn)
    //reject

    
  })

}
```




[refer](https://juejin.im/post/5e3b9ae26fb9a07ca714a5cc#heading-20)
