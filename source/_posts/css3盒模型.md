title: css3盒模型
tags: []
categories:
  - css
date: 2016-03-13 14:41:00
---
在css中,万物都是一个盒子,只是不同盒模型的计算方式,和增加了样式会让不同的元素看起来千差万别.

![](https://leohxj.gitbooks.io/front-end-database/content/html-and-css-basic/assets/box-model.svg)

<!--more-->

盒模型的值
1. content-box (默认)
2. padding-box
3. border-box

其不同的点在于对一个盒子的宽高属性值的计算.

##### content-box
width/height即为content的宽高
##### padding-box
width/height为content的宽高加上自己的padding值
##### border-box
width/height为在padding-box的基础上加上border的值


### margin叠加

1. 无padding&border的空元素,其上下margin会产生叠加,添加内容或者padding/border时,叠加消失
2. 相邻的两个元素上下边相遇时,margin叠加(可以将相邻的两个元素用空元素隔开)
3. 父子元素若没有padding/border相隔,其margin产生叠加.