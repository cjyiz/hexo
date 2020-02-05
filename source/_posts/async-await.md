---
title: async/await
date: 2019-3-21 11:08:42
tags: ES6
categories: Javascript
---
### async简介
`async`英文的意思是异步，是ES2017标准引入的新函数，使得异步操作更加方便。简单说也是Generator语法糖。<!-- more -->
```
var gen=function* (){
  let f1=yield readFile('/etc/a')
  let f2=yield readFile('/etc/b')
  console.log(f1.toString())
  console.log(f2.toString())
}
```
上面是一个Generator函数，将其用async函数来写：
```
var asyncReadFile=async function(){
  let f1=await readFile('/etc/a')
  let f2=swait readFile('/etc/b')
  console.log(f1.toString())
  console.log(f2.toString())
}
```
对比可以看出，`async`函数就是将`Generator`函数的`*`替换成`async`，`yield`替换成`await`。
`async`在`Generator`的基础上做了改进，自带执行器。同时语义化更清晰，最后的返回值是Promise度一项，更加便于后续操作。因此退一步讲，async函数可以看做是由多个异步操作包装成的一个Promise对象，而`await`命令就是内部`then`命令的语法糖。

### 用法
`async`函数返回一个Promise对象，可以直接进行promise操作，见如下函数：
```
async function getStockPriceByName(name){
  let symbol=await getStockSymbol(name)
  let stockPrice=await getStockSymbol(name)
  return stockPrice
}
getStockPriceByName('goog').then(function(result){
  console.log(result)
})
```

### await
正常情况下await命令后是一个Promise对象，如果不是，会被转成一个立即resolve的Promise对象，如果await语句后面的Promise变成reject，整个async函数会中断执行。如果不想async中断，可以在抛出reject的await函数后面添加一个catch方法，处理前面抛出的错误即可。如下例子：
```
async function f(){
  await Promise.reject('出错了').catch(e=>console.log(e))
  return await Promise.resolve('hello world')
}
f().then(v=>console.log(v))
```