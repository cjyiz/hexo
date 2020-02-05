---
title: ES6模块化语法
date: 2019-11-18 13:22:14
tags: ES6
categories: Javascript
---
## 概述
在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。
ES6模块设计思路是尽量静态化，这样在编译时就能确定模块的依赖关系，以及输入输出的变量。<!-- more -->
### CommonJS模块
```
let {stat,exists,readFile}=require('fs')
<!-- 等同于 -->
let _fs=require('fs')
let stat=_fs.stat
let exists=_fs.exists
let readfile=_fs.readfile
```
commonJs使用运行时加载方案，先整体加载模块，然后再运行时读取需要的方法。同事commonJs模块就是对象，输入时必须查找对象属性。
### ES6模块
ES6模块不是对象，而是通过`export`命令显示指定输出的代码，再通过`import`命令输入。
ES6模块在代码编译时加载属于静态加载。
```
<!-- ES模块 -->
import{stat,exist,readFile} from 'fs
```

## 主要命令
ES6模块功能主要由`export`和`import`命令构成
### `export`命令
用于规定模块的对外接口，整个模块是一个独立的文件。该文件内部的所有变量外部都无法获取。
想要外部能够读取模块内部内容，必须使用`export`关键字输出该变量。
```
export var firstName='JSON'
export var lastName='Lucy'
export var year=1998
<!-- 可以写成如下 -->
var firstName='Michael'
var lastName='Lucy'
var year=1998
export {firstName,lastName,year}
```
`export`命令除了输出变量，还可以输出函数或者类。
```
export function multiply(x,y){
  return x*y
}
```
`export`语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以获取到模块内部实时的值。
### `export default`命令
为了方便用户的读取，使用`export default`命令为模块指定默认输出。
本质上，`export default`就是输出一个叫做`default`的变量或方法，然后系统允许你为它取任意名字。
## import命令
使用`export`命令定义了模块的对外接口后，其他JS文件就可以通过`import`命令加载这个模块。
```
import {firstName,lastName,year} from './profile.js'
function setName(element){
  element.textContent=firstName+' '+lastName
}
```
使用`as`关键字，可以将输入的变量换一个名字，见如下代码：
```
import {lastName as surname} from './profile.js
```
`import`输入的变量都是制度的，不允许修改。
`import`后面的from指定引用文件路径。
`import`命令在编辑阶段，在代码运行前静态执行。不能使用表达式和变量。
### `export`和`import`何用
如果一个模块先输入后输出同一个模块，可以这样子写：
```
export {foo,bar} from 'cc'
<!-- 等价于 -->
import {foo,bar} from 'cc'
export {foo,bar}
```
### `import()`函数
由于import命令是在代码运行前静态执行的。有些情况下，我们需要按需加载，在此引入了`import()`函数。
```
if(condition){
  import('cc').then(
    <!-- 模块加载成功后，这个模块会作为一个对象，当作then方法的参数 -->
    ({export1,export2})=>{
       console.log(export1)
  })
}
```

