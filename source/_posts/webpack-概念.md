---
title: webpack-概念
date: 2020-01-14 21:26:16
tags:
    - webpack
---
# 概念
webpack实质上是静态模块打包器，递归构建一个依赖图谱，其中包含应用程序所需的所有模块，然后将所有模块打包成一个或者多个bundle

- 入口 entry
```aidl
//单个入口
const config = {
    entry: './src/app.js'
}
//多个入口
const config = {
    entry:{
        app: './src/app.js',
        vendors: './src/vendors.js'
    }

}
```
- 输出 output
```aidl
const config = {
    output: {
        filename: [name].js,
        path: '目标输出目录 path 的绝对路径'//__dirname
    }
}
// CDN 和资源 hash 
output: {
  path: "/home/proj/cdn/assets/[hash]",
  publicPath: "http://cdn.example.com/assets/[hash]/"
}
```
- loader
```aidl
const config = {
    module:{
        rules: [
            {
                test: /\.css$/, use: 'css-loader'
            },{
                test: /\.scss$/,use: [
                    loader: 'style-loader',
                    options:{ modules: true }
                ]
            }
        ]
    }
}
```
- 插件 plugin
```aidl
const config = {
    plugins: [
        new webpack.optimize.UglifyJsPlugin(),
        new HtmlWebpackPlugin({template: './src/index.html'})
    ]
}
```

### module.rules
```aidl
module: {
  rules: [
    {
      parse: { requireEnsure: false },//修改解释器
    },{
      oneOf: [/* rules */]// 只使用这些嵌套规则之一
    },{ 
      rules: [ /* rules */ ]// 使用所有这些嵌套规则（合并可用条） 
    },
            
  ]
}
```

### 模块解析
webpack 使用 enhanced-resolve 

### 热更新
hot module replacement




(css-chain)[https://blog.51cto.com/13869008/2161778]
