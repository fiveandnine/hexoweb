---
title: webpack-配置
date: 2020-01-15 16:15:47
tags:
    - webpack
---
## 配置
### 配置
[配置](https://www.webpackjs.com/configuration/)

### 多种配置类型
```aidl
module.exports = {
    mode: 'production'
}
```
```aidl
module.exports = (env, argv)=>{
    return {
        mode: env.production,
        plugins: [
            new webpack.optimize.UglifyJsPlugin({
            compress: argv['optimize-minimize'] // 只有传入 -p 或 --optimize-minimize
           })
        ]
    }
}
```
```aidl
module.exports = [{
  output: {
    filename: './dist-amd.js',
    libraryTarget: 'amd'
  },
  entry: './app.js',
  mode: 'production',
}, {
  output: {
    filename: './dist-commonjs.js',
    libraryTarget: 'commonjs'
  },
  entry: './app.js',
  mode: 'production',
}]
```

### 上下文和入口
 - content上下文
 基础路径，绝对路径，从配置中解析入口起点(entry point)和 loader
 webpack 的主目录
 entry 和 module.rules.loader 选项
 相对于此目录解析



### output
```aidl
library  导出库的名称
libraryTarget  导出库的类型 umd


```


## plugin
### clean-webpack-plugin
```
const {CleanWebpackPlugin} = require('clean-webpack-plugin')
```

### html-webpack-plugin
将 webpack中`entry`配置的相关入口thunk  和  `extract-text-webpack-plugin`抽取的css样式   插入到该插件提供的`template`或者`templateContent`配置项指定的内容基础上生成一个html文件，具体插入方式是将样式`link`插入到`head`元素中，`script`插入到`head`或者`body`中。


## loader
文件预处理器，处理静态文件时要使用loader加载各种文件
