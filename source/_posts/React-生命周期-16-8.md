---
title: React 生命周期(16.8)
date: 2019-07-19 05:18:11
tags:
---
# React生命周期

生命周期三个阶段
 - mounting
 - upating
 - unmounting

## 旧生命周期

![旧生命周期](https://user-gold-cdn.xitu.io/2019/6/10/16b41956d9dc2dfe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### mounting（6个什么周期函数）
 1. constructor(props)
 加载时调用一次，可以用来设置state等
 2. getDefaultProps()
给props设置默认值，dufaultProps

 3. getInitialState()
给state设置默认值，state，在constructor中使用this.state

 4. componentWillMount()
组件加载时调用一次，以后跟新组件不掉用

 5. render()
组件渲染，创建虚拟dom，调用diff算法，更新dom

 6. componentDidMount()
组件渲染后掉用，只调用一次

### upadting（5个生命周期函数）
 1. componentWillReceiveProps(nextProps)
组件加载时不调用，props改变时调用

 2. shouldCompnentUpdate(nextProps,nextState)
组件接受新的props或者新的state时进行计算，返回true时调用render方法，返回false时不render（不调用render）

 3. componentWillUpdate()
组件加载时不调用，只是在组件跟新时调用，此时可以修改state

 4. render()

 5. componentDidUpdate()
组件加载时不调用，组件更新完成后调用


### unmounting（1个生命周期函数）
 1. componentWillUnmount()
组件渲染之后调用，只调用一次

## 新生命周期
### mounting(4个生命周期函数)
 1. constructor
 设置state
 2. static getDerivedStateFromProps(props, state)
 挂载时调用的最后一个方法，根据初始的props来设置state
 函数return的就是state，
 注意： 我们可以将此代码放在 constructor 中，与之相 getDerivedStateFromProps的优点是它更直观 - 它仅用于设置状态，而构造函数有多种用途。
总结： getDerivedStateFromProps 的最常见用例（在mount期间）：根据初始props返回状态对象。
```
class ScrollingList extends React.Component {
  listRef = React.createRef();

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // 如果在列表中添加新项目
    // 获取列表的当前高度，以便我们稍后调整滚动
    if (prevProps.list.length < this.props.list.length) {
      return this.listRef.current.scrollHeight;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // 如果我们 snapshot 的值不为空，说明添加了新项目
    // 调整滚动，以便这些新项目不会将旧项目推出可视区域
    if (snapshot !== null) {
      this.listRef.current.scrollTop +=
        this.listRef.current.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}
```

 3. render

 4. componentDidMount

###updating（5个生命周期函数）
 1. static getDerivedStateFromPros

 2. shouldComponentUpdate(nextProps, nextState)
 this.prop获取之前的props
 this.state获取之前的state

 3. render

 4. getSnapshotBeforeUpdate(prevProps, prevState)
 返回的参数作为componentDidUpdata的第三个参数

 5. componentDidUpdate(prevProps, prevState, snapshot)

###unmounting（1个生命周期函数）
 1. componentWillUnmount
 清除事件监听、定时器等，防止内存泄漏。

### error Handling（） 
 1. getDerivedStateFromError
不做任何负面作用，只是设置state，返回值就是state，捕获任何地方的js错误

 2. componentDidCatch
只捕获生命周期和render的错误
与 getDerivedStateFromError 区别在于不是为了响应错误而更新状态，可以执行任何副作用，例如记录错误。
```
class ErrorBoundary extends Component {
  state = { errorMessage: null };
  static getDerivedStateFromError(error) {
    return { errorMessage: error.message };
  }
  componentDidCatch(error, info) {
    console.log(error, info);
  }
  render() {
    if (this.state.errorMessage) {
      return <h1>Oops! {this.state.errorMessage}</h1>;
    }
    return this.props.children;
  }
}

```

reference
>[React v16 生命周期函数详解：如何、何时使用它们（React 组件生命周期的修订和最新指南）](https://juejin.im/post/5c9b57d65188251d081cba4a#heading-6)






