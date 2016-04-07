title: Redux
tags:
  - redux
  - action
categories:
  - Redux
date: 2016-04-06 11:56:00
---
在Reactjs中,每一个component的数据来源分为两个部分`props`&`state`  

`props`属于从外界传入的属性集,不能在组件周期中进行修改  
`state`是内部的属性集,可以在组件周期中随便修改

由于Reactjs只是涉及到view层,view层的具体显示是根据各个数据的变化来进行渲染.那么Reactjs就需要一个来对数据进行统一处理的工具,类似提供 c & m 层.

### Redux

Facebook官方提出了Flux这种单向数据流的应用模式

> Action -> Dispatcher -> Store -> View

而Redux则是这种模式的一种实现,其为零依赖.


在Flux中Action和Store对于dispatch有强耦合

> 1. Action在Flux中就是对一个dispatch做了封装,但是在Redux中,Action只是单纯的返回一个对象
> 2. Store在Flux中也需要封装一个dispatch,同时在修改完state之后还需要emmit一个change事件,而在Redux中Store只是接受一个oldValue,处理完之后返回一个newValue

所以在Redux的整个流程中将会变成

> Dispatcher -> Action -> Reducer -> View

在任何的一个地方进行Dispatch的动作,其参数就是一个Action的对象.  
此时所有的Reducer是会进行顺序响应来判断action.type是否为自己需要处理的事件.  
传入新值返回旧值, 更改view

这几乎就是Redux的全部


参考:
> 1. [React-Tutorial -  GitBook](https://hulufei.gitbooks.io/react-tutorial/)