---
title: ES6之symbol
date: 2018-11-18 11:39:00
tags: ES6
categories: Javascript
---
# 一.symbol的作用
因为对象添加新的方法，新方法名字可能与现有方法产生冲突，因此引入symbol。

# 二.symbol注意点
1. symbol值是通过Symbol函数生成，但是Symbol函数不能使用new命令。因为生成的Symbol是一个原始类型的值，不是对象。
2. Symbol函数的参数只是表示对当前Symbol值的描述，因此相同参数的Symbol函数的返回值是不相等的。
3. Symbol值不能与其他类型的值进行运算，会报错。
4. 创建Symbol的时候可以使用实例属性`description`直接返回Symbol的描述
```
const sym=Symbol('foo')
console.log(sym.description) //foo
```
5. symbol值作为对象属性名时，不能用点运算符
```
const mySymbol=Symbol()
const a={}
a.mySymbol='hello' //错误写法
a[mySymbol] //正确写法
a['mySymbol'] //错误写法
```
6. 在对象内部，使用Symbol值定义属性时，Symbol值必须放在方括号中。如果不在，就是字符串。
```
let s=Symbol()
let obj={
  [s].function(arg){...}
}
obj[s](123)
```