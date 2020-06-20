---
title: EventLoop
date: 2020-06-10 11:50:34
tags:
---
## 浏览器

### 宏队列
浏览器api

setTimeOut setInterval I/O requestAnimationFrame

UI rendering (浏览器独有ENV)

主： setTimeOut的解释是多少秒后会把回掉方法放入队列（定时触发器线程触发）

### 微队列
内部线程api

promise Object.observe MutationObserver

### 执行过程
先执行全局js代码，执行完成之后stack栈会清空

执行微队列

然后执行宏队列的第一个任务，然后执行微队列，循环

执行完毕后，调用栈Stack为空

## nodejs

### 宏队列
timer - setTimeOut setInterval 

io - 除了close的callback setTimeout setInterval  setImmediate

check - setImmediate 

close callback - 

### 微队列
nexttick - process.nextTick(callback)

other - promise

### 执行过程
1. 先执行全局js，清空stack栈

2. 按顺序清空微队列

3. 按顺序执行完一个宏队列

4. 回到2

[事例](https://image-static.segmentfault
.com/690/666/690666428-5ab0a22b5cbca_articlex)


[参考](https://segmentfault.com/a/1190000016278115#item-2-2)
