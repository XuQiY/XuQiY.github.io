---
layout:     post
title:      "JS面试题02"
subtitle:   " \"URL解析\""
date: "2019-10-9 10:05"
author:     "Mrx"
header-img: "img/2019-08-13.png"
catalog: true
tags:
    - 面试题
    - URLSearchParams
    - Js
---

> 今天做面试题遇到一题解析URL参数，采用了常用的分割分割再分割的方法，感觉有点臃肿，固查了一下其它方法，结果发现了新大陆——URLSearchParams这个URL对象接口。由于之前没有接触过，所以搜索了一下具体的用处，发现这个接口的功能很实用。下文摘自https://segmentfault.com/a/1190000019099536



## URLSearchParams是什么

`URLSearchParams` 接口定义了一些实用的方法来处理 `URL` 的查询字符串。[参照](https://developer.mozilla.org/zh-CN/docs/Web/API/URLSearchParams)

从而我们可以知道，它是用来处理URL相关的。那具体都有哪些功能呢？

## 接口方法

首先，我们调用`new URLSearchParams()`会返回一个 `URLSearchParams` 对象实例。在这个实例下面我们可以调用以下方法：

**append(name, value)**:插入一个指定的键/值对作为新的搜索参数。
其中`name`是需要插入搜索参数的键名，`value`是需要插入搜索参数的对应值。

```
let url = new URL('https://example.com?foo=1&bar=2');
let params = new URLSearchParams(url.search.slice(1));

//添加第二个foo搜索参数。
params.append('foo', 4);
params.toString();
// 'foo=1&bar=2&foo=4'
```

**delete(name)**:从搜索参数列表里删除指定的搜索参数及其对应的值。
`name`是需要删除的键值名称。

```
let url = new URL('https://example.com?foo=1&bar=2');
let params = new URLSearchParams(url.search.slice(1));

//添加第二个foo搜索参数。
params.delete('foo');
params.toString();
// 'bar=2'
```

**entries()**:返回一个`iterator`可以遍历所有键/值对的对象。

```
// 创建一个测试用 URLSearchParams 对象
let searchParams = new URLSearchParams("key1=value1&key2=value2");

// 显示键/值对
for(var pair of searchParams.entries()) {
   console.log(pair[0]+ ', '+ pair[1]); 
}

// key1, value1
// key2, value2
```

**get(name)**:获取指定搜索参数的第一个值。
`name`是将要返回的参数的键名。返回一个`USVString`；如果没有，则返回`null`。
如果一个页面的URL是 `https://example.com/?name=Jonathan&age=18` ，你可以这样解析参数`name`和`age`:

```
let params = new URLSearchParams(document.location.search.substring(1));
let name = params.get("name"); // is the string "Jonathan"
let age = parseInt(params.get("age"), 10); // is the number 18

// 查找一个不存在的键名则返回 null:
let address = params.get("address"); // null
```

**getAll(name)**:获取指定搜索参数的所有值，返回是一个数组。
`name`是返回的参数的名称。

```
let url = new URL('https://example.com?foo=1&bar=2'); 
let params = new URLSearchParams(url.search.slice(1)); 

//为foo参数添加第二个值 
params.append('foo', 4);

console.log(params.getAll('foo'))' //输出 ["1","4"].
```

**has(name)**:返回 Boolean 判断是否存在此搜索参数。
`name` 是我们要查询的参数的键名。

```
let url = new URL('https://example.com?foo=1&bar=2');
let params = new URLSearchParams(url.search.slice(1));

params.has('bar') === true; //true
```

**keys()**:返回iterator 此对象包含了键/值对的所有键名。

```
// 建立一个测试用URLSearchParams对象
let searchParams = new URLSearchParams("key1=value1&key2=value2"); 

// 输出键值对
for(var key of searchParams.keys()) { 
  console.log(key); 
}

// key1
// key2
```

**set(name, value)**:设置一个搜索参数的新值，*假如原来有多个值将删除其他所有的值*。
其中`name`是需要插入修改参数的键名，`value`是需要插入搜索参数的新值。

```
let url = new URL('https://example.com?foo=1&bar=2');
let params = new URLSearchParams(url.search.slice(1));

//Add a third parameter.
params.set('baz', 3);
```

**sort()**: 按键名排序。

```
// Create a test URLSearchParams object 
let searchParams = new URLSearchParams("c=4&a=2&b=3&a=1"); 

// Sort the key/value pairs
searchParams.sort();

// Display the sorted query string
console.log(searchParams.toString());

// a=2&a=1&b=3&c=4
```

**toString()**:返回搜索参数组成的字符串，可直接使用在URL上。

```
let url = new URL('https://example.com?foo=1&bar=2');
let params = new URLSearchParams(url.search.slice(1));

//Add a second foo parameter.
params.append('foo', 4);
console.log(params.toString());
//Prints 'foo=1&bar=2&foo=4'.
```

**values()**:返回iterator 此对象包含了键/值对的所有值。



```
// 创建一个测试用URLSearchParams对象
let searchParams = new URLSearchParams("key1=value1&key2=value2");

// 输出值
for(var value of searchParams.values()) {
  console.log(value);
}
```

上面就是针对其所有的接口方法进行的一个梳理。然而，感觉好像和我们平时的关联没有很大呢？下面让我们来看几个具体的使用场景。



## 使用场景



### 场景一 获取浏览器地址参数

我们之前在获取浏览器地址参数时很多时候是通过对地址进行分割，然后拼接字段对象的方式来做的，类似

```
function GetRequest() {
  let url = location.search; //获取url中"?"符后的字串
  let theRequest = new Object();
  if (url.indexOf("?") != -1) {
    let str = url.substr(1);
    strs = str.split("&");
    for (let i = 0; i < strs.length; i++) {
      theRequest[strs[i].split("=")[0]] = (strs[i].split("=")[1]);
    }
  }
  return theRequest;
}
```

但是我们如果使用`URLSearchParams`时就不用这么繁琐了

```
const params = new URLSearchParams(location.search)
params.get(key)
```

### 使用URLSearchParams处理axios发送的数据

在我们使用`axios`和`fetch`来替换之前的`ajax`进行数据请求时，我们会遇到数据格式不一致的问题。

```
axios({
    method: 'post',
    url: '/test',
    data: {
        name: 'li lei',
        age: 18
    }
})
```

上面的调用方法和我们使用ajax时非常相似，我们可能也会自然而然的这样来写，但是我们会发现，其默认的数据格式是有差别的：

axios数据格式：
![axios数据格式](https://lengxing.club/2019/05/07/2019-05-07/1.png)

ajax数据格式：
![akax数据格式](https://lengxing.club/2019/05/07/2019-05-07/2.png)

是的，多了一层包裹，这样和我们后端的对接就出现问题了。哪怕是手动去修改ContentType为`application/x-www-form-urlencoded`仍然没有解决。

![axios数据格式修改后](https://lengxing.club/2019/05/07/2019-05-07/3.png)

那么URLSearchParams能如何解决呢

```
let params = new URLSearchParams();
params.append('name', 'li lei');
params.append('age', 18);

axios({
    method: 'post',
    url: '/test',
    data: params
})
```

#### 兼容性解决

工具好用，但是不可避免的兼容性并没有那么的理想。那我们该怎么办呢？

> 工欲善其事，必先利其器

[url-search-params-polyfill](https://github.com/jerrybendy/url-search-params-polyfill/)

这是一个专门为URLSearchParams制作的polyfill库。具体的使用方法大家可以参照库的相关说明。在这主要再强调一下，这个库能够解决浏览器的兼容性问题，但是在使用fetch进行请求调用时，我们仍然需要手动去设置ContentType的值。引用该库中给到的一个实例

```
function myFetch(url, { headers = {}, body }) {
    headers = headers instanceof Headers ? headers : new Headers(headers);
    
    if (body instanceof URLSearchParams) {
        headers.set('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
    }
    
    fetch(url, {
        headers,
        body
    });
}
```

## 小结

通过我们对官方接口的说明以及实际场景的使用，详细了解了URLSearchParams的主要功能和使用方法，希望能够在我们以后的开发中起到帮助作用。





> by Mrx