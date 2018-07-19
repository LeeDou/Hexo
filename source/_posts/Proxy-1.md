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

#### Proxy实例的方法   
get()    
- 用于拦截某个属性的读取操作。get方法可以继承。  

set()  
- 用于拦截某个属性的赋值操作  
```
let validator = {
  set: function(obj, prop, value) {
    if(prop === 'age') {
      throw new Error('the age is not invalid')
    }
    // 对于age以外属性都之际额保存
    obj[prop] = value;
  }
}

let person = new Proxy({}, validator);

person.age = 10;
person.age; // 10
```

apply()
- 用于函数的调用、call、apply操作。

has()   
- 可以隐藏某些属性，不被in操作符发现。

construct()   
- 用于拦截new()命令。

deleteProperty()   
- 用于拦截delete操作，如果这个方法抛出错误或返回false，当前属性就无法被delete命令删除。  

defineProperty()   
- 方法拦截了Object.defineProperty操作。

enumerate()   
- enumerate方法用于拦截for...in 循环。  

getOwnPropertyDescripter()   
- 方法拦截了Object.getOwnPropertyDescriptor, 返回一个属性描述对象或undefined。

getPrototype()   
- 用于拦截Object.getPrototype运算符及其它一些方法。

ownKeys()   
- 用于拦截Object.keys()方法。

isExtensible()
- 用于拦截Object.isExtensible操作。

preventExtension()、setPrototype() 均用于拦截对应的方法。  

#### Proxy.revocable()
返回一个可取消的Proxy实例。
```
let target = {};
let handler = {};

let {proxy, revoke } = Proxy.revocable(target, handler);

proxy.foo = 123;
proxy.foo; // 123

revoke();
proxy.foo; // Typeerror: Revoked
```

> Proxy.revocable方法返回一个对象，其proxy属性是Proxy实例，revoke属性是一个函数，可以取消Proxy实例。

