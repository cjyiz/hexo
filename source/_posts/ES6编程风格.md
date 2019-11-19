---
title: ES6编程风格
date: 2019-06-8 09:32:39
tags: ES6
categories: Javascript
---
# 一.块级作用域
### 合理使用const和let取代var
在`let`和`const`之间，建议优先使用`const`，尤其在全局环境下，尽量避免设置变量。多使用`const`有利于提高程序的运行效率。
`let`和`const`的本质区别是编译器内部的处理不同。
`const`声明常量还有两个好处，一是阅读代码的人会立刻意识到不应该修改这个值。二是防止了无意间修改变量值所导致的错误

# 二.字符串
静态字符串一律使用单引号或反引号，不使用双引号。动态字符使用反引号。
```
//不建议
const a="foobar"
const b='foo'+a+'bar'

//建议
const a='foobar'
const b=`foo${a}bar`
```

# 三.解构赋值
### 使用数组成员对变量赋值时，优先使用解构赋值。
```
const arr=[1,2,3,4]

//不建议
cosnt first=arr[0]
const second=arr[1]

//建议
const [first,second]=arr
```

### 函数的参数如果是对象的成员，优先使用解构赋值
```
//不建议
function fn(user){
  const firstName=user.firstName
  const lastName=user.lastName
}

//建议
function getFullName({firstName,lastName}){}
```
如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值，这样便于以后添加返回值，以及更改返回值的顺序。

# 对象
对象定义后，尽量避免添加新的属性。如果要加，推荐使用`Object.assign`方法
```
//不建议
const a={}
a.x=3

//非要后加
const a={}
Object.assign(a,{x:3})

//建议
const a={x:null}
a.x=3
```

# 数组
使用扩展运算符`...`拷贝数组
```
const itemsCopy=[...items]
```
使用Array.from方法，将类似数组的对象转为数组
```
const foo=document.querySelectorAll('.foo')
const nodes=Array.from(foo)
```

# 函数
所有配置项都应该集中在一个对象，放在最后一个参数，**布尔值不可以直接作为参数**。
```
//不建议
function divide(a.b,option=false){}

//建议
function divide(a,b,{options=false}={})
```

# Map结构
注意区分Object和Map,只有模拟现实世界的实体对象时，才能使用Object。如果只是需要`key-value`的数据结构，使用Map即可，因为Map有内建的遍历机制。

# Class
使用class类
```
//不推荐
function que(contents=[]){
  this._que=[...contents]
}
que.prototype.po=function(){
  const value=this._que[0]
  this._que.splice(0,1)
  return value
}


//推荐写法
class que{
  constructor(contents=[]){
    this._que=[...contents]
  }
pop(){
  const value=this_que[0]
  this._que.splice(0,1)
  return value
}
}
ES6中使用extends实现继承。不过值得一提的是，在TypeScript中，引入了直接的类的概念，比ES6的更优。
```

# 模块
1. 使用`import`取代`require`
2. 用`export`取代`module.exports`
3. 如果模块只有一个输出值，就是用`export default`。如果模块有多个输出值，就不使用`export default`,`export default`与普通的`export`不要同时使用。
4. 尽量避免在模块中使用通配符`*`
```
//不建议
import * as myObject from './sad'

//建议
import myObject from './sad/
```
5. 模块默认输出一个函数，函数名的首字母应该**小写**
```
function makeStyle(){}
export default makeStyle
```

6. 模块默认输出一个对象，对象名的首字母应该大写
```
const StyleGuide={es6:{}}
export default StyleGuide
```
