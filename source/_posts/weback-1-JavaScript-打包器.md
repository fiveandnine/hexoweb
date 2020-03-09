---
title: weback-1-JavaScript 打包器
date: 2019-12-27 16:13:31
tags:
    - webpack
---

## JS打包

- 解析入口文件，获取所有的依赖项
```aidl
// 模块
'src/entry': {
  code: '', // 文件解析后内容
  dependencies: ["./message.js"], // 依赖项
}

```
- 递归解析所有的依赖项，生成依赖关系图
```aidl
// graph 依赖关系图
let graph = {
  // entry 模块
  "src/entry.js": {
    code: '',
    dependencies: ["./src/message.js"],
    mapping:{
      "./message.js": "src/message.js"       
    }
  },
  // message 模块
  "src/message.js": {
    code: '',
    dependencies: [],
    mapping:{},
  }
}

```
- 使用依赖图，返回一个可以在浏览器运行的js
 立即执行函数IIFE
```aidl
(function(man){
    function(name){
        console.log(name)
    }
})({name: 'xxx'})
```
- 输出到dist/bundle.js

fs.writeFile 写入 dist/bundle.js 即可。


## 解析入口文件，遍历所有依赖项
@babel/parser解析入口文件，获取AST
```aidl
/**
 * 解析文件内容及其依赖，
 * 期望返回：
 *      dependencies: 文件依赖模块
 *      code: 文件解析内容 
 * @param {string} filename 文件路径
 */
function createAsset(filename) {
  // 读取文件内容
  const content = fs.readFileSync(filename, 'utf-8')
  // 使用 @babel/parser（JavaScript解析器）解析代码，生成 ast（抽象语法树）
  const ast = babelParser.parse(content, {
    sourceType: "module"
  })

  // 从 ast 中获取所有依赖模块（import），并放入 dependencies 中
  const dependencies = []
  traverse(ast, {
    // 遍历所有的 import 模块，并将相对路径放入 dependencies
    ImportDeclaration: ({
      node
    }) => {
      dependencies.push(node.source.value)
    }
  })
  // 获取文件内容
  const {
    code
  } = transformFromAst(ast, null, {
    presets: ['@babel/preset-env'],
  })
  // 返回结果
  return {
    dependencies,
    code,
  }
}

```
## 递归解析所有依赖项，生成一个依赖关系图
```aidl
//获取入口文件
const mainAssert = createAsset(entry)
//解析文件内容及其依赖
function createAsset(filename){
    const content = fs.readFileSync(filename,'utf-8')
    const ast = babelParser.parse(content, {
        sourceType: "module"
    })
    const dependencies = []
    traverse(ast, {
        // 遍历所有的 import 模块，并将相对路径放入 dependencies
        ImportDeclaration: ({
          node
        }) => {
          dependencies.push(node.source.value)
        }
    })
    // 获取文件内容
    const {
        code
    } = transformFromAst(ast, null, {
        presets: ['@babel/preset-env'],
    })
    // 返回结果
    return {
        dependencies,
        code,
    }
}
//创建依赖关系图
const graph = {
    [entry]: mainAssert
}
//递归所有依赖
function createGraph(entry) {
  // 从入口文件开始，解析每一个依赖资源，并将其一次放入队列中
  const mainAssert = createAsset(entry)
  const queue = {
    [entry]: mainAssert
  }

  /**
   * 递归遍历，获取所有的依赖
   * @param {*} assert 入口文件
   */
  function recursionDep(filename, assert) {
    // 跟踪所有依赖文件（模块唯一标识符）
    assert.mapping = {}
    // 由于所有依赖模块的 import 路径为相对路径，所以获取当前绝对路径
    const dirname = path.dirname(filename)
    assert.dependencies.forEach(relativePath => {
      // 获取绝对路径，以便于 createAsset 读取文件
      const absolutePath = path.join(dirname, relativePath)
      // 与当前 assert 关联
      assert.mapping[relativePath] = absolutePath
      // 依赖文件没有加入到依赖图中，才让其加入，避免模块重复打包
      if (!queue[absolutePath]) {
        // 获取依赖模块内容
        const child = createAsset(absolutePath)
        // 将依赖放入 queue，以便于 for 继续解析依赖资源的依赖，直到所有依赖解析完成，这就构成了一个从入口文件开始的依赖图
        queue[absolutePath] = child
        if (child.dependencies.length > 0) {
          // 继续递归
          recursionDep(absolutePath, child)
        }
      }
    })
  }

  // 遍历 queue，获取每一个 asset 及其所以依赖模块并将其加入到队列中，直至所有依赖模块遍历完成
  for (let filename in queue) {
    let assert = queue[filename]
    recursionDep(filename, assert)
  }
  // 返回依赖图
  return queue
}
```
## 使用依赖图，返回浏览器可以运行的js文件



[参考](https://juejin.im/post/5e04c935e51d4557ea02c097#heading-14)
[github](https://github.com/sisterAn/minipack/blob/master/index.js)
