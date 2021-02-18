---
title: HTML5
date: 2021-02-05 17:07:42
tags: HTML
---

## HTML5 标签

- 布局标签、语义化标签
  - `<header>`
  - `<nav>`
  - `<section>`
  - `<article>`
  - `<aside>`
  - `<footer>`
  - `<details>`
  - `<summary>`
- 表单
 - `<datalist id="hello">`为`<input list="hello">`规定预定义选项
 - `<keygen>`
 - `<output>`

- 多媒体
  - `<embed>` 添加HTML插件的容器
  - `<audio> <video>` 音频、视频
    - `controls=''`: 添加播放暂停、音量控件
    - `source=''`: 允许添加多个source，使用第一个可识别格式
    - `autoplay=''`：自动播放
    - `preload=''`: 若有autoload忽略此属性
    - [video标签还有一些属性 方法和事件...](https://www.w3school.com.cn/html5/html_5_video_dom.asp)
    - video标签之间的文本是在不支持的浏览器中显示的
---
## HTML表单属性
- `<form>`属性：
  - autocomplete
  - novalidate
- `<input>`属性：
  - autocomplete
  - autofocus
  - placeholder
  - required
---
## HTML拖放
1. 被拖动的元素要首先设置为可拖动
2. 触发开始拖动的事件，把被拖元素的数据类型和值给到事件
3. 拖到到目的地的元素数据，(默认元素是不允许被拖动的)所以需组织对元素的默认处理
4. 放置被拖动元素，触发drop事件(默认drop是以链接的方式打开)，所以组织默认处理，获得被拖元素，放置被拖元素
```
<body>
<img id='drag1' src='' draggable='true' ondragstart='drag(event)'>
<div id='div1' ondrop='drop(event)' ondragover='allowDrop(event)'>
</body>

<script>
function drag(event){
  event.dataTransfer.setData('Text',event.target.id);
}
function allowDrop(event){
  event.preventDefault();
}
function drop(event){
  event.preventDeafult();
  var data = event.dataTransfer(event).getData('Text');
  event.target.appendChild(document.getElementById(data));
}
</script>
```
---
## HTML canvas & HTML svg
### HTML canvas
- HTML5的canvas元素使用Javascript在网页上绘图，可以控制每一像素
- 规定canvas元素的id、宽度、高度
  `<canvas id='mycanvas' width='200' height='200'></canvas>`
- canvas本身没有绘图的能力，绘图工作其实都是js完成的
  ```
  <script type='text/javascript'>
  var c = document.getElementById('mycanvas'); //寻找元素
  var cxt = c.getContext('2d'); //创建对象
  cxt.fillStyle('#FF0000'); //红色
  cxt.fillRect(0,0,150,75); //矩形
  </script>
  ```
- 还可以画线条、圆、渐变色、图片...

### HTML svg
- SVG - Scalable Vector Graphics 可伸缩 矢量 图形
- 使用XML定义图形
- 改变尺寸图形质量不损失
- 可通过文本编辑器创建、修改
- 可被搜索、索引、脚本化、压缩
- 可伸缩
- 不失真
- 可添加js事件处理器
---
## HTML 地理定位

---

## HTML Web存储
- localStroage: 没有时间限制的数据存储
- sessionStorage: 针对一个session的数据存储，关闭浏览器，数据删除
---
## HTML 应用程序缓存
- 使用HTML5、创建cache manifest文件->轻松创建web应用离线版本
- 优势：
  - 离线浏览
  - 速度快：资源已经缓存了加载快
  - 渐少服务器负载：浏览器只从服务器下载更新或更改的的资源
- 使用：
  - 添加属性：`<html manifest='demo.appcache'></html>`
  - web服务器上配置manifest文件
- manifest文件组成：
  - CACHA MANIFEST - 要缓存的
  - NETWORK - 不缓存的
  - FALLBACK - 页面访问不了的返回页面
  ```
  CACHE MANIFEST
  # 2012-02-21 v1.0.0
  /theme.css
  /logo.gif
  /main.js

  NETWORK:
  login.asp

  FALLBACK:
  /html5/ /404.html
  ```
- 什么情况缓存会发生改变？
  - 用户清空浏览器缓存
  - manifest文件被修改
  - 程序更新缓存
- 为确保浏览器缓存与服务器内容一致，一旦更新服务器文件，务必更改manifest文件 
---
## HTML Web Worker
[ref here](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)

---
## HTML server sent event
[ref here](http://www.ruanyifeng.com/blog/2017/05/server-sent_events.html)

> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除
