---
layout: post
title: commitizen指南
date: 2020-06-30
categories: programming node.js
tags: git commitizen
permalink:
published: true
---

## 安装 node.js

到 [node.js](https://nodejs.org/en/) 官网下载所需要的安装包，这里下载的是 16.14.0 LTS。

```bash
sudo apt-get install xz-utils
xz -d node-v16.14.0-linux-x64.tar.xz
tar xvf node-v16.14.0-linux-x64.tar
```

## 设置环境变量

```bash
# set node home.
export NODE_HOME=/usr/local/node
export NODE_PATH=$NODE_HOME/lib/node_modules
export PATH=$NODE_HOME/bin:$PATH
```

## 安装 commitizen

```bash
npm install -g commitizen

# 生成 package.json 文件
npm init --yes
commitizen init cz-conventional-changelog --save --save-exact
```

## 使用 commitizen

### feat

A new feature

### fix

A bug fix

### docs

Documentation only changes

### style

Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)

### refactor

A code change that neither fixes a bug nor adds a feature

### perf

A code change that improves performance

### test

Adding missing tests or correcting existing tests

### build

Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)

### ci

Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)


### chore

Other changes that don't modify src or test files

### revent

Reverts a previous commit
