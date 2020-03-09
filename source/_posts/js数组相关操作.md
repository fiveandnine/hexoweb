---
title: js数组相关操作
date: 2019-07-18 11:06:16
tags:
    - js
categories: 
    - Dictionaries
---
简介：js数组相关操作笔记

## 数组属性
length

prototype
可以挂在方法

constructor
## 判断数组
typeof  //String Object Number Undefined 
instanceof 返回true或false
```
instanceof Array
```

## 数组新建
Array === new Array
```
const list1 = Array()    //[]
const list2 = Array(3)   //[ , , ]
const list3 = Array(3,4,5)  //[3,4,5]
```

Array.of()
```
const list1 = Array.of()    []
const lsit2 = Array.of(3)   //[3]
const list3 = Array.of(3,4,5)   [3,4,5]
```

Array.from()
参数：
 - 1: 必填 要转化的对象
 - 2: 选填 每个对象的处理，类似于map方法
 - 3: 选填 要绑定的this
 
将两类数据转为数组，不改变原对象，返回新的数组
1.有length属性的对象
2.部署了Interator接口的数据结构，string map set
```
const obj1 = {0: 'a', 1: 'b', 2: 'c', length: 3}
const list1 = Array.from(obj1)  //['a', 'b', 'c']
```

## 数组方法
### 改变原数组的9个方法
pop
参数：🈚️
返回尾部弹出的一个元素

shift
参数：🈚️
返回弹出的第一个元素

unshift
参数：压入数组第一个的元素
返回数组长度

push
参数：压入数组最后的一个元素
返回数组长度

splice
参数：
 - 1.必填 起始位置
 - 2.选填 删除的数量(长度)
 - 3.选填 要插入的新项目
返回删除的项目组成的数组，没有删除返回[]
注：
 1. 如果元素不够，到最后一个为止
 2. 插入是在开始位置前面

sort
参数：
 - 参数可选: 规定排序顺序的比较函数，函数的两个参数(a, b)是要比较的两个参数，返回<0，则a在b前
会调用toString()方法 按Unicode排序
[实现机制-深入了解javascript的sort方法](https://juejin.im/entry/59f7f3346fb9a04514635552)

reverse

copyWithin
指定位置的成员复制到其他位置
```
array.copyWithin(target, start, end)
```
1. *不包括end*
2. 数组的长度不会改变，*读了几个元素就从开始被替换的地方替换几个元素*
3. 第一个参数是开始被替换的元素位置

fill
数组填充
参数：
 - 要填充数组的项目
 - 开始位置
 - 终止位置（不包括）默认为数组长度
长度不变


### 不改变原数组的8个方法
slice前拷贝数组项目
参数：
 - 起始位置
 - 结束位置（*不包括end*）（coopyWithin也不包括）

concat
连接两个数组，返回新数组

join
使用特定字符连接数组项目

indexOf
查找第一个符合条件的项目下标
```
array.indexOf(searchElement,fromIndex)
```

lastIndexOf
查找最后一个位置

toLocateString
每个链接的项目使用join(',') 方法连接

toString
值得注意的是：当数组和字符串操作的时候，js 会调用这个方法将数组自动转换成字符串
```
   let b= [ 'toString','演示'].toString(); // toString,演示
   let a= ['调用toString','连接在我后面']+'啦啦啦'; // 调用toString,连接在我后面啦啦啦
```

includes


## 数组遍历
 - 空数组不执行
 - 在迭代过程中删除的会跳过回调函数，修改的会传入新值
 - 遍历次数在第一次执行就确定，在增加不会执行回调函数
forEach
```
array.forEach(function(item, index, array){}, thisValue)
```
1. 无法退出，只能用return 返回，进入下一次循环
2. 总是返回undefined，即使你返回了一个指

map
返回新数组
```
array.map(function(item, index, array){}, thisValue)
```

filter
过滤 返回符合条件的值
```
array.filter(fucntion(item,index,array){}, thisValue)
```

some
返回true或false，只要有一个返回true，就会终止方法，返回true
```
array.some(function(item, index, array){}, thisValue)
```

every
返回true或false，只有所有都返回true，就会终止方法，返回true
```
array.every(function(item, index, array){}, thisValue)
```

reduce
数组提供累加器
initial = 第一个项目值，currentValue = 第二个项目值
```
array.reduce(function(total,currentValue,currentIndex,array){}, initialValue)
// total: 第一项的值或者上一次叠加的结果值
```
注：空数组，无initialValue时报错

reduceRight
数组提供累加器

find
数组中查找符合条件（return true）的第一个项目下标，没有则返回undefined
findIndex
数组中查找符合条件的第一个项目，没有返回-1
```
let new_array = arr.find(function(currentValue, index, arr), thisArg)
let new_array = arr.findIndex(function(currentValue, index, arr), thisArg)
```

keys
values
entries

for...of
在for..of中如果遍历中途要退出，可以使用break退出循环。

如果不使用for...of循环，可以手动调用遍历器对象的next方法，进行遍历:
```
let letter = ['a', 'b', 'c'];
    let entries = letter.entries();
    console.log(entries.next().value); // [0, 'a']
    console.log(entries.next().value); // [1, 'b']
    console.log(entries.next().value); // [2, 'c']
```

参考
> [掘金](https://juejin.im/post/5b0903b26fb9a07a9d70c7e0)