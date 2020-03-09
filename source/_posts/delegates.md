---
title: delegates
date: 2020-02-24 17:00:12
tags:
  - js
  - node
---
### __defineSetter__ 
### __defineGetter__
### defineProperty
# delegates
快速使用委托模式，delegate pattern，外层暴露的对象委托给内部的其他对象处理
```aidl
const delegates = require('delegates')
const petShop = {
  dog: {
    name: 'xxx',
    age: '22',
    sex: 'xxx',
    bar(){
        console.log('bar!')
    }
  }
}

delegates(petShop, 'dog').getter('name').setter('aga').access
('sex').method('bar').fluent('name')
```

源码
```aidl

```

[refer](https://blog.csdn.net/weixin_33766168/article/details/91428790)
