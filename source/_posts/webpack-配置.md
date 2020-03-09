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
 - 入口
