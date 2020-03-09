---
title: webpack-tapable
date: 2020-01-13 16:32:58
tags:
    - webpack
---
## webpack设计模式
插件架构 tapable

### tapable
事件发布订阅插件，支持同步和异步，在需要使用的类上继承tapable，并且该类的构造函数中使用this.hooks添加事件名称。
```aidl
this.hooks = {
    accelerate: new SyncHook(["newSpeed"]),
    break: new SyncHook(),
    calculateRoutes: new AsyncParallelHook(["source", "target", "routesList"]
}
```
### 订阅

### 发布

## webpack插件架构
从配置初始化到build完成   一个生命后期

在这个生命周期中的每个阶段定义一些完成不同功能功能的含义

webpack流程就是定义了一个规范，所有插件遵循这个规范完成构建

webpack主要是使用compiler和compilation类来控制整个生命周期，定义执行流程

webpack内部有一堆plugin，内部plugin是webpack
打包构建过程中的功能实现，订阅感兴趣的是事件，在执行流程中调用不同的订阅函数就构成了webpack的完整生命周期

ref: 
[tapable模型](https://segmentfault.com/a/1190000020360490)
