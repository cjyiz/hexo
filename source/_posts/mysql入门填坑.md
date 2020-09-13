---
layout: post
title: '''mysql入门填坑'''
date: 2020-09-13 23:34:34
tags: mysql
---
# 一.数据库密码强度导致连接失败
打开mysql命令行工具，输入如下指令，即可。
```
USE mysql
ALERT USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';
FLUSH PRIVILEGES
```