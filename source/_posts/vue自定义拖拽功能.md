---
title: vue自定义拖拽功能
date: 2019-12-15 10:06:41
tags: Vue
categories: Vue
---
# 具体代码如下
```
<template>
  <div v-drag>
  </div>
</template>
<script>
export default {
  name: 'drag',
  directives: {
    drag (el, bindings) {
      el.onmousedown = function (e) {
        var disX = e.pageX - el.offsetLeft;
        var disY = e.pageY - el.offsetTop;
        document.onmousemove = function (e) {
          el.style.left = e.pageX - disX + 'px';
          el.style.top = e.pageY - disY + 'px';
        }
        document.onmouseup = function () {
          document.onmousemove = document.onmouseup = null;
        }
      }
    }
  }
}
</script>
```