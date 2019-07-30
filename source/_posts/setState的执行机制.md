---
layout: react
title: setState的执行机制
date: 2019-07-21 09:30:10
tags:
---

## setState
```
setState(updater, [callback])
```
updater: 跟新数据 FUNCTION／Object
callback: 更新后的回掉函数

*浅合并 Objecr.assign()*
```
this.setState((state, props)=>{
    return {
        count: state + props
    }
})

this.setState({
    count: '10'
})
```

## setState源码
#### this.setState()
```
ReactComponent.prototype.setState = function(partialState , callback){
    this.updater.enqueueSetState(this, particalState) 
    //this组件的实例
    //updater就是reactUpdateQueue
    if (callback){
        this.updater.enqueueCallback(this, callback, 'setState')
    }
}
```
---
#### enqueueSetState()
```
enqueueSetState: function(publicInstance, particalState){
    //获取实例
    var internalInstance = getInternalInstanceReadyForUpdate(publicInstance,'setState')
    //初始化跟新队列
    var queue = internalInstance._paddingStateQueue || (internalInstance._paddingStateQueue)
    //将state放入数组
    queue.push(particalState)
    //将要更新的组件放入队列
    enqueueUpdate(internalInstance)
}
```
---
#### enqueueUpdate()
如果正处于更新／创建组件时，不会立即去更新组件，而是先把当前组件放到dirtyComponent里，所以不是每次的state跟新都会跟新组件
```
enqueueUpdate: function(component){
    if(!batchingStrategy.isBatchingUpdates){
        batchingStrategy.batchedUpdates(enqueueUpdate, component)
    }
    dirtyComponets.push(component)
}
```
---
batchingStrategy
```
var ReactDefaultBatchingStrategy = {
    isBatchingUpdates: false,
    batchedUpdates: function(callback, a, b, c, d, e){
        var readyBatchingUpdates = ReactDefaultBatchingStrategy.isBatchingUpdates;
        ReactDefaultBatchingStrategy.isBatchingUpdates = true;
        if(readyBatchingUpdates){
            return callback(a, b, c, d, e)
        }else{
            // 否则执行更新事务
            return transaction.perform(callback, null, a, b, c, d, e);
        }
    }
}
```
---
#### transaction
initalize(空函数) -> perform(anyMethos) -> close
```
var RESET_BATCHED_UPDATES = {
    initialize: emptyFunction,
    close: function () {
        ReactDefaultBatchingStrategy.isBatchingUpdates = false;
    }
}
var FLUSH_BATCHED_UPDATES = {
    initialize: emptyFunction,
    close: function () {
        ReactUpdates.flushBatchedUpdates.bind(ReactUpdates)
    }
}
var TRANSACTION_WRAPPERS = [FLUSH_BATCHED_UPDATES, RESET_BATCHED_UPDATES];
```

*总结*
1.setState 只在合成事件和钩子函数中是“异步”的，在原生事件和 setTimeout 中都是同步的。
2.setState的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的，**只是合成事件和钩子函数的调用顺序在更新之前**，导致在合成事件和钩子函数中没法立马拿到更新后的值，形式了所谓的“异步”，当然可以通过第二个参数 setState(partialState, callback) 中的callback拿到更新后的结果。
3.setState的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的，在原生事件和setTimeout 中不会批量更新，在“异步”中如果对同一个值进行多次 setState ， setState 的批量更新策略会对其进行覆盖，取最后一次的执行，如果是同时 setState 多个不同的值，在更新时会对其进行合并批量更新。


### setTimeout中的setState
基于*[event loop]*的模型下， setTimeout 中里去 setState 总能拿到最新的state值。


>[setState机制](https://segmentfault.com/a/1190000016805467)



































