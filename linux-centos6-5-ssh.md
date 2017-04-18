---
title: linux-centos6.5-ssh
date: 2017-04-16 12:13:29
tags: linux
---


## linux-centos6.5之ssh配置

查询\安装SSH服务

#rpm -qa |grep ssh 检查是否装了SSH包

#yum install openssh-server 没有的话，安装SSH服务

#chkconfig --list sshd 检查SSHD是否在本运行级别下设置为开机启动

#chkconfig --level 2345 sshd on  如果没设置启动就设置下

#service sshd restart  重新启动SSHD

#netstat -antp |grep sshd  看看是否启动了22端口，需要确认下

#iptables -nL  看看是否放行了22口

#iptables -I INPUT -p tcp --dport 22 -j ACCEPT 没有的话放行22端口

#iptables save 保存防火墙规则

# vi /etc/ssh/sshd_config　 

用vi打开SSH的配置文件，在这里我们先保持默认（允许普通用户通过口令登录）

#useradd lhc    添加普通用户（lhc）

#passwd lhc     修改lhc密码

 

 

下载安装超级终端

链接：http://pan.baidu.com/s/1c2mbJBq 密码：awlc

安装成功后，启动应用——>新建连接

输入无误的话，应该就可以成功登陆了。

通过sftp上传下载

# 下载包路径
/usr/local/src
