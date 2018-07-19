---
layout: postname
title: Proxy
date: 2018-07-19 15:05:38
category: 文章
tags:
---



###  Proxy   

 Proxy用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。
 Proxy 可以理解为在目标对象前假设一层“拦截”层，外界对改对象的访问必须想通过该层的拦截，因此提供了一种机制，可以对外界的访问
 进行过滤和改写。      
```
var obj = new Proxy({}, {
  get: function(target, key, receiver) {
    console.log(`getting ${kkey}`);
    return Reflect.get(target, key, receiver);
  },
  set: function(target, key, value, receiver) {
    return Reflect.set(target, key, value, receiver);
  }
})

// 对一个空对象做了一层拦截，重定义了属性的读（get）和设置（set）行为
```  

ES6 原生提供了Proxy的构造函数，用于生成Proxy实例。  
`var proxy = new Proxy(target, handler)`  
> 参数target表示要拦截的目标对象，handler也是一个对象，用来定制拦截行为。  

