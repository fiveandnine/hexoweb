---
title: js引擎
date: 2020-04-26 16:39:17
tags:
  - js
---
## js引擎
相关概念
执行环境栈、全局对象、执行环境、变量对象、活动对象、作用域、作用域链
```
var x = 1
function A(y){
   var x = 2;  //定义一个局部变量 x
   function B(z){ //定义一个内部函数 B
       console.log(x+y+z);
   }
   return B; //返回函数B的引用
}
var C = A(1); //执行A,返回B
C(1); //执行函数B，输出 4
```
### 全局初始化
 - 创建全局对象GO(global object)
 ```
  var GO = {
    Math: {},
    String: {},
    Date:{},
    document:{}, //DOM操作
    ...
    window: this
  }
```
 - 执行环境栈(Execution Context Stack)，在创建一个**全局执行环境**EC(Execution Context)
 ```
 ECstack = []
 EC = {}
 
 ECstack.push(EC)
 ECstack.pop(EC)
 ```
 - 创建一个与EC关联的全局变量对象VO(Varibale Object)，并指向全局对象Global Object
 
```js
var ECstack = [
  EC(G) = {
      VO(G) = {
        ... //包含全局对象原有的属性
        x = 1,
        A = function(){},
        A[[scope]] = this//给A添加一个内部属性，并赋值给VO
      }
  }
]
//在定义每个函数的时候都会创建一个与之关联的scope属性，scope重视指向定义当前函数的所在环境，即执行环境E
```
执行A函数的时候
```js
var ECstack = [
  EC(A) = {
    [scope]: VO(G),
    AO(A): {
      x: 2, //定义一个局部变量 x
      B: function(z){}, 
      B[[scope]]: this,//指向AO(A)本身
      argument: [],
      this: window
    },
    scopeChain: <AO(A), A[[scope]]>
  },
  EC(G) = {
    VO(G): {
      ...
      x: 1,
      A: function (y){},
      A[[scope]]: this //VO(G)
    }
  }
]
```
变量对象和活动对象只是不同的叫法，只是在函数中的叫法不同而已（你可以认为变量对象是一个总的概念，而活动对象是它的一个分支）

执行B函数的时候
```js
var ECstack = [
  EC(B) = {
    [scope]: AO(A),
    AO(B): {
      z: 1,
      arguments: [],
      this: window
    },
    scopeChain: <AO(B), B[[scope]]>
  },
  
]
```
函数执行的时候，js引擎会生成一份EC，每次函数声明的时候都会生成AO
#### refer
[探索JS引擎工作原理](https://www.cnblogs.com/onepixel/p/5090799.html)
