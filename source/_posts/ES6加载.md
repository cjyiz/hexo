---
title: ES6加载
date: 2018-11-12 16:30:43
tags: ES6
categories: Javascript
---
# 浏览器加载
默认情况下，浏览器时同步加载JS脚本，即渲染器遇到`<script>`标签就会停下来，等执行完脚本，再继续向下渲染。如果是外部脚本，还必须加入脚本下载时间。
如果加载不顺利，会造成浏览器堵塞。因此可以进行异步加载。<!-- more -->
```
<script src=''  defer></script>
<script src='' async>>/script>
```
渲染引擎遇到这一行命令，就会开始下载外部脚本，但不会等他下载完毕和执行，而是执行后面的命令。
 **defer和async的区别**：defer是“渲染完再执行”，async是“下载完就执行”。另外，如果有多个defer脚本，会按照它们在页面出现的顺序加载，而多个async脚本是不能保证加载顺序的。 

## 加载ES6模块
需要加入`type='module'`,浏览器对于这种JS都是异步加载，不会堵塞浏览器。
```
<script type="module" src="./foo.js"></script>
```
值得注意的时，模块之中，顶层的this关键字返回undefined ，并不是指向window。通过这一点，可以侦测当前代码是否在ES6模块之中。
```
const isNotModuleScript=this !== undefined
```
## 循环加载

“循环加载”（circular dependency）指的是，a脚本的执行依赖b脚本，而b脚本的执行又依赖a脚本



##  chrome最新的更新JS已经可以异步加载，不会阻塞加载
