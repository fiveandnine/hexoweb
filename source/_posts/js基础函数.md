---
title: js基础函数
date: 2019-07-22 10:05:05
tags:
    - js
categories: 
    - Dictionaries    
---
## call(thisArg, arg1, aeg2, ...)
把需要改变this指向的方法挂载到目标this上执行并返回
调用一个对象的方法，以另一个对象替换当前对象，如果没有就用Global对象替换
参数：
 - thisArg 当要被用作当前对象的对象
 - arg1, aeg2, ... 要传入方法的参数
```
Function.prototype.mycall = function(context=window){
    if ( typeof this != 'function' ){
        throw new TypeError('not function') 
    }
    context.fn = this
    var args = [...arguments].slice(1)
    var results = context.fn(...args)
    delete context
    return results 
}
```
```
//demo1
function add(a,b) { 
    alert(a+b); 
} 
function sub(a,b) { 
    alert(a-b); 
} 
add.call(sub,3,1);
//demo2
function c1(){
    this.name = 'c1';
    this.consoleLog = function(){
        console.log(this.name)
    }
}
function c2(){
    this.name = 'c2';
    this.consoleLog = function(){
        console.log(this.name)
    }
}
var class1 = new c1()
var class2 = new c2()
class1.consoleLog.call(class2)
```
---
## apply(thisArg, [...])
调用一个对象的方法，以一个对象替换当前对象，（同call，只是参数不一样）
```
Function.prototype.myapply = function(context){
    if(typeof this !== 'function'){
        throw new TypeError('this not function')
    }
    context = context || window
    context.fn = this;
    var args = [...arguments][1]
    var results = context.fn(...args)
    delete context
    return results
}
```
---
## bind(thisArg,...)
```
Function.prototype.mybind = function(context){
    if( typeof this !== 'function'){
        throw new TypeError('this not function')
    }
    var _this = this
    //context = context || window
    //context.fn = this
    var args = [...arguments].slice[1]
    return function F(){
        if(this instanceof F){
            return new _this(...arg, ...arguments)
        }else{
            _this.apply(context, [...args].concat(arguments))
        }
    }
}
```
---
## instanceof
右边变量的原型存在于左边变量的原型链上
```
function(left, right){
    var l = left.__proto__
    var r = right.prototype
    while(true){
        if(l === undefined){
            return false
        }
        if(l === r){
            return true
        }
        l = l.__proto__
    }
}
```
---
### Object.create
将传入对象作为原型
```
function create(obj){
    function F(){}
    F.prototype = obj
    return new F()
}
```
---
### new 本质
- 新建一个控对象
- 将对象的```_proto_```指向构造函数的prototype成员对象
- 使用```apply```调用构造函数，属性和方法被添加到this引用的对象中
- 如果构造函数没有return其他函数，则返回this， 即创建的新对象，否则返回对象

### 浅拷贝

### 深拷贝

### 继承
