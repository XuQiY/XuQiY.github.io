---
layout:     post
title:      "JS控制动画"
subtitle:   " \"AnimationRequestFrame\""
date: "2019-9-26 2:57"
author:     "Mrx"
header-img: "img/2019-07-27.png"
catalog: true
tags:
    - AnimationRequestFrame
    - setIntervel
    - Js
---
今晚做笔试题遇到了一题是要求点击DIV使其旋转，再次点击让其加速和点击stop让其减速，机灵的我使用了Animation完成
```CSS
 @keyframes div_rot {
            to {
                transform: rotate(360deg);
            }
        }
        
        .div1 {
            width: 200px;
            height: 200px;
            background-color: red;
            margin: 0 auto;
            animation: div_rot 9999999ms infinite linear;
        }
/*先设置个animation属性，添加时间999999让其不动（有点多此一举），然后通过JS操控Animation实现*/
```
```js
    var div1 = document.getElementById("div1");
    var speed = 500;  //通过操控speed实现速度加减
    function start() {
        console.log("start click");
        if (speed > 50) speed -= 50;
        div1.style.animation = `div_rot ${speed}ms infinite linear`;
    }

    function stop() {
        console.log("stop click");
        speed += 50;
        div1.style.animation = `div_rot ${speed}ms infinite linear`;
    }
        
```
但是题目有个提示用**AnimationRequestFrame**完成，AnimationRequestFrame是何方神圣，这还真没用过，所以考完赶紧找资料来看一下.发觉它的用法其实和`setTimeout`挺相似的，只是不需要添加时间.



>  `window.requestAnimationFrame(callback)` 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行

 ### 参数
>
>  ```
>  callback
>  ```
>
>  下一次重绘之前更新动画帧所调用的函数(即上面所说的回调函数)。该回调函数会被传入[`DOMHighResTimeStamp`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMHighResTimeStamp)参数，该参数与[`performance.now()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Performance/now)的返回值相同，它表示`requestAnimationFrame()` 开始去执行回调函数的时刻。

 ### 返回值
>
>  一个 `long` 整数，请求 ID ，是回调列表中唯一的标识。是个非零值，没别的意义。你可以传这个值给 [`window.cancelAnimationFrame()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/cancelAnimationFrame) 以取消回调函数。
>
>  

```js
//***不愧是与浏览器屏幕刷新次数相匹配，转起来特别好看***
       function start() {
            console.log("start click");
            if (!flag) {
                var timer = requestAnimationFrame(function fn() {
                    div1.style.transform = `rotate(${deg+=30*flag}deg)`;
                    div1.style.transition = "transform 500ms linear";
                    //通过回调多次执行；
                    timer = requestAnimationFrame(fn); 
                });
            }
            flag += 1;
            console.log("start", flag)
        }

        function stop() {
            if (flag > 0)
                flag -= 1;
        }
```

>by Mrx