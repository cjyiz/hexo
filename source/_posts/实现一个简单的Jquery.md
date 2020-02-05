---
title: 实现一个简单的jQuery
date: 2018-12-10 13:33:55
tags: jQuery
categories: Javascript
---
## 思路
1. 根据字符串接受一个选择器或者节点，将其封装成伪数组(对象)
2. 在伪数组上加入几个封装好的API
3. 返回伪数组
4. 使用时，声明一个变量使用jQuery()方法获取元素，然后调用其属性方法就可以。
jQuery本质是一个构造函数，接受参数，根据封装好的API操作对应节点，返回一个结果。<!-- more -->

## 源码如下
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>封装一个简单jQuery</title>
</head>
<style>
    div {
        border: 1px solid black;
        width: 200px;
        height: 200px;
    }
    .red {
        color: red;
    }
    .green {
        color: green;
    }
</style>

<body>
    <div>1</div>
    <div id='n'>2</div>
    <div>3</div>
</body>
<script>
    window.jQuery = function (nodeOrSelector) {
        let nodes = {}   //定义一个空的对象，方便后面传值
        if (typeof nodeOrSelector === 'string') { //对传入的节点进行判断，如果是多个节点，需要遍历将其一一取出，
            let temp = document.querySelectorAll(nodeOrSelector) //伪数组
            console.log(temp)
            for (let i = 0; i < temp.length; i++) {
                nodes[i] = temp[i]
            }
            nodes.length = temp.length
        } else if (nodeOrSelector instanceof Node) { //如果只是单个节点，给他一个固定值
            nodes = {
                0: nodeOrSelector,
                length: 1
            }
        }
        //封装addClass函数
        nodes.addClass = function (value) { //因为有多个节点，所以需要一一遍历
            for (let i = 0; i < nodes.length; i++) {
                nodes[i].classList.add(value)
            }
        }
        //封装setText函数
        nodes.setText=function(text){
            for (let i = 0; i < nodes.length; i++) {
                nodes[i].textContent=text
            }
        }
        return nodes   //很重要，返回一个伪数组。
    }
    window.$ = jQuery
    var $div = $('div')
    $div.addClass('red')
    $('#n').addClass('green')
    $div.setText('hi')
</script>
</html>
```

## 注意事项
$div 本质上就是一个Hash结构的对象,如下:
```
{
  0:div,
  1:div,
  2:div,
  addClass:f1,
  setText:f2,
  length:6
}
```