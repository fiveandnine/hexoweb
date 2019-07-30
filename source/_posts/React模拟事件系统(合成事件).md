---
title: React模拟事件系统(合成事件)
date: 2019-07-19 03:53:56
tags:
---
## react合成事件和原生事件
react合成事件：并不将事件直接绑定到dom元素上，而是采用事件冒泡到dom上，然后把事件封装给正式的函数运行和处理(中间层SyntheticEvent)。
 1. 当用户在为onClick添加函数时，React并没有将Click时间绑定在DOM上面。
 2. 而是在document上监听所有的支持事件，当事件发生并冒泡至document处时，React将事件内容封装交给中间层SyntheticEvent（负责所有事件合成）
 3. 所以当事件触发的时候，对使用统一的分发函数dispatchEvent将指定函数执行。

注意
原生事件先于合成事件
e.stopPropagation()会组织合成事件

## React事件机制
 1. 事件机制分为事件注册和事件分发
 2. 事件注册，所有的事件都会注册到document上，拥有统一的回调函数，dispatchEvent来执行事件分发
 3. 事件分发，首先生成合成事件，同一个事件类型只能生成一个合成事件Event




## 其他
 1. 显示的e.preventDefault()阻止默认行为
 2. class 所以要手动bind(this)


>(React合成事件和DOM原生事件混用须知)[https://juejin.im/post/59db6e7af265da431f4a02ef]