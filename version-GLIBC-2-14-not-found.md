---
title: version GLIBC_2.14 not found
date: 2017-04-16 15:33:42
tags: linux
---

{% asset_img 1.png %}

## 好吧，人家需要的是'GLIBC_2.14'，先查看一下当前系统glibc的情况：

```bash
[root@localhost build]# strings /lib64/libc.so.6 |grep GLIBC
GLIBC_2.2.5
GLIBC_2.2.6
GLIBC_2.3
GLIBC_2.3.2
GLIBC_2.3.3
GLIBC_2.3.4
GLIBC_2.4
GLIBC_2.5
GLIBC_2.6
GLIBC_2.7
GLIBC_2.8
GLIBC_2.9
GLIBC_2.10
GLIBC_2.11
GLIBC_2.12
GLIBC_PRIVATE
```


> 好吧，确实没有，那简单粗暴，安装一下。

##  glibc下载

> 从http://www.gnu.org/software/libc/ 下载源代码。我下载的版本是2.14，链接地址是http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.gz。

##  安装

> 因为glibc库使用广泛，为了避免污染当前系统环境，最好自定义安装目录，使用时定义一下环境变量就行了。具体步骤如下：

```bash
[root@localhost ~]# tar xvf glibc-2.14.tar.gz
[root@localhost ~]# cd glibc-2.14
[root@localhost glibc-2.14]# mkdir build
[root@localhost glibc-2.14]# cd ./build
[root@localhost build]# ../configure --prefix=/opt/glibc-2.14
[root@localhost build]# make -j4
[root@localhost build]# make install
```
