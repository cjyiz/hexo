---
layout: post
title: vue项目页面刷新方案
date: 2020-09-10 00:15:53
tags: 浏览器
categories: 面试
---
# 方案一：类似于浏览器刷新
  1.location.reload()
  2.this.$router.go(0)
缺点是会出现一瞬间空白

#  方案二：新建空白页面跳转过去再回来
   不会出现一瞬间空白，只是地址栏会快速切换

#  方案三:使用provide/indeject
