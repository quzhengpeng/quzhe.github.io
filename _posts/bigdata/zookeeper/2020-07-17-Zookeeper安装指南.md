---
layout: post
title: Zookeeper安装指南
date: 2020-07-17
categories: bigdata zookeeper
tags: zookeeper 安装指南
permalink: install_zookeeper
published: true
---

## 安装环境

- ubuntu-20.04.3 LTS

- jdk-1.8.0_321

- apache-zookeeper-3.6.3

## 安装 zookeeper

在 [Zookeeper 官网](https://zookeeper.apache.org) 下载所需要版本的 zookeeper 安装包，解压到 `/usr/local` 文件夹中，并在 `~/.bashrc` 中设置环境变量。

```bash
# set zookeeper home
export ZOOKEEPER_HOME=/usr/local/apache-zookeeper
export PATH=$ZOOKEEPER_HOME/bin:$PATH
```

## 修改 zookeeper 配置文件

单机版的使用默认配置就可以。

### zoo.cfg

```conf
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/usr/local/apache-zookeeper/data
clientPort=2181
admin.serverPort=8070
service.1=localhost:2888:3888
```

## 创建 myid

```bash
echo 1 > /usr/local/apache-zookeeper/data/myid
```

## 测试 zookeeper 是否可用

```bash
$ZOOKEEPER_HOME/bin/zkServer.sh start
$ZOOKEEPER_HOME/bin/zkCli.sh -server localhost:2181

ls /
create /foo bar
get /foo
delete /foo
```
