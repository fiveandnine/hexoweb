---
title: css相关loader
date: 2020-06-08 22:56:48
tags:
---

## scss-loader
scss ---> css
```js
options: {
          includePaths: ["absolute/path/a", "absolute/path/b"]
        }
```
## autoprefixer-loader废弃，postcss-loader
postcss-loader配置文件postcss.config.js配合使用autoprefixer

## css-loader
解释样式中的url import等

## style-loader
插入js

## extract-text-webpack-plugin
```js
const Extra = new ExtractTextWebpackPlugin({
  filename: 'css/[name].css'
})

Extra.extract({
  use: [],//loader list
  fallback: 'css-loader'
})
```
报错：DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead
   ⬢ webpack: Uncaught exception: Error: Chunk.entrypoints: Use Chunks.groupsIterable and filter by instanceof Entrypoint instead
   ⬢ webpack: Error: Chunk.entrypoints: Use Chunks.groupsIterable and filter by instanceof Entrypoint instead
```js
npm install --save-dev extract-text-webpack-plugin@next
```


## mini-css-extract-plugin
