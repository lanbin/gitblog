title: Javascript继承
tags: []
categories:
  - javascript
date: 2016-03-01 14:44:00
---
Javascript的继承一直都是一个世纪大难题. 
主要是因为在Javascript中所有的数据类型都是对象,但是没有类的概念.  
虽然现在ES6中已经可以开始使用class关键字,但是离大面积使用还是有段距离.而且在文档中,class关键字并非是一种新的创建对象的方式,它只是一种更清晰/方便的创建类和继承的语法.

### 理解prototype
Javascript的起源是用作简单的网页交互.但是由于其数据类型都是对象,所以需要用继承将所有的对象关联起来.那么有了对象要创建实例就引入了new命令.  

但是new命令会将构造函数中的所有数据都全部创造一个副本,这样一些公用的属性和方法就会随着实例的增多而耗费更多的资源

```` javascript
function Sth(){
	this.pro_one = ''
    this.fun_one = function(){}
}

var sth_one = new Sth()
var sth_two = new Sth()

sth_one.fun_one != sth_two.fun_one //false, 因为在实例化的时候开辟两个内存区域
````

所以为了解决这个问题,引入了prototype.  
有了prototype,大家开始建议这样书写

```` javascript
function Sth(){
	this.pro_one = ''
}

Sth.prototype.fun_one = function() {}
````

prototype属性是一个对象,存放的是所有实例对象需要共享的属性和方法.  
其实相当于构造函数里面的属性和方法分了两种,一种在构造函数里在this下自己拥有,一种在prototype上共享使用的.


### 理解继承


理解继承有两个主要的属性
```` javascript
function Sth(){
	...
}

var sth = new Sth()

//sth.prototype 原型对象
//sth.construct (指向Sth)此属性指向其构造函数
````

### 原型链继承

继承就是需要子类要拥有父类的属性和方法,原型继承的方式就是在子类定义了自己的属性和方法之后,再将父类的属性和方法放在子类的公共区域,可以供子类的所有的实例进行使用,那么按照上方说的方法,就是讲父类的实例要放在子类的prototype中,形如

```` javascript
function Sup(){
	this.age = 45
}

//父类中的prototype对象中所有的属性和方法可以看做是public,而在构造函数中的属性和方法则是private
Sup.prototype.getAge = function() {return this.age}

function Sub(){
	this.age = 20
}

//将父类的属性和方法放在子类的公共区域
Sub.prototype = new Sup() //Sub.prototype为Sup的一个实例,其construct指向的为Sup

//假如此时创建一个实例
//var sub = new Sub()
//实例的construct对象也会指向Sup,这明显是有问题的,所以需要手动将此属性指回来再创建实例
//console.log(sub.construct) //显示 Sup

Sub.prototype.construct = Sub
````

参考:

[阮一峰的网络日志 - Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)