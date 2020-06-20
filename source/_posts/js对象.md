---
title: js对象
date: 2020-05-18 15:46:55
tags:
  - js
---
## 对象属性类型
### 数据属性
```js
Object.defineProperties(person, {
  name: {},
  age: {}
})
Object.defineProperty(person, 'name',{
  configurable:false,
  writable: false,
  value:'xxx',
  enumerable: false
})
```
### 访问器属性
```js
getter
setter

```

### 原型prototype
每个函数都有一个prototype（原型）属性

每个prototype是一个指针，指向一个对象，即原型对象，原型对象自带constructor属性，函数指针（指向prototype
属性所在的函数）

getPrototypeof  __proto__
```js

```

## 构造函数function


# class
### class表达式
```js
let A = class {
  constructor(x,y){
    this.x = x;
    this.y = y
  }
}

let B = class B2 {
  constructor(x, y){
    this.x = x;
        this.y = y
  }
}
B.name  // 'B2'
```
#### static方法
static方法无需对class实例化，也不能被实例对象调用

### class声明
没有提升，需要先声明再使用，function声明有hosting状态提升
```js
class A{
  constructor(x,y){
    this.x = x;
    this.y = y
  }
}
```
### extends
es5继承是先创建子类对象this，然后再将父类的方法Parent.apply(this)

es6是先创建父类的实例对象this，然后在用子类的构造函数修改this

子类中的super()相当于Parent.prototype.constructor.call(this)


Object.setPrototypeOf()
### new


## Object.create()

