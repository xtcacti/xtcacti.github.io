---
title: CSS3
date: 2021-02-19 22:22:54
tags: CSS
---

## 样式
- `border-raduis`
- `border-image`
- `box-shadow`
- `background-size`
- `background-origin`
- `background-image`可以同时用几个图片了，多重背景图片
- `text-shadow`
- `text-wrap`
- `@font-face`

## 用户界面
- [resize](https://codepen.io/xtcacti/pen/RwoJvQv?editors=1100) 搭配overflow 指定用户是否可以调整该元素的大小
  - none： 默认
  - both： 无法调整
  - horizontal： 可调整宽度
  - vertical： 可调整高度
- [box-sizing](https://codepen.io/xtcacti/pen/XWNYGvw) 
  - content-box：默认值 W3C标准模式 width/height = width/height(不包括padding border)
  - border-box：怪异模式 width/height = border+padding+width/height
  - inherit：从父级继承
- [outline-offset](https://codepen.io/xtcacti/pen/MWbXRWL) 搭配outline属性看效果 轮廓不占用空间
  - length： border往外的距离
  - inherit

## 弹性盒子 Flex Box
弹性盒子flexbox是CSS3的一种新的布局方式，当屏幕大小不同，设备类型不同时，采用flexbox就会对容器中的子元素进行合理的分配，合理的排列对齐，合理的分配空白。
flexbox = flex container + flex items
- [display](https://codepen.io/xtcacti/pen/ZEBRGPv)
  - flex
```
<style>
.flex-container{
    display:flex;
    width: 400px;
    height: 250px;
    background-color: #bdc3c7
}
.flex-item{
    background-color: #2980b9;
    width: 100px;
    height: 100px;
    margin: 10px;
}
</style>

<div class='flex-container'>
    <div class='flex-item'>item1</div>
    <div class='flex-item'>item2</div>
    <div class='flex-item'>item3</div>
</div>
```

- [flex-direction](https://codepen.io/xtcacti/pen/gOLKpJa)
  - row
  - row-reverse  
  - column 
  - column-reverse
```
.flex-container{
    display:flex;
    flex-direction:row;
    ...
}
```
- [justiify-content](https://codepen.io/xtcacti/pen/rNWKOar) flex-items沿着flex-container的主轴线main axis对齐
  - flex-start：  居左 不分割
  - flex-end： 居右 不分割
  - center： 居中 不分割
  - space-between： 只中间分割
  - space-around： 环绕分割
![justify-content](https://www.runoob.com/wp-content/uploads/2016/04/2259AD60-BD56-4865-8E35-472CEABF88B2.jpg)

- [align-items](https://codepen.io/xtcacti/pen/YzpvyWP) flex-items沿着flex-container的纵轴对齐
  - flex-start： 居上 items没height，延伸到自身内容的height
  - flex-end： 居下 items没height，延伸到自身内容的height
  - center： 居中 items没height，延伸到自身内容的height
  - baseline： 居上 items没height，延伸到自身内容的height
  - stretch： 居上 items没height，延伸到container的height

- [flex-wrap](https://codepen.io/xtcacti/pen/jOVKWGo) flex-container的子元素换行方式 container.width > item.width
  - nowrap：默认 item.width溢出
  - wrap：溢出的item 换行放置 断行（上下）
  - wrap-reverse：(下上)

- [align-content](https://codepen.io/xtcacti/pen/eYBKJKJ) 用于修改flex-wrap非nowrap时的行为，不是修改item的对齐，而是修改各个行的
  - stretch：默认 每一行会伸展一部分height，均匀占满空间
  - flex-start：向上挤
  - flex-end：向下挤
  - center：居中
  - space-between：中间分割
  - space-around：环绕分割

- flex-item的属性
  - [order](https://codepen.io/xtcacti/pen/bGBKEyP) 通过整数大小来定义item的排列顺序,小的在前，可以为负 
  - [margin](https://codepen.io/xtcacti/pen/oNYyxzy) 完美居中
  - [align-self](https://codepen.io/xtcacti/pen/qBqKZqY) 设置item自身在纵轴上的一个对齐方式
    - auto
    - flex-start
    - flex-end
    - center
    - baseline
    - stretch
  - [flex](https://codepen.io/xtcacti/pen/xxRzVdW) flex-item如何分配空间



## 多媒体查询 Media Quiery
[@media](https://codepen.io/xtcacti/details/QWGxNXv)
```
@media not|only mediatype and(expresstions){
    CSS code...;
}
```
操作符
- not
- only

多媒体类型
- all：所有多媒体设备
- print：打印机
- screen：电脑、平板、智能手机
- speech：屏幕阅读器

> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除