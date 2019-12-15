---
title: vue中使用Bus进行通信
date: 2019-12-15 10:20:44
tags: Vue,Bus
categories:  Vue
---
# 简介
Bus是一个简单的总线机制，在状态通信比较少的情况下，使用该方法会非常快捷简便。
总的使用方式就是，在一个地方提交一个事件，另外一个地方监听。

# 如何使用
 ### 首先在资源目录下创建一个`bus.js`文件，文件内容如下：
 ```
 import Vue from 'vue'
 export default new Vue;
 ```

 ### 在需要引入Bus的地方加载`bus.js`文件：
 ```
 import Bus from "../utils/bus.js"
 ```
 ### 触发事件：
 Bus.$emit('事件名','传递参数')

 ### 监听事件：
 ```
 Bus.$on('事件名',e=>{
  // 这里e是接收触发事件那里传递过来的参数，没有类型限制
  console.log(e)
 })
 ```