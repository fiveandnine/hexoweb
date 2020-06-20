---
title: js循环
date: 2020-04-30 15:00:19
tags:
  - js
categories: 
    - Dictionaries
---
 ###for 循环

 - continue 退出当前循环的item，直接进入下个item
 - break 退出循环
 
 ###for key in object
 遍历对象属性
 
 ###for of
 break可以退出循环
 
 ###forEach
 - return 退出当前循环的item，进入下个item，相当于for的continue

 #### $.each
```js
$.each(object, [callback])
callback(i, value)
```
i: 对象成员或者是数组的索引
value: 对应变量或者数组的值

return false可以退出循环，其他的返回值会被忽略

```js
$.each = function (object, callback){
  if (isArrayLike(obj)){
    for (var i = 0; i < object.length; i++){
      if (callback.call(object[i] ,i, object[i]) === false){
        break;
      }
    }
  }else{
    for (var key in obj){
      if (callback.call(obj[key], key, obj[key]) === false){
        break;
      }
    }
  }
}
```
