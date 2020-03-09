---
title: React webpack
date: 2019-07-19 05:16:58
tags:
   - webpack
   - react
---
# create react app
## create-react-app
### createReactApp
node执行包安装的流程，并把文件模版拷贝到对应目录下
 - 判断node版本 create-react-app/index
 - 命令行初始化，help帮助提示
 - 判断用户输入参数是否合法
 - 创建package.json
 - 使用某个版本的react-script执行安装依赖
 - 安装完之后跑 react-scripts/script/init.js 修改 package.json 的依赖版本，运行脚本，并拷贝对应的模板到目录里。
 
### init
修改package.json，执行安装，拷贝模版

[模版](https://github.com/facebook/create-react-app/blob/master/packages/cra-template/template/README.md)

## react-scripts/

### react-scripts/index.js


### start.js

### env.js
设置环境变量，
 - dotenv-expand
 - dotenv





ref:
 
[create-react-app 源码解析](https://jsonz1993.github
.io/2018/05/create-react-app-o/#%E9%A1%B9%E7%9B%AE%E5%88%9D%E5%A7%8B%E5%8C%96)
[create-react-app 源码解析之react-scripts](https://juejin.im/post/5af98aaf518825426d2d4142)
