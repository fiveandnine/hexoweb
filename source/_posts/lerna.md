---
title: lerna
date: 2019-11-04 16:23:09
tags:
---
# lerna

## lerna init
### 目录结构
```aidl
//package.json
{
    "workspaces":[
        "packages/*"
    ]
}
//lerna.json
{
    "useWorkspaces": true// 只有顶层有一个node_module
}
```
### --independence
独立模式，允许对每个库单独进行修改版本号
```aidl
//lerna.json
{
  "packages": [
    "packages/*"
  ],
  "version": "independent"
}

```
### --exact



## lerna publish

## lerna add 
```aidl
lerna add shelljs --scope=psc
```

## lerna create
增加子包

# yargs
## argv
```aidl
const yargs = require('yargs')
const argv = yargs.argv      //获取命令行参数
```
## command
command(cmd, describe, [builder], [handler])
```aidl
const args = require('yargs').command('init', 'init offical 
website', {
    'name': {
        alias: 'n',
        default: 'zoomlion'
    },
}).help().argv

//builder 可以是一个函数
const args = require('yargs').command('init', 'init offical 
website', function(){
    return yargs.options('name', {
       demand: true,
       alias: 
    })    
},
}).help().argv
```
### yargs.positional()
描述和配置参数
```aidl
function(yargs){
    return yargs.position('name',{
        describe: 'name describe',
        type: 'type',
        default: 'default name'
    })
}
```
### yargs.option()
配置参数
```aidl
function(yargs){
    return yargs.option('name',{
        alias: 'n',
        default: 'default name',
        
    })
}
```
### yargs.middleware((yargs)=>{})
中间件，可以修改返回的argvs的值

###yargs.pkgConf()
获取package.json中的值

# inquirer
## inquirer.prompt([QuestionObject])
问题列表
返回一个promise
### QuestionObject
```aidl
{
    type: '',//input, number, confirm, list, rawlist, expand, checkbox, password, editor
    name: '',//
    message: ''//
    default: '',//String|Number|Boolean|Array|Function
    choices: '',
    validate: ()=>{}//
}
```


