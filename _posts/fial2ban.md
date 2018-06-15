---
title: fial2ban
date: 2018-06-08 15:32:45
tags: 安全
---

##### 安装：
``` bash
$ yum install epel-release
$ yum install fail2ban
```
##### 配置：

新建配置文件，默认是没有的，也可以定义nginx-cc防护
``` bash
$ vim /etc/fail2ban/jail.d/sshd.local
[sshd]
enabled = true					# 是否启用
filter = sshd					# 过滤表
findtime = 120					# 统计时间范围，单位：秒
bantime = 120					# 封锁时间，单位：秒
maxretry = 3					# 最大错误次数
banaction = iptables-allports
```
##### 运行状态：
![](images/fail2ban.png)
