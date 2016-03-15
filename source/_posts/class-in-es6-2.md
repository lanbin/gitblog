title: Class in ES6(2) -- 私有变量
tags: []
categories: []
date: 2016-03-05 13:06:00
---
#### class的私有变量

>1. Keeping private data in the environment of a class constructor
>2. Marking private properties via a naming convention (e.g. a prefixed underscore)
>3. Keeping private data in WeakMaps
>4. Using symbols as keys for private properties


>1. 将私有变量放置在构造函数内
>2. 给私有变量使用同一的标识,比如前缀下划线
>3. 设置私有变量为WeakMaps类型
>4. 设置使用symbol作为私有变量的key

<!--more-->

第1/2点在ES5中就是正常使用的,但是在class中,容易造成冲突.  
要避免冲突,使用的方法就不够优雅.  

第3/4点是在ES6中新的方法

WeakMap是一个弱映射关系的对象,拥有set/get/has/delete方法,目前浏览器的支持不算特别的好
````javascript
//创建两个WeakMap对象
const _counter = new WeakMap();
const _action = new WeakMap();
class Countdown {
    constructor(counter, action) {
        _counter.set(this, counter);
        _action.set(this, action);
    }
    dec() {
        let counter = _counter.get(this);
        if (counter < 1) return;
        counter--;
        _counter.set(this, counter);
        if (counter === 0) {
            _action.get(this)();
        }
    }
}
````
或者使用Symbol创建一个标识,这个标识无法在for..in中被循环出来.  
Object.getOwnPropertyNames() 也无法匹配出来  
 Object.getOwnPropertySymbols() 则是可以的
````javascript
const _counter = Symbol('counter');
const _action = Symbol('action');

class Countdown {
    constructor(counter, action) {
        this[_counter] = counter;
        this[_action] = action;
    }
    dec() {
        if (this[_counter] < 1) return;
        this[_counter]--;
        if (this[_counter] === 0) {
            this[_action]();
        }
    }
}
````
每一个symbol实例都是唯一的,所以用symbol作为key永远都不会冲突的.  
而且这个标识代表的变量也是和外界隔绝的.但是现在浏览器支持也不好.






参考:

[exploringjs.com- Classes](http://exploringjs.com/es6/ch_classes.html)  
[WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)  
[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)