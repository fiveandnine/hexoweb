---
title: code-snippet cache
date: 2020-03-17 11:14:34
tags:
  - code-snippet
---
## cache
```aidl
export const setCache = (key, value) => {
  if(typeOf value === 'object'){
      _value = JSON.stringify(value)
  }
  window.localStorage.set(key, _value)
}

export const getCache = (key, isObject = true) => {
  let value = window.localStorage.getItem(key) 
  if( isObject ){
    try{
      value = JSON.parse(window.localStorage.getItem(key))
    }catch(){
      value = {} 
    }
  }
  return value
}

export const removeCache = (key) => {
   window.localStorage.removeItem(key)
}

export default {
  setCache,
  getCache,
  removeCache
}

```

```aidl
//url 缓存
export default class Cache {
  static getID ({url, params, data, method, baseURL, headers}){
    return Symbol.for(hash(url, params, data, method, baseURL, headers))
  }
  constructor(){
    this._cache = {}
  }
  getCache = (id, scope = "global") => {
    if(typeOf id != "symbol"){
      id = this.constructor.getID(id) 
    }
    
    return get(this._cache, `${[scope]}`, {})[id]
  }
  append = (key, value, scopeName) => {
    const id = getID(key)
    this._cache[scopeName] = Object.assin(
      {},
      this._cache[scopeName],
      { id: value }
    )
    return this
  }
  clean = () => {
    
  }
  get allCache = () => {
    
  }
}
```
注： get方法中 get(obj, "[name]") ===> get(obj, "name")


## instanceof
```js
function myInstanceof (left, right){
  if(typeof left !=='object' || left === null) return false
  
  while (true){
    let pro = Object.getPrototypeOf(left)
    
  } 
}
```
