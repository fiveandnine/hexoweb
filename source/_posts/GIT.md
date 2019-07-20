---
title: GIT
date: 2019-07-20 08:03:21
tags:
---
# 相关操作
##同步删除分支
git remote prune origin

## 放弃本地修改，强制拉取更新
git checkout . && git clean -xdf
git reset --hard
```
git fetch --all
git reset --hard origin/master
git pull //可以省略
```

## 生成 ssh key：
ssh 登录开发服务器 192.168.1.139，用户名为各位的邮箱前缀，密码统一为 123456，使用下面的命令生成ssh key：
```
ssh-keygen
cat ~/.ssh/id_rsa.pub
```

## 修改历史记录
```
git reset [hash]
git add . && git commit -m "sss" && git push -f
```

## fetch


# 相关问题
# fork

```
git remote add upstream https://github.com/zhipenglin/tob_mobile_demo.git

git fetch upstream
git checkout master
git merge upstream/master

git push origin master
```


