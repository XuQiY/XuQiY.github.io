---
layout:     post
title:      "JS面试题"
subtitle:   " \"设计模式\""
date: "2019-9-19 22:27"
author:     "Mrx"
header-img: "img/post-bg-universe.jpg"
catalog: true
tags:
    - 面试题
    - 闭包
    - Js
---

# js

### 1.闭包

``` js
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log(new Date, i);
    }, 1000);
}

console.log(new Date, i);  //5,5,5,5,5

//要求输出5,0,1,2,3,4
//方法一 IIFE
for (var i = 0; i < 5; i++) {
    (function(i) {
        setTimeout(function() {
            console.log(new Date, i);
        }, 1000);
    })(i)
}

//方法二 setTimeout(f,time,params)传递参数
for (var i = 0; i < 5; i++){
        setTimeout(function(j) {
            console.log(new Date, j);
        }, 1000,i);
}
console.log(new Date, i);

//方法三 调用外部函数
function output(j) {
    setTimeout(() => console.log(new Date, j))
}
for (var i = 0; i < 5; i++) {
    output(i)
}

console.log(new Date, i);

//要求输出0,1,2,3,4,5

//方法一 IIFE闭包
for (var i = 0; i < 5; i++) {
    ((j) => {
        setTimeout(function() {
            console.log(new Date, j);
        }, 1000 * j);
    })(i)
}

setTimeout(() => console.log(new Date, i), i * 1000);

//方法二 promise  var可以修改成let块级作用域
var task = []
for (var i = 0; i < 5; i++) {
    ((j) => task.push(new Promise((resolve, reject) => {
        setTimeout(() => console.log(j, new Date), 1000 * j)
        resolve();
    })))(i)
}
Promise.all(task).then(() => {
    setTimeout(() => {
        console.log(i, new Date)
    }, 1000 * i);
})


//方法三 async
const sleep = (timeountMS) => new Promise((resolve) => {
    setTimeout(resolve, timeountMS);
});

(async () => {  
    for (var i = 0; i < 5; i++) {
        if (i > 0) {
            await sleep(1000);
        }
        console.log(new Date, i);
    }

    await sleep(1000);
    console.log(new Date, i);
})();
```
  
>   Mrx
