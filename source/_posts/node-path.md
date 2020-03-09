---
title: node path
date: 2019-12-27 16:29:46
tags:
---

## path.resolve([from...], to)
从后往前，将to解析为绝对路径
```aidl
var path = require("path")     //引入node的path模块

path.resolve('/foo/bar', './baz')   // returns '/foo/bar/baz'
path.resolve('/foo/bar', 'baz')   // returns '/foo/bar/baz'
path.resolve('/foo/bar', '/baz')   // returns '/baz'
path.resolve('/foo/bar', '../baz')   // returns '/foo/baz'
path.resolve('home','/foo/bar', '../baz')   // returns '/foo/baz'
path.resolve('home','./foo/bar', '../baz')   // returns '/home/foo/baz'
path.resolve('home','foo/bar', '../baz')   // returns '/home/foo/baz'
```

## require.resolve()
[require.resolve](https://www.cnblogs.com/joyeecheung/p/3941705.html)
[node](https://github.com/nodejs/node-v0
.x-archive/blob/master/lib/module.js#L321)
