---
title: linux
date: 2017-03-19 14:55:13
tags: linux
---

# linux 安装软件后给系统添加一个PATH 环境变量

```bash
vi ~/.bashrc
```

```bash
MONGODB_HOME = /home/admin/Downloads/mongodb
PATH = $PATH:$MONGODB_HOME/bin
```

> 是配置生效

```bash
source ~/.bashrc
```

3. 启动数据库

```
mongod --dbpath $dbpath
--logpath $logpath
--logappend
--fork
```

**脚本启动或者配置文件启动**

> 在mongodb解压后的文件中通过mkdir命令新建 data log 文件夹跟bin目录同级