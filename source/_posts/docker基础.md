---
title: docker基础
date: 2019-09-18 14:16:04
tags:
---

## 安装
```aidl
brew cask install docker
docker info
docker version

```
brew安装
```aidl
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```
[brew](https://www.jianshu.com/p/ab50ea8b13d6)

## build
```aidl
docker build -t xl/nginx:1.0 .
docker images

```
-t 镜象名字及标签 通常 name:tag

## run
```aidl
docker run [options] image [command] [arg...]

```
options:
-d 后台运行 返回id
-i 交互形式 和-t同时使用
-p 端口映射 主机端口:容器端口
-t 为容器重新分配一个伪输入终端，通常与 -i 同时使用
--name="xlnginx" 容器名称
-e username="xl" 设置环境变量
--env-file=[] 指定文件读入环境变量
-v 绑定一个卷
