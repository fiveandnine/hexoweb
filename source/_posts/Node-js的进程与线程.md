---
title: Node.js的进程与线程
date: 2019-08-10 07:30:24
tags:
    - Node
---

## 进程process
是计算机程序在某一数据集合上的一次运行活动 是计算机进行资源分配和调度的基本单位
进程是线程的容器。
```aidl
//node进程
const http = require('http')
const server = http.createServer()

server.listen(3000, () => {
    process.title = 'node 进程'
    console.log('进程id',process.pid)
})

```


## 线程
线程隶属于进程，一个进程可以有多个线程
一个线程只能属于一个进程

*单线程：一个进程只开一个线程*

Javascript 就是属于单线程，程序顺序执行
```aidl
//线程阻塞
const http = require('http')
const server = http.createServer()
//耗时操作
function longComputation(){
//    
}
server.on('request', (req, res) =>{
    if(req.url === '/'){
        console.info('计算开始',new Date());
        const sum = longComputation();
        console.info('计算结束',new Date());
        return res.end(`Sum is ${sum}`);
    }eles{
        res.end('ok')
    }
})
server.listen(3000)

```
----
## nodejs的进程
nodejs是js在服务端的运行环境，构建在v8引擎上，基于事件驱动，非阻塞io模型，
充分操作系统提供的异步io进行多任务执行，适应io密集型场景，因为异步，程序无需阻塞等待结果返回，
而是基于回调通知的机制，原本同步模式等待的时间，则可以用来处理其它任务

### 异步io
做io操作时不会阻塞process

### 同步io
做io操作的时候会阻塞process，所以阻塞io，非阻塞io，io多路复用i/o都是同步io

### 非阻塞io && 阻塞io
阻塞io：当用户发一个读取文件描述符的操作的时候，进程就会阻塞，直到读取数据完全准备好之后返回给用户，block状态才会接触
非阻塞io：当用户发出读取文件描述符操作的时候，函数直接返回给用户，不做任何等待，进程继续执行，后续轮询
（非阻塞io都不阻塞process为什么还是同步io：当数据准备好之后还是需要阻塞进程去内核中拿数据）

### 事件驱动
当收到请求时，请求会被压入队列，通过循环来检测队列中的时间变化

nodejs是单线程，通过一个事件循环（event-loop）取出消息队列（event-queue
）中的消息进行处理，处理基本上是对应的回调函数，消息队列就是当事件状态改变时，将一个消息压入队列
 - 因为是单线程的，所以在顺序执行js的时候，事件循环是暂停的
 - 当js执行结束之后，事件循环开始，从队列中取出消息进行执行
 - 执行的时候事件循环暂停
 - 当涉及io操作的时候，nodejs会开一个独立的线程进行io操作，操作结束后将消息压入消息队列
 
 压入事件队列的方法 setTimeout() process.nextTick() setImmediate()
 
 参考：(https://segmentfault.com/a/1190000005173218)
 [https://segmentfault.com/a/1190000005173218]

### 线程驱动
当收到请求是，会新开一个线程去处理请求，就有线程池以及线程池满了之后的队列
 ------
### process模块
node内置模块
process.title
process.pid
process.ppid
process.env
process.nextTick
process.cwd()  当前项目工作目录
process.plantform
process.on('uncatchedExpection', () =>{}) process.on
('exit', () =>{}) 事件监听
三个标准流：process.stdout 标准输出、process.stdin 标准输入、process.stderr 标准错误输出

### child_process模块
child_process.spawn()
child_process.exec()
child_process.execFile()
child_process.fork() 衍生新的进程
```aidl
//fork衍生子进程
const http = require('http')
const fork = require('child_process).fork

const server = http.createServer((req, res) => {
    if(req.url === 'compute'){
        const compute = fork('./compute.js)
        compute.send('开启一个新的子进程')
        compute.on('message', (sum) => {
            res.end(`Sum is ${sum}`);
            compute.kill();
        })
        compute.on('close', (code, signal)=>{
            console.log(`收到close事件，子进程收到信号 ${signal} 而终止，退出码 ${code}`);
            compute.kill();
        })
    }else{
        res.end('ok')
    }    
})

```
```aidl
//compute.js
function compute (){
//耗时通道
}
proess.on('message',(msg)=>{
    console.log(msg, 'process.pid', process.pid)
    const computeResult = compute()
    process.send('computeResult')
})
```
### cluster模块
集群有两种方案
 - 多个node加多个端口
    集群中的node各自监听不同的端口，再由反向代理实现请求到多个端口的转发
    优点：实现简单，实例相对稳定，对服务稳定性有好处
    缺点：各进程中通信困难，端口占用
 - 主进程向子进程转发请求（cluster）
    集群内创建一个主进程master，以及若干个子进程worker，master监听用户端请求，并根据策略转发给子worker
    优点：通常只占用一个端口，通信相对简单，转发策略更灵活。
    缺点：实现相对复杂，对主进程的稳定性要求较高。
```aidl
const cluster = require('cluster')
const cpus = require('os').cpus().length
const http = require('http')
if(process.isMaster){
    for(let i =0; i ++; i<cpus){
        cluster.fork()
    }
}else{
    http.createServer((req, res)=>{
        res.end(`response from worker ${process.pid}`);
    }).listen(8000)
    console.log(`Worker ${process.pid} started`);
}
```
#### cluster原理
1. master和worker之间的通信
    cluster内部是使用child_process.fork()实现的
    父子进程，通过ipc
2. 多个server如何实现监听同一个端口
    net模块中，对 listen() 方法进行了特殊处理
    master进程正常监听端口
    worker进程创建server实例，通过ipc通道向master发送消息，让master也创建server实例，并在端口上监听请求
    
3. master如何将多个客户端请求分发到worker实例
    worker创建server实例来监听请求之后都通过ipc会在master上注册，master进行分发请求
    具体转发给哪个worker，由转发策略决定
    可以通过NODE_CLUSTER_SCHED_POLICY设置，也可以通过cluster.setupMaster
    (options)传入，默认是SCHED_RR(轮询)
    当有客户请求到达，master会轮询一遍worker列表，找到第一个空闲的worker，然后将该请求转发给该worker。

### Nodejs内部通信原理
ipc inter-process-communication 进程内部通信，node是基于libuv，message和send方法
父进程创建子进程时先创建ipc通道
#### 内部通信
```aidl
const msg = {
    cmd: 'NODE_CLUSTER',
    act: 'queryServer'
}
process.send(msg)

//master伪代码
worker.process.on('internalMessage', fn);

```

cluster内部使用负载均衡平衡各进程的压力，使用round-robin算法



(https://juejin.im/post/5c4317d2518825254e4d388e)[https://juejin.im/post/5c4317d2518825254e4d388e]
