---
layout:     post
title:      "简单的东西做到极致"
subtitle:   " \"细微而致\""
date: "2019-9-24 22:11"
author:     "Mrx"
header-img: "img/2019-08-06.png"
catalog: true
tags:
    - 生活
    - Vue
    - Js
---

>### 把简单做到极致，就是匠心
----
 | 前言

  难得没有面试和笔试的一天,竟然感觉有点不适应。哈哈，奇怪~
  昨天学VUE的时候做了的[todolist](http://dengtingting.top:8001/todolist.html)的，想着今天把它优化一下，利用`localStorage`来进行todo的永久存储。
  + 首先遇到的第一个问题是关于`localStorage`存储格式的问题，我想要存储的是对象,但是localStorage返回的是String类型，想到了`JSON`的`parse`和`stringify`方法，先用`stringify`把数据转为字符串存入,需要用时再把它取出`parse`成对象
  + 第二个问题就是发现了`localStorage`设置不了`timeout`，其实这也刚好符合我的预想，设置了个按钮`click`点击然后`delete localStorage.todolist`即可
  + 第三个问题是初始todolist为空，巧用三元运算符解决,`todolist: localStorage.todolist == null ? [] : JSON.parse(localStorage.todolist)`
  + 初步涉及到vue的生命周期函数，和U3D，安卓的生命周期其实大同小异，理解起来还不错，只是是需要应用加深
  + ...
  就这样不知不觉做着做着就已经天黑了，但是还是不曾觉得疲倦，接下来把定时提醒，颜色提醒搞搞，哈哈，感觉我可以在这个todolist耗上一个月,或许这就是前端的魅力所在吧，*所见即所得*，每一次小成功都可以激励你进行下一步。加油~

  >by Mrx
