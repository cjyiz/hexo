---
title: flex布局简介
date: 2018-10-29 13:13:54
tags: flex
categories: CSS
---
# 什么是flex模型
  Flex布局又称弹性布局，是W3C于09年提出的新的布局方案。相比于传统的盒子模型，Flex布局更加灵活，可以简便，完整，响应式的实现各种页面布局。并且得到了所有浏览器的支持，因此该布局方案是未来布局的首选方案。
  任何一个容器都可以设置Flex布局，包括*行内元素容器*！<!-- more -->
```
.box{
	display:flex;
}
```
   *值得注意的是：设为Flex布局以后，子元素的`float`,`clear`,`vertical-align`属性都将失效。*
---
# flex语法
  容器设置为Flex布局后，其所有子元素自动成为容器成员，称为Flex项目。
  Flex容器和Flex项目各有6个属性，利用这些属性可以设置成各种想要的布局。

## 容器的6个属性如下
```
flex-direction
flex-wrap
flex-flow
justify-content
align-items
align-content
```

### 1.flex-direction
   决定项目排列的方向。有4个值：
   `row`: **默认值！**项目从左向右排列
   `row-reverse`: 项目从右向左排列
   `column`: 项目从上向下排列
   `column-reverse`: 项目从下向上排列
### 2.flex-wrap
   `wrap`:换行，第一行在上方
   `nowrap`:**默认值！**不换行
   `wrap-reverse`:换行，第一行在下方
### 3.flex-flow
   该属性是`flex-driection`属性和`flex-wrap`属性简写形式，默认值为`row nowrap`
### 4.justify-content
   该属性定义了项目在主轴上的对齐方式。有5个值：
  `flex-start`:按照项目排列顺序对齐
  `flex-end`:按照项目排列顺序反向对齐
  `center`:居中对齐
  `space-between`:两端对齐，项目之间等间隔
  `space-around`: 每个项目之间两侧间隔相等
### 5.align-items属性
   该属性定义项目在交叉轴（*与主轴垂直*）上如何对齐。同样有5个值：
   `flex-start`:交叉轴起点对齐
   `flex-end`:交叉轴终点对齐
   `center`:交叉轴中点对齐
   `baseline`:项目第一行文字的基线对齐
   `stretch`:**默认值！**如果项目为设置高度或者设为auto，将占满整个容器的高度。
### 6.align-content属性
   该属性定义多根轴线对齐方式。如果只有一根轴线，该属性不起作用。
   `flex-start`:交叉轴起点对齐
   `flex-end`:交叉轴终点对齐
   `center`:交叉轴中点对齐
   `space-between`:与交叉轴两端对齐，轴线之间的间隔平均分布
   `space-around`:每根轴线两侧的间隔都相等
   `stretch`:**默认值！**自动铺开，轴线占满整个交叉轴

----
## 项目的6个属性如下

```
order
flex-grow
flex-shrink
flex-basis
flex
align-self
```

### 1.order属性
  定义项目排列顺序，数值越小，排列越靠前，默认为0。
### 2.flex-grow属性
  定义项目放大比例，默认值为0，即项目空间足够时，项目不放大。
### 3.flex-shrink属性 
  定义了项目缩小比例，默认值为1，即空间不足时，项目等比例缩小。
### 4.flex-basis属性
  定义了项目在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间。默认值为`auto`，即项目本来大小。
### 5.flex属性
  该属性是`flex-grow`,`flex-shrink`,`flex-basis`属性的简写，默认值为`0 1 auto`。常用的快捷属性有
  `auto(1 1 auto)`,`none(0 0 auto)`
### 6.align-self属性
   该属性有6个属性，除了`auto`，其他属性与`align-items`一样。允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性，默认值为`auto`，表示继承父元素`align-items`属性，如果没有父元素，则等同于`stretch`。


----



