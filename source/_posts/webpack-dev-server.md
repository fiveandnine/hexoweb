---
title: webpack-dev-server
date: 2019-10-25 16:59:52
tags:
    - webpack
---

小型静态资源服务器和socketio链接的小型运行时程序

### 两种刷新页面的方式
1. iframe     localhost:9000/webpack-dev-server/index.html
2. inline     命令行和NodeJS Api

inline 时会自动把webpack-dev-server客户端加到webpack的入口文件配置中

**注意**：使用webpack-dev-server时会自动查找webpack.config.js的配置文件，否则
```aidl
webpack-dev-server --inline --config webpack.config.dev.js
```
node 调用时需要手动把webpack-dev-server/client?http://localhost:9000
加到配置文件中，因为devserver没有inline：true配置

### 两种模块热替换
1. 命令行  **`--line --hot：HMR前缀的信息由webpack/hot/dev-server模块产生，WDS
前缀的信息由webpack-dev-server客户端产生。？？？？？`**
2. nodejs API 






[refer](https://www.jianshu.com/p/941bfaf13be1)

## 其他问题
```aidl
output: {
  filename: '文件名称',
  path: '文件落地路径（绝对路径）',
  publicPath: '文件路径前缀，如cdn'
}

```

#### webpack-dev-server环境下，path、publicPath、--content-base 区别与联系
path：指定编译目录而已（/build/js/），不能用于html中的js引用。
publicPath：虚拟目录，自动指向path编译目录（/assets/ => 
/build/js/）。html中引用js文件时，必须引用此虚拟路径（但实际上引用的是内存中的文件，既不是/build/js
/也不是/assets/）(包括webpack-dev-server)。
--content-base：必须指向应用根目录（即index.html所在目录），与上面两个配置项毫无关联。

