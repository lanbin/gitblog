title: Class in ES6(1) -- class基本
tags: []
categories: []
date: 2016-03-04 22:30:00
---

#### class的基本使用方法
````javascript
//在ES6中使用了class关键字,类中包含一个显式的构造函数
class Point{
    constructor(x, y){
    	this.x = x
        this.y = y
    }
}

//继承使用了extends,同时在子类的构造函数中需要使用super来调用父类的构造函数,不然会报错
class ColorPoint extends Point{
    constructor(x, y, color){
    	super(x, y)
        this.color = color
    }
}

//类的使用方法
var p = new Point(5, 8)

//typeof一个类,返回仍是一个function,说明其实class并不是一种新的数据类型.
//只是一种新的创建方式,看起来更加清晰明了
(typeof Point === 'function') // true

//但是类不能像functioin那样被调用,此为区别
Point() //TypeError: Classes can’t be function-called
````


#### class的提升

在ES5中,function的声明会被提升到当前scope的最前面,即方法调用不用管其声明在哪里
```` javascript
//调用写在函数声明之前是OK的
Foo()

function Foo(){}
````

但是对于class,就不能这样处理了.
````javascript
//会报错
new Foo() // ReferenceError

class Foo{}
````
不能这样做的原因是,class可能包含extends表达式,而extends不能被提升,所以extends必须依赖已经声明的class


#### class定义

除了之前的使用class表达式直接定义一个类,也有如下方式
````javascript

//可以使用匿名表达式
const Myclass = class {}

//也可以使用一个名称,但是这个名称只能在class的内部使用
const MySndClass = class msc{
    getClassName() {
    	return msc.name
    }
}
````

#### class的静态变量和方法

````javascript
class Foo(){
    constructor(){}
    //静态方法定义
    static staticMethod(){
    	return 'static method'
    }
}

typeof Foo.staticMethod //'function'
Foo.staticMethod // 'static method'
````
因为在class中只能定义静态方法而不能直接定义静态变量,所以要通过其他方式做实现
````javascript
//1.直接给类增加属性,此属性即为静态属性
Foo.staticVariable = 'sth'
//2.使用get方法
class Foo{
  static get staticVariable(){
  	return 'sth'
  }
}

Foo.staticVariable // 'sth'
````
父类的静态方法也是可以被子类继承的,甚至被override

#### 构造函数相关

1. 继承时,需要优先调用super
````javascript
class Bar extends Foo {
    constructor(num) {
        const tmp = num * 2; // OK
        this.num = num; // ReferenceError
        super();
        this.num = num; // OK
    }
}
````

2. 修改构造函数的返回
````javascript
class Foo {
    constructor() {
        return Object.create(null);
    }
}
console.log(new Foo() instanceof Foo); // false
//这种情况下,无需考虑this是否被初始化,也不用调用super(),因为反正返回的也是其他的对象
````

3. 构造函数的默认调用
````javascript
//父类不显示生命constructor方法,实际上会这样调用
constructor() {}

//子类的话,会是这样的
constructor(...args) {
    super(...args);
}
````


参考:

[exploringjs.com- Classes](http://exploringjs.com/es6/ch_classes.html)