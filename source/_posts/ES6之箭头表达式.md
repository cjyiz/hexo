---
title: ES6之箭头表达式
date: 2018-11-08 16:05:27
tags: ES6
categories: Javascript
---

### 基本用法
  ES6允许使用'箭头（`=>`)'定义函数
**例一**：
```
var f = v => v;
//等同于
 var f = function (v) {
     return v;
 };
```
-----
**例二**：如果箭头函数不需要参数或者需要多个参数，就是用一个圆括号代表参数部分。
```
var f = () => 5;
//等同于
var f = function () {return 5 } ;

var sum = (num1,num2)=> num1 +num2;
//等同于
var sum = function(num1,num2){
    return num1+num2;
};
```
-----

**例三**：如果箭头函数代码块部分多于一条语句，就要使用大括号将他们括起来，并且使用`return`语句返回。
```
var sum = (num1,num2) => {return num1+num2;}

```

**例四**： 入股箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错。
```
//报错
let getId = id => { id:id, name:'Temp'};

//不报错
let getId = id => ({id: id,name:'Temp'});

```
------
### 箭头函数中的this
  在箭头函数中，修复了this的指向。箭头函数内部this总是指向外层调用者。是因为箭头函数本身没有this，因此调用的this是外层作用域的this。

例五：箭头函数转成ES5代码如下

```
//ES6
function foo() {
  setTimeout(() => {
    console.log('id:',this.id);
  },100);
}

//ES5
function foo(){
  var _this=this
  setTimeout(function(){
    console.log('id',_this.id);
  },100);
}
```
------

# 注意事项
1.函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
2.不可以当作构造函数，即不可以使用new命令，否则会抛出一个错误。因为箭头函数本身没有自己的this。
3.不可以使用arguments对象，该对象在函数体内不存在。
4.不可以使用yield命令，因此箭头函数不能用作Generator函数。

------

# 参考
阮老师写的ES6教材：箭头函数介绍https://github.com/ruanyf/es6tutorial/blob/a67b5782e7f161f8919b37f2288061e0f4a20454/docs/function.md#L596 