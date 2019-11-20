---
title: Promise简介
date: 2018-12-20 13:09:18
tags: Promise,ES6
categories: Javascript
---
### 简介
Promise是异步编程的一种解决方案。语法上来说，Promise是一个对象，里面保存着一些异步操作的结果。
使用Promise对象，可以将异步操作已同步操作的流程表达出来，避免了层层嵌套回调函数。另外Promise对象提供了一些统一的接口，使得异步操作更加容易。


### 特点
Promise对象有两个特点:
1. 对象的状态不受外界影响
2. 一旦状态改变就不会再变。常用的是Resovled(成功状态),Rejected(失败状态)

### 如何使用Promise
ES6中规定，Promise对象是一个构造函数，用来生成Promise实例。
```
var fn=new Promise((resolve,reject)=>{
  if(/*操作成功*/){
    resolve(value)
  }else{
    reject(err)
  }
})
```
上面代码创造了一个Promise实例，构造函数接受了一个函数作为参数，这个函数参数分别为resolve和reject。他们两个是函数，由Javascript引擎提供，不用自己部署。
resolve函数的作用是，在操作成功时调用，并将成功操作的结果作为参数传递出去。
reject函数的作用是，在操作失败时调用，并将失败操作的结果传递出去。

### 方法
1. Promise.prototype.then()
他的作用是为Promise实例添加状态改变时的回调函数。`then(fn1,fn2)`第一个参数是Resolved状态的回调函数，第二个参数是Rejected状态的回调函数。
2. Promise.prototype.catch()
该方法等同于`.then(null,rejection)`，用于指定发生错误时的回调函数。看起来这个方法多此一举，功能被`then()`涵盖了。实际上Promise对象的错误具有冒泡性质，会一直向后传递直到被捕获为止。如果有多个Promise对象的话，可以不在`then()`中定义Rejected状态的回调函数，直接在最后使用catch()方法。这样前面代码任何一个抛出错误都会被捕获。
3. Promise.all()
用于将多个Promise实例包装成一个新的Promise实例。
```
let p=Promise.all([p1,p2,p3])
```
上面这段代码中，p1,p2,p3都是Promise对象的实例。三者只要有一个是Rejected状态，最后p的状态都会变为Rejected。
4. Promise.race()
同all()
5. Promise.resolve()
讲一个对象转换成Promise对象
6. Promise.reject()
返回一个状态为Rejected的新的Promise对象

### 用Promise对象实现AJAX操作
```
<!-- 封装一个XMLHttpRequest对象 -->
var  getJSON=function(url){
  let promise=new Promise((resolve,reject)=>{
    let client=new XMLHttpRequest()
    client.open('get',url)
    client.onreadystatechange=handler
    client.responseType='json'
    client.setRequestHeader('Accept','application/json')
    client.send()
    function handler(){
      if(this.readerState!==4){
        return 
      }if(this.status>=200&&this.status<400){
        resolve(this.response)
      }else{
        reject(new Error(this.statusText))
      }
    }
  })
  return promise
}

getJSON('/posts.json').then((json)=>{
  console.log('Contents:'+json)
}).catch((err)=>{
  console.log(err)
})
```