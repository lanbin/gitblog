title: Javascript原型链
tags: []
categories:
  - javascript
date: 2016-03-03 14:43:00
---
#### 原型链继承
原型链在Javascript中主要用作继承,比如下面的例子:   

````javascript
var superObject = {"a": 1, "b": 2}

//此行等同于
//var subObject = {}
//subObject.prototype = superObject
var subObject = Object.create(superObject)

//这样subObject就已经继承了superObject的属性
console.log(subObject.a) // 1
````
<!--more-->

另外一种方式,在继承的时候,给subObject也添加属性

````javascript
var superObject = {"a": 1, "b": 2}

var subObject = Object.create(superObject, {
                    //设置一个属性名为"b"的属性,其对应一个对象描述这个属性的特征
                    "b": { writable:true, configurable:true, value: "3" },
                    "c": { writable:true, configurable:true, value: "4" }
                })

//subObject拥有了自己的属性
console.log(subObject.c) // 4
//同时subObject和supObject拥有了同名的属性"b"
console.log(subObject.b) // 3
````

在对于构造函数继承的时候其实要做的事情也是一样的
````javascript
var point = function(){},
    colorPoint = function(){}

//将父类的方法全部放到原型链上
colorPoint.prototype = new point() 
//重置原型对象的构造函数,单纯为了保持纯净
colorPoint.prototype.construct = colorPoint
````

#### 原型链归结
所有的原型链最终归结

````javascript
//所有的原型链最终会回溯到null
//Object的prototype就是null,Object在这个基础上创建了几乎是javascript基底的所有方法
//Array/Function/Number继承了Object,分别实现了数组/函数/数字类型
sth --> Array.prototype --> Object.prototype --> null
sth --> Function.prototype --> Object.prototype --> null
sth --> Number.prototype --> Object.prototype --> null

//当调用某个属性和方法的时候,首先会查看sth本身是否有这个方法
//如果没有,就从原型链回溯上去,比如去找Array/Function/Number,如果还没有就再回溯一直到null
//其实调用的是 
Object.getPrototypeOf(objectOnPrototype).foo()
````