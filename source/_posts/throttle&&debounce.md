---
title: throttle&&debounce
date: 2019-08-10 04:14:08
tags:
---

## 截流throttle
在一段时间内(interval内只执行一次)，无论触发多少次，都只认第一次
```
document.addEventListener(fun)
fun = throttle(fn, interval)
```
```
function throttle(fn, interval){
    let last = 0;
    <!-- 返回一个函数 -->
    return function(){
        let context = this;
        let args = arguments;
        let now = +new Date();
        <!-- 超过时间间隔就执行 -->
        if(now - last > interval){
            last = now;
            fn.apply(context, args)
        }
    }
}
```


## 防抖Debounce
一段时间内，无论触发多少次，只认最后一次;
最后一次触发后的delay后触发回调函数
```
function(fn, delay){
    let timer = null;
    return function(){
        let context = this;
        let args = arguments
        if(timer){
            clearTimeout(timer)
        }
        timer = setTimeout(function(){
            fn.apply(this, args)
        }, delay)
    }
}
```

## throttle&&debounce
```
function td(fn, delay){
    let last = 0;
    let timer = null;
    return function(){
        let context = this;
        let args = arguments;
        let now = +new Date()
        if(now - last < delay){
            clearTimeout(timer)
            timer = setTimeout(function(){
                fn.apply(context, args)
            }, delay)
        }else{
            last = now
            fn.apply(context, args)
        }
    }
}
```