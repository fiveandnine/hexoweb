---
title: webpack-API
date: 2020-01-15 19:47:42
tags:
    - webpack
---
# plugin
## compiler钩子
compiler模块通过配置创建一个compilation实例，它扩展至tapable类，以便注册和调用插件

### 监听
compiler支持监听文件系统，在文件修改时重新编译，处于监听模式时，会触发watchRun、watchClose和invalid
等而外的事件，常用于开发环境，常常会在 webpack-dev-server 这些工具的底层之下调用，由此开发人员无须每次都使用手动方式重新编译

### 相关钩子
compiler暴露之后，可以通过
```aidl
compiler.hooks.someHooks.tap()
```
访问相关的生命周期钩子函数
 - done
 
 编译(compilation)完成。
 参数：stats
 - invalid
 
 监听模式下，编译无效时。
 参数：fileName, changeTime
 - fail
 
 编译(compilation)失败。
 参数：error

