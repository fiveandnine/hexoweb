---
title: defineProperty
date: 2019-08-10 05:01:21
tags:
    - js
---

## 属性的特性以及内部属性
js三种类型属性
 - 命名数据属性
    有一个确定值
 - 命名访问器属性
    通过getter和setter进行读取和赋值的属性
 - 内部属性
    由JavaScript引擎内部使用的属性，不能通过JavaScript代码直接访问到

### Object.defineProperty()
两种为对象设置属性（不可以混用）
1. 数据属性
```
let obj = {}
Object.definePropety(obj, 'name', {
    value: 'xl',
    writable: true,
    configurable: true
})
```

2.访问器属性 
```
let obj = {}
let temp = null
Object.definePropety(obj, 'name', {
    getter: function(){
        return temp
    },
    setter: function(value){
        temp = value
    }
})
```
| 属性名 | 默认值 |
| ----- | ------ |
| value | undefined |
| getter| undefined | 
| setter| undefined |
| writable | false |
|configurable| false|
|enumberable| false|

```
let Person = {}

Person.name = 'xl'
<!-- 等价于 -->
Object.defineProperty(obj,'name',{
    value: 'xl',
    writable: true,
    configurable: true,
    enumerable: true
})

let Person = {
    name: 'xl'
}
<!-- 等价于 -->
Object.defineProperty(obj, {
    'name': {
        value: 'xl',
        writable: true,
        configurable: true,
        enumerable: true
    }
})

Object.defineProperty(obj,'name',{
    value: 'xl'
})
Object.defineProperty(obj,'name',{
    value: 'xl',
    writable: false,
    configurable: false,
    enumerable: false
})



```

## 其他方法
```
Object.preventExtensions(Person)  // 禁止扩展,但任然可以配置（赋值）
Object.seal() //在每个属性上调用preventExtesions,并且设置configurable: false
Object.freeze() //Object.seal(),并把所有现有属性标记为writable: false
```

赋值可能回调用原型上的setter，定义会创建一个自身属性。
原型链中的同名只读属性可能会阻止赋值操作，但不会阻止定义操作
定义 
```
Object.defineProperty(obj, 'bar', {
    value: '',
    writable: false,
    configurable: true
})
```
赋值不会改变原型链上的属性，只会在obj上新建一个自身属性







[https://www.jianshu.com/p/8fe1382ba135](https://www.jianshu.com/p/8fe1382ba135)