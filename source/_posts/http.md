---
title: http
date: 2020-06-16 17:21:51
tags:
---
# http
## http 报文结构
请求报文
```
GET / http/1.1
casch-control:
cookie:xxx

```
相应报文
```
http/1.1 200 OK

```
空行区分头部和实体

## get post区别
 - 传参方式不同，敏感信息应该用post
 - 缓存方面get会被浏览器主动缓存，而post不会
 - get只接受ascii码，而post没有限制
 - get会一次性发出，post会分两次发出
 
## accept
accept:application/json         content-type

accept-encoding:gzip            content-encoding
accept-Language:en              content-language
accept-charest:charest=utf-8    content-type

## http定长不定长
content-length:8
transfer-length: chunked(忽略content-length)

## http 大文件上传
范围请求 Content-Range返回

## http表单提交
### accept:application/x-www-form-urlencoded
编码成已&分割的键值对
```
{a: 1, b:2} ==> a=1&b=2 ==> encodeURIComponent
```
### multipart/form-data
请求头中的Content-Type字段会包含boundary

数据会分为多个部分，每两个部分之间通过分隔符来分隔

## http队头阻塞
并发链接和域名分片

## cookie
httponly

secure https only

sameSite strict, lax, none 

问题： 安全性能和容量

## http代理
作用
 - 负载均衡
 - 安全，过滤非法域名什么的
 - 缓存

via

x-forwarded-for

X-Real-IP

## http缓存
强缓存

协议缓存

代理缓存
cache-control
 - public
 
 指出服务器缓存
 - private
 
 不支持服务器缓存
 - must-revalidate
 
 客户端缓存过期就去源服务器获取
 - proxy-revalidata
 
 客户端缓存过期就去代理服务器取
 - s-maxage
 ```
Cache-Control: public, max-age=1000, s-maxage=2000
```
 - only-if-cached
 
   这个字段加上后表示客户端只会接受代理缓存，而不会接受源服务器的响应。如果代理缓存无效，则直接返回504（Gateway Timeout）。
 
## 跨域
 - cors
 - jsonp
 - nginx
 
 
 
 
 [](https://juejin.im/post/5e76bd516fb9a07cce750746)
 [](https://zhuanlan.zhihu.com/p/86426969)
```js
 exports.createServer = function(requestListener) {
   return new Server(requestListener);
 };

```
