---
title: xtrabackup
date: 2018-06-10 17:24:42
tags: data
---
#### 安装:
``` bash
$ yum install http://www.percona.com/downloads/percona-release/redhat/0.1-4/percona-release-0.1-4.noarch.rpm
$ yum list | grep percona
$ yum install percona-xtrabackup-24
```
#### 创建备份用户:
``` bash
mysql> CREATE USER 'bkpuser'@'localhost' IDENTIFIED BY 'passwd';
mysql> GRANT RELOAD, LOCK TABLES, PROCESS, REPLICATION CLIENT ON *.* TO 'bkpuser'@'localhost';
mysql> FLUSH PRIVILEGES;
```
#### 简单操作:
``` bash
# 创建存放目录
$ mkdir -pv /data/bkp
# 创建完全备份
$ xtrabackup --defaults-file=/etc/my.cnf \   # 指定数据库配置文件
--backup
--user=bkpuser \                             # 指定之前创建的备份用户
--password=passwd \                          # 用户密码
--target-dir=/data/bkp                       # 指定备份存放目录

$ innobackupex  --defaults-file=/etc/my.cnf \
--user=bkpuser \
--password=passwd /data1/bkp

```
两种备份的区别：
[root@localhost ~]# ls /data1/bkp/
2018-06-10_13-40-01
[root@localhost ~]# ls /data/bkp/
backup-my.cnf  ib_buffer_pool  mysql               sys                     xtrabackup_checkpoints  xtrabackup_logfile
db1            ibdata1         performance_schema  xtrabackup_binlog_info  xtrabackup_info

*在备份时可以看到整个备份过程:*
* 连接数据库
* 开始拷贝redo log
* 拷贝innodb表文件
* 锁表、拷贝非innodb表文件
* 停止拷贝redo log
* 解锁

*安装 xtrabackup 提示 /etc/my.cnf 冲突解决办法:*
###### 这里是 mysql 5.7 的版本，其它没有测试
``` bash
yum install mysql-community-libs-compat
```
