---
title: nvm安装nodejs
date: 2017-04-16 13:56:36
tags: linux
---

## 通过NVM安装

> NVM（Node version manager）顾名思义，就是Node.js的版本管理软件，可以轻松的在Node.js各个版本间切换，项目源码GitHub
 
### 1.下载并安装NVM脚本

> curl https://raw.githubusercontent.com/creationix/nvm/v0.13.1/install.sh | bash
source ~/.bash_profile

### 2.列出所需要的版本

nvm list-remote

返回结果如下

```
v0.10.29
v0.10.30
 v0.11.0
 v0.11.1
 v0.11.2
 v0.11.3
 v0.11.4
 v0.11.5
 v0.11.6
 v0.11.7
 v0.11.8
 v0.11.9
v0.11.10
v0.11.11
v0.11.12
v0.11.13
```


### 3.安装相应的版本

```
nvm install v0.10.30
```

### 4.查看已安装的版本

```bash
nvm list
->  v0.10.30
      system
```


### 5.切换版本
```
nvm use v0.10.30
```

### 6.设置默认版本

```bash
nvm alias default v0.10.30
```