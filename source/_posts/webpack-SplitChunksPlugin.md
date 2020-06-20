---
title: webpack-SplitChunksPlugin
date: 2020-04-07 20:49:40
tags:
  - webpack
---
## splitChunk插件配置项
#### chunks
表示哪些代码需要优化，initial（初始块）async（按需加载块，默认）all
（全部）
#### minSize
形成一个新代码块最小的体积
#### minChunks
默认为1，分割之前这个代码块最小被引用的次数（保证代码的复用，默认配置不需要多次应用也可以被分割）
#### maxInitialRequests
一个入口最大的并行请求数，默认3
#### maxAsyncRequests
按需加载最大的并行请求数，默认5

#### 缓存组test
用于哪些模块被缓存组匹配到，原封不动传递出去的话，默认选择所有模块，可以传regexp，string，function
#### name
打包的chunk名字，字符串或者函数
#### priority
缓存组打包的先后顺序

```
optimization:{
  splitChunks:{
    chunks: "all",
    minSize: 30000,   // （默认值：30000）块的最小大小
    minChunks: 1,
    maxAsyncRequests: 5,
    maxInitialRequests: 3,
    automaticNameDelimiter: '~',
    name: true,
    cacheGroups: { 
      commons: {
        chunks: "initial",
        minChunks: 2,
        maxInitialRequests: 5, // The default limit is too small to showcase the effect
        minSize: 0 // This is example is too small to create commons chunks
      },
      react: {
        test: /react/,
        chunks: "initial",
        name: "react",
        priority: 11,
        enforce: true
      },
      vendors: {
        test: /node_modules/,
        chunks: "initial",
        name: "vendor",
        priority: 10,
        enforce: true
      },
  }
}
```





[refer](https://juejin.im/post/5b99b9cd6fb9a05cff32007a)
[refer](https://juejin.im/post/5b6a4d71f265da0fa8676814)
[refer](https://www.jianshu.com/p/2cc8457f1a10)
