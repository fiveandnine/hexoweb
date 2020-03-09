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

### centos
```aidl
sudo yum update
yum -y install docker

```
修改docker目录
```aidl
vi /etc/docker/daemon.json

{
  "registry-mirrors": [ 
    "http://hub-mirror.c.163.com", 
    "https://pee6w651.mirror.aliyuncs.com", 
    "https://docker.mirrors.ustc.edu.cn"
  ],
  "insecure-registries":[
    "hub.zhinanzhen.wiki",
    "192.168.1.233:5000"
  ],
    "graph":"/home/docker"
}

```
## build
```aidl
docker build -t xl/nginx:1.0 .
docker images

```
-t 镜象名字及标签 通常 name:tag

## run
```aidl
docker run [options] image [command] [arg...]

docker run -it hub... --rm 
docker run hub... -d(-it) -p 80:80 -v /opt/log:/app/log

docker run --name live214 -d -p 80:80 -v /Users/xiao/Desktop/zhinanzhen/dockerServer/sensetime/nginx.conf:/etc/nginx/nginx.conf live214
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

## 删除none镜像
```aidl
docker rmi $(docker images | grep "none" | awk '{print $3}')
docker rmi $(docker images | grep image-b | grep -v "v1d0-7" | awk  '{print $3}')

docker ps -a | grep "none" | awk "{print $3}" | xargs docker rm


```
## docker保存压缩文件
```aidl
docker save <myimage>:<tag> | gzip > <myimage>_<tag>.tar.gz
gunzip -c <myimage>_<tag>.tar.gz | docker load

```

## Swarm
### 集群
集群是一组协同工作的服务实体，可以理解为服务器，用于提供比单一服务器更具扩展性和可用性的服务平台。
 - 可扩展性
 
 集群不限于单一的服务实体，，新的服务实体可以动态的加入到集群，增强集群的性能
 
 - 高可用性
 
 服务实体冗余，使客户端避免轻易遇到out of service的警告。在集群中，同样的服务可以由多个服务实体提供。如果一个服务实体失败了，另一个服务实体会接管失败的服务实体。集群提供的从一个出错的服务实体恢复到另一个服务实体的功能增强了应用的可用性。

https://blog.csdn.net/anumbrella/article/details/80369913
