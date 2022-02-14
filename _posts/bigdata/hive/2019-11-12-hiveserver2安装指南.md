---
layout: post
title: hiveserver2安装指南
date: 2019-11-12
categories: bigdata hive
tags: hive hiveserver2 安装指南
permalink: install_hiveserver2
published: true
---

## 配置 hive-site.xml

```xml
    <property>
        <name>hive.server2.thrift.port</name>
        <value>10000</value>
    </property>
    <property>
        <name>hive.server2.thrift.bind.host</name>
        <value>localhost</value>
    </property>
    <property>
        <name>hive.server2.long.polling.timeout</name>
        <value>5000ms</value>
    </property>
```

## 配置 core-site.xml

```xml
  <property>
    <!-- xxx 是连接 beeline 的用户，将 xxx 替换成自己的用户名即可 -->
    <!-- * 表示可通过超级代理 xxx 操作 hadoop 的用户、用户组和主机 -->
    <name>hadoop.proxyuser.xxx.hosts</name>
    <value>*</value>
  </property>
  <property>
    <name>hadoop.proxyuser.xxx.groups</name>
    <value>*</value>
  </property>
```

## 启动 hiveserver2 服务

```bash
hive --service hiveserver2
```

- 查看端口占用情况

  `netstat -anp | grep 10000`

## 通过 beeline 连接hive

```bash
beeline
!connect jdbc:hive2://localhost:10000

beeline -u jdbc:hive2://localhost:10000 -n username -p passwd
```

## 修改注释乱码

hive 元数据库默认的存储字符集是 latin1 需要修改成utf-8。

### 执行代码

```sql
-- （1）修改表字段注解和表注解
alter table COLUMNS_V2 modify column COMMENT varchar(256) character set utf8；
alter table TABLE_PARAMS modify column PARAM_VALUE varchar(4000) character set utf8；

-- （2）修改分区字段注解
alter table PARTITION_PARAMS modify column PARAM_VALUE varchar(4000) character set utf8;
alter table PARTITION_KEYS modify column PKEY_COMMENT varchar(4000) character set utf8;

-- （3）修改索引注解
alter table INDEX_PARAMS modify column PARAM_VALUE varchar(4000) character set utf8;
```

### 修改 jdbc 连接配置

```xml
<property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://localhost:3306/hive?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8</value>
</property>
```
