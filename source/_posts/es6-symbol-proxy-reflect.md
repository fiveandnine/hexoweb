---
title: es6-symbol-proxy-reflect
date: 2020-06-15 13:25:58
tags:
  - js
---
## symbol
### Symbol.prototype.description


### Symbol()

### Object.getOwnPropertySymbols()

### Symbol.for()


### Symbol.keyFor()


## 内置对象
### Symbol.hasInstance
foo instanceof Foo === Foo[Symbol.hasInstance](foo)

### Symbol.isConcatSpreadable
concat时是否展开，数组默认展开（此值为undefined），为false时不展开

类数组{0:1,1:2,length: 2}，默认为不展开，true时展开

### Symbol.species

### Symbol.match

'a'.match(myObject) === myObject[Symbol.match]

### Symbol.replace

Sting.property.replace(str, replaceStr) ===
str[Symbol.replace](this, replaceStr)

### Symbol.search

### Symbol.split

...

## Reflect
### Reflect.has(obj, name)
Reflect.has方法对应name in obj里面的in运算符。

### Reflect.deleteProperty(obj, name)
delete obj.nama

### Reflect.construct(Obj, options)
```js
function Person(name){
  this.name = name
}
const p = new Person('xxx')
const p2 = Reflect.construct(Person, 'xxx')
```
