---
title: vue笔记
date: 2019-10-23 14:39:57
tags:
---

##
### 指令
 - v-text
 - v-html
 - v-bind
 - v-on
 - v-model
 - v-for
   (item, key, index) in items
    <!-- item 为值，key 为键，index 为索引 -->
 - v-bind:class
 ```aidl
    <div v-bind:class="{ active: true }"></div> ===> 解析后
    <div class="active"></div>

```
 - v-if
 - v-show
 - v-pre
    Mustache 标签
 - v-once

### 过滤器
 #### 全局过滤器
  
 #### 局部过滤器 

### 按键值修饰符
### 监听数据变化 watch
 键是监听的需要观察的表达式
 值是对应的回调函数
 
 ### 计算属性
 computed
 
 ### 组件的生命周期
 - beforeCreate()
 ----
 实力初始化之后，数据观测和event/watch之前
 因此无法获取data中的数据、methods中的方法
 - created()
 ----
 可以调用method中的方法，改变data中的数据
 - beforeMounted()
 ----
 挂在开始之前被调用
 - mounted()
 ----
 此时，vue实例已经挂载到页面中，可以获取到el中的DOM元素，进行DOM操作
 - beforeUpdated()
 ----
 说明：数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。
 
 注意：此处获取的数据是更新后的数据，但是获取页面中的DOM元素是更新之前的
 - updated()
 
 - beforeDestroy()
 
 - destroyed()

### 自定义指令

### 组件

### 组件通信
```aidl
$on
$emit

```

### 获取组件
 - `vm.$refs`,持有已注册过 ref 的所有子组件（或HTML元素）
 - 在 HTML元素 中，添加ref属性，然后在JS中通过`vm.$refs.属性`来获取
 - 如果获取的是一个子组件，那么通过ref就能获取到子组件中的data和methods
