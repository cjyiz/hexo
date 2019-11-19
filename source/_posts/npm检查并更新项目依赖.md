---
title: npm检查并更新项目依赖
date: 2019-11-19 13:51:00
tags: npm
categories: 工程化
---
## 前言
安装新项目时，经常遇到`package.json`中的依赖版本过低导致项目无法启动的状况。因此我们可以使用`npm-check-updates`插件来进行更新依赖。
## 使用方法
```
<!-- 安装插件 -->
npm install npm-check-updates -g

<!-- 检查当前目录下可更新的依赖项 -->
ncu

<!-- 升级package.json中引用依赖的版本 -->
ncu -u

<!-- 更据更新后的package.json升级依赖 -->
npm install
```

##  依赖地址
[https://acme.top/nodejs-npm-check-updates](https://acme.top/nodejs-npm-check-updates)