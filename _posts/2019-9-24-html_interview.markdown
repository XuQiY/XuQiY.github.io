---
layout:     post
title:      "H5面试题(一)"
subtitle:   " \"H5\""
date: "2019-9-24 17:00"
author:     "Mrx"
header-img: "img/2019-07-17.png"
catalog: true
tags:
    - 面试题
    - HTML
    - H5
---

### 1.行内元素和块级元素的区别？
``` html
    行内元素:<a><b><br><em><i><img><input><label><span><strong>...
    块级元素:<h1>~<h5><p><div><li><ol><ul><dd><dl><dt><td>...
    1.行内元素在宽度足够的情况下会并排在一行（宽度只与内容有关），而块级元素单独占据一行，宽度默认为父元素的宽度（与内容无关）
    2.块级元素可以包含行内元素和块级元素，而行内元素只能包含文本或行内元素
    3.行内元素设计宽高无效，margin与padding上下无效
    4.两者转换{display:bolck} {display:inline}
```

### 2.H5新特性？
``` html
    1.新增语义化标签:<footer><header><section><nav>...
    2.新的表单控件：<data><time><search><url>...
    3.新的技术:webworker,websockt,Geolocation..
    4.媒体音频播放:<video><audio>
    5.用于绘图:canvas

```

### 3.什么是<!DOCTYPE>?
> DOCTYPE是html5标准网页声明，且必须声明在HTML文档的第一行。来告知浏览器的解析器用什么文档标准解析这个文档。


### 4. 渐进增强和优雅降级
>+ <strong>渐进增强</strong>：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能，达到更好的用户体验。
>+ <strong>优雅降级</strong>：一开始就构建完整的功能，然后再针对低版本的浏览器进行兼容

### 5.3. HTML语义化

>+ 用正确的标签做正确的事情。
>+ html语义化让页面的内容结构化，结构更清晰，便于对浏览器，搜索引擎解析；
>+ 即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的；
>+ 搜索引擎的爬虫也依赖于HTML标记确定上下文和各个关键字的权重，利于SEO;
>+ 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

------

> by Mrx

