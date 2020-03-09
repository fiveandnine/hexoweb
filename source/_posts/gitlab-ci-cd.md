---
title: gitlab ci/cd
date: 2019-11-23 14:55:34
tags:
---

## runner 安装
```aidl
//centos
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash
sudo yum install gitlab-runner


```
## register runner
```
gitlab-runner register
```

# 服务器免登陆
将用户的`id_rsa.pub`传输到服务器上
其中192.168.20.7为用户机器
```aidl
//用户机器上运行
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.20.7
```

## rsync
```aidl
rsync -r xxx@192.168.20.7:/opt/env/ /opt/env/
```
### 示列
#### 本地传输
```aidl
rsync /opt/ /home/
//将opt下面的所有文件传输到home下
rsync /opt /home/
//将opt文件夹传输到home下
//使用rsync一定要注意的一点是，源路径如果是一个目录的话，带上尾随斜线和不带尾随斜线是不一样的，不带尾随斜线表示的是整个目录包括目录本身，带上尾随斜线表示的是目录中的文件，不包括目录本身。

```
#### 脚本软链接
```aidl
ln -s /opt/zhinanzhen/buildanddeploydocker/neituiDeploy.sh /usr/local/bin
```
#### 服务器到本地
```aidl
rsync -r root@192.168.1.111:/opt /opt
```
#### 本地到服务器
```aidl
rsync -r  /opt root@192.168.1.111:/opt
```
### 参数
```aidl
-r 同步目录时要加上，类似cp时的-r选项
-v 同步时显示一些信息，让我们知道同步的过程
-l 保留软连接
-L 加上该选项后，同步软链接时会把源文件给同步
-p 保持文件的权限属性
-o 保持文件的属主
-g 保持文件的属组
-D 保持设备文件信息
-t 保持文件的时间属性
--delete 删除DEST中SRC没有的文件
--exclude 过滤指定文件，如--exclude “logs”会把文件名包含logs的文件或者目录过滤掉，不同步
-P 显示同步过程，比如速率，比-v更加详细
-u 加上该选项后，如果DEST中的文件比SRC新，则不同步
-z 传输时压缩
-a, --archive 归档模式，表示以递归方式传输文件，并保持所有文件属性，等于-rlptgoD 
-r, --recursive 对子目录以递归模式处理 

-R, --relative 使用相对路径信息 

```
[参考]('https://blog.csdn.net/MatrixGod/article/details/89708070')

## nvm
```aidl
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash
source ~/.bashrc

```
## 卸载
```aidl
yum remove gitlab-runner
```
## 权限
```aidl
chmod 775 /opt/env/ -R
chmod 777 /opt/env/ -R

```

## tag

# Action
[Action](http://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)


```aidl
//20.7 同步223的资源
rsync -r --delete root@192.168.2.223:/opt/gitlab-runner-static/frontend_tob_referral_deps/build/ /opt/userhome/gitlab-runner/frontend_tob_referral_deps/build/


//162 同步223的资源
rsync -r --delete root@192.168.2.223:/opt/gitlab-runner-static/frontend_tob_referral_deps/build/ /home/gitlab-runner/toc_frontend_tob_referral_deps/build/


//更新223资源
rsync -r --delete /home/gitlab-runner/toc_frontend_tob_referral_deps/build/ root@192.168.2.223:/opt/gitlab-runner-static/frontend_tob_referral_deps/build/



```
