---
title: note
date: 2018-06-10 19:40:10
---
#### 免密登陆
***
``` bash
ssh-keygen -t rsa
# 三次回车
ssh-copy-id -i ~/.ssh/id_rsa.pub <远程主机IP>
```
#### Hexo 安装:
***
* 安装 Node.js
``` bash
curl https://raw.github.com/creationix/nvm/master/install.sh | sh
nvm install stable
```
* 安装 git
``` bash
    yum install git
```
* 安装 Hexo
``` bash
nmp install hexo -g     # 全局安装，npm默认为当前项目安装
npm install -g hexo-cli
npm install hexo-server --save
hexo init <directory> # 执行 Hexo 初始化
cd <directory>
npm install
hexo generate          #自动根据当前目录下文件,生成静态网页,可简写：hexo g
hexo server            # 启动 Hexo，简写：hexo s [-i <ip>] [-p <port>]
```
* Hexo 的一些操作
``` bash
hexo new <port> proj1
hexo new draft proj2
hexo new page proj3
```
* 对应关系
``` bash
| 布局  | 路径           |
| ----- | -------------- |
| post  | source/_posts  |
| page  | source         |
| draft | source/_drafts |
```
