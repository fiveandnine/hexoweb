---
title: babel
date: 2020-06-08 14:18:40
tags:
---
## #babel

### @babel/cli
命令行工具，提供了使用命令行来对js编译

**直接命令行babel运行编译，使用的是全局的@babel/cli，测试babel时可以使用项目安装@babel/cli
然后使用npm命令测试**

### @babel/plugin-transform-xxx
@babel/plugin-transform-arrow-function
@babel/plugin-transform-block-scoping
```js
//.babelrc

{
  plugins[
    '@babel/plugin-transform-arrow-function',
    '@babel/plugin-transform-block-scoping'
  ]
}
```
由于配置麻烦然后使用预设

### @babel/preset-env
预设 插件包
```js
//.babelrc
{
  presets: [
    'env',
    'react',
    'stage0'
  ]
}
```

### @babel/polyfill(7)
垫片，磨平哪个浏览器的兼容
在应用开始的时候引用
```js
import '@babel/polyfill'
// import 'babel-polyfill'
```
设置presets中的useBuiltIns: useage自动按需引用
### @babel/runtime
helperh函数包

### @babel/plugin-transform-runtime
抽离helper函数
指定corejs版本





[](https://segmentfault.com/a/1190000011155061)
[](https://www.jianshu.com/p/cbd48919a0cc)
[](https://segmentfault.com/a/1190000011155061)

[](https://juejin.im/post/5d94bfbf5188256db95589be)
