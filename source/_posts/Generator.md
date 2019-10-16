---
title: Generator
date: 2019-07-17 21:23:44
tags:
---
## 基础语法
- generator是状态机，里面封装了多个状态
- 执行generator函数会返回一个遍历器对象，所以除了是状态机之外还是一个遍历器对象生成函数，返回的遍历器对象可以遍历内部每个状态
- 特点：function关键字和函数名字之间有一个 * ，函数内部使用yield表达式，定义不同的内部状态
```aidl
function * helloworldgenerator(){
    yield 'hello'
    yield 'world'
    return 'ending'
}
var hw = helloworldgenerator()
hw.next(); //{value: 'hello', done: false}
hw.next(); //{value: 'world', done: false}
hw.next(); //{value: 'ending', done: true}
hw.next(); //{value: undefined, done: true}


```
返回的hw不是函数执行结果，而是指向函数内部状态的指针对象，也就是遍历器对象

## yield表达式
运行逻辑
- 只用调用next方法才会遍历下一个内部状态，其实提供了一个能暂停执行的函数，yield表示暂停标示。
- 类似js惰性求值

## iterator
任意对象的Symbol.iterator方法等于该对象的遍历器生成函数
```aidl
var m = {}
m[Symbol.iterator] = function *(){
    yield 1
    yield 2
    yield 3
}
[...m]  //[1,2,3]
```
```aidl
function *gen(){
    //some code
}
g = gen()
g[Symbol.iterator] === g

```
## next方法的参数
 - yield表达式本身没有返回值，或者说返回值一直都是undefined
 - next的参数会作为上一个yield表达式的返回值
 - 第一次使用next方法时传递参数是无效
```aidl
function *f(){
    for (i = 0; true; i++){
        var reset = yield i;
        if(reset){
            i = -1
        }
    }
}
var g = f()
g.next();        //{value: 0, done: false}
g.next();        //{value: 1, done: fasle}
g.next(true);    //{value: 0, done: false}
```
```aidl
function* foo(x) {
  var y = 2 * (yield (x + 1));
  var z = yield (y / 3);
  return (x + y + z);
}
var a = foo(5);
a.next();        //{value: 6, done: false}
a.next();        //{value: NaN, done: false}
//没有返回值 2*undefined ／3  = NaN
a.next();        //{value: NaN, done: false}
//5 + NaN + undefined  = NaN

var b = foo(5);
b.next(); //{value: 6, done: false}
b.next(12); //{value: 8, done: false}
b.next(13); //{value: 6, done: false}

```
实现斐波那契数列的例子
```aidl
function * fibonacci(){
    let [pre, curr] = [0, 1]
    for(;;){
        yield curr;
        [pre, curr] = [curr, pre+cur]
    }
}
for(let n of fibonacci()){
    if(n>1000) break;
    console.log(n)
}

```
## 对象扩展Iterator 接口

## Generator.prototype.throw()

## Generator.prototype.return()
 - return可以直接返回对应的值并结束Generator函数
 
 
 
 [参考阮一峰](http://es6.ruanyifeng.com/#docs/generator)
