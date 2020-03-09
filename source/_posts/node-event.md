---
title: node event
date: 2020-02-25 15:23:47
tags:
  - Node
---
# events模块
使用
```
const EventEmitter = require('event')
class Man extends EventEmitter{ }
const Man = new Man()
let buyAj = (size) => {
  console.log("buy aj" + size)
}
let buyYeezy = ( size ) => {
  console.lg("buy yeezy" + size)
}
Man.on('rich', buyAj)
Man.on('rich', buyYeezy)
Man.emit('rich')
```

代码
```
function EventEmitter(){
  EventEmitter.init.call(this)
}
EventEmitter.init = funciton(){
  this._event = Object.create(null)
}
EventEmitter.on = function(eventName, callback, boolean){
  if (this._event[eventName]){
    boolean ? this._event[eventName].unshift(callback) : this
    ._event[eventName].push(callback)
  }else{
    this._event[eventName] = [callback]
  }
}
EventEmitter.emit = function(eventName, ...args){
  if(this._event[eventName]){
    this._event[eventName].forEach(callback => {
      callback.apply(this, args)
    })
  }
}
```

removeListener
```aidl
EventEmitter.removerListener = function(eventName, callback){
   if(this._event[eventName]){
    this._event[eventName] = this._event[eventName].filter
    (itemCallback) => {
      return (itemCallback !== callback && itemCallback.listener 
      !==callback )
    }
      
   }
}
```
once
```aidl
EventEmitter.once = function(eventName, callback){
  function wrap(...args){
    callback.apply(this, args)
    this.removeListener(eventName, wrap)
  }
  wrap.listener = callback
  this.on(eventName, wrap)
}
```
eventNames
```aidl
EventEmitter.prototype.eventNames = function(){
  return Object.keys(this._event)
}
```
removeAllListeners
```aidl
removeAllListeners = function(eventName){
  if(eventName){
    delete this._evnet[eventName]
  }else{
    this._event = Object.create(null)    
  }
}
```
prependListener
```aidl
EventEmitter.prependListener = function(eventName, callback){
  this.on(eventName, callback, true)
}
```
prependOnceListener


[refer](https://www.jianshu.com/p/152fddf0628c)
