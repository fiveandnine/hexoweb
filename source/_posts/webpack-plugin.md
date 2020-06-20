---
title: webpack-plugin
date: 2020-03-31 10:50:55
tags:
---
## 多页面plugin

1.配置一个模版路径，解析里面所有的html模版
2.配置解析模版的加载器loader, 用于解析模版，在module.loaders中配置同样有效
3.配置exclude等通用配置
4.可以配置模版后缀，用与过滤文件夹下的非文件模版
5.还要提供一套规则来引用生产的css和js


## 插件开发

 - 一个非匿名的js函数
 - 在他的原型上定义apply方法
 - 指明挂在自身的webpack钩子事件
 - 操作webpack内部的特定数据
 - 方法完成时唤起webpack提供的回调
