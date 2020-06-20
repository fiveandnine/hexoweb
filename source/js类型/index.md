---
title: js类型
date: 2020-05-06 16:44:20
  - js
---

```js
var class2Type = {}

// 生成class2type映射
"Boolean Number String Function Array Date RegExp Object Error Null Undefined".split(" ").map(function(item) {
    class2Type["[object " + item + "]"] = item.toLowerCase();
})

function type(object){
  if(object == null){
    return '[object null]'
  }
  return typeof object === 'obect' || typeof object === 'function' 
  ? class2Type[Object.prototype.toString.call(object)] : typeof object
  
}
```
