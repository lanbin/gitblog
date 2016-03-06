title: Class in ES6(3) -- class的使用细节
tags: []
categories: []
date: 2016-03-06 13:57:00
---
### 使用细节

*extends后面接可以任何表达式*

````javascript
//此方法可以用于多重继承
class Foo extends combine(MyMixin, MySuperClass) {}
````

*class中的方法后面可以接分号*
````javascript

class Foo {
    construct(){};
    method(){};
}
````

*一些细节*

>1. 类名不能为val/arguments
>2. 类的属性和方法名不能重复
>3. constructor方法只能是普通方法,不能设置成getter/setter或者是generator方法
>4. 类名不能当做方法名使用
>5. 类的prototype对象不能当做构造函数使用
>1. 静态方法可以被写或者配置,但是不能被枚举
>2. 类的prototype对象不能被写/枚举/配置
>3. 类的prototype.construct方法也是一样
>4. 类的prototype对象的方法可以被写/配置,但是不能被枚举


参考:

[exploringjs.com- Classes](http://exploringjs.com/es6/ch_classes.html)