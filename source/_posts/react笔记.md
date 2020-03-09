---
title: react笔记
date: 2020-02-29 14:17:40
tags:
  - react
---

### 函数组件
```
function Name(props){
  return <div>{props.name}</div>
}
export default Name
```
```aidl
export default (props) => {
  return <div>{props.name}</div>
}
```
1. 性能提升，直接精简成render函数，所以没有实例化过程，不需要分配多余内存
2. 无状态组件
3. 无法访问生命周期函数


**函数组件和类组件最大的不同是捕获渲染值（capture value）**
**function component capture value**

[refer](https://segmentfault.com/a/1190000018660625?utm_source=tag-newest)

## hook
### useState
为什么用use而不是用create，state是组件首次渲染时创建的，下次渲染useState返回
```aidl
let = memoizedState;
function useState(initState){
  memoizedState = memoizedState || initState
  function setState(newValue){
    memoizedState = newValue
  }
  return [ memoizedState, setState ]
}
```

```aidl
let memoizedState = [];
let index = 0;
function useState(initState){
  memoizedState[index] =  memoizedState[index] || initState;
  let current = index
  function setState(newValue){
    memoizedState[current] = newValue
  }
//index = index +1 
//return [memoizedState[ current ], setState ]  
  return [ memoizedState[ index++ ], setState ]
}

```
### useEffect
类似于componentDidMount, componentWillUnmount, 
componentDidUpdate生命周期的函数的执行，异步
```aidl
export default () => {
  const [count, setCount] = useState(0)
  
//useEffect 第二个参数
//如传对应的变量数据,变量更新之后就会调用。  
  useEffect(() => {
//    
  }, [count])
  useEffect(() => {
// 如传空数组, 类似componentDidMount

  }, [])
  useEffect(() => {
    return () => {
//      
    }
  })
}
按顺序执行定义的useEffect

```
### react.Memo
优化渲染，只有当props更新时才会渲染
```aidl
export default React.Memo((props) => {
  return <div>{props.name}</div>
})
```

### useMemo

```aidl
export default (props) => {
  const [list, setList] = useState([{title: '华泰'}]))
  const Childs = useMemo(()=>{ <child list={list}/> }, [list])
  return <div>{Childs}</div>
}
```

### useContext
```aidl
import ctx from '../App.js'
const params = useContext(ctx)
console.log(params)

```

### useRef()

