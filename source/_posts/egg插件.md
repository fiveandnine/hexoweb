---
title: egg插件
date: 2020-04-23 16:35:42
tags:
  - egg
  - Node
---
## 插件
### 中间件 插件 应用的关系
插件是迷你应用，没有路由router和控制器controller
插件包含service、中间件、配置等
插件没有 plugin.js，只能声明跟其他插件的依赖，而不能决定其他插件的开启与否。
