---
title: HTML基础
date: 2021-02-05 14:51:21
tags: HTML
---

## HTML 是什么？

- Hyper Text Markup Language
- 不是一种编程语言，是一种标记语言
- HTML 是一套标记标签，通过标记标签来描述网页
- HTML 文档=网页
- Web 浏览器的作用就是读取 HTML 文档，进而展示成网页

---

## HTML 标签
- HTML头部 `<head>`
  - 页面标题，工具栏的标题，被收藏的标题，搜索引擎的标题 `<title>`
  - 页面上所有链接的默认地址或默认目标 `<base>`
  - 定义文档与外部资源的关系 `<link>`
  - 内部样式表方式 `<style>`
  - 定义元数据，用于搜索引擎 `<meta>`
  - 定义客户端脚本 `<script>`
- HTML 标题 主->次 `<h1> <h2> <h3> <h4> <h5> <h6>`
  - 效果展示之用
  - 搜索引擎 编排索引之用
- HTML 段落 `<p>`
- HTML 链接 `<a>`
- HTML 图像 `<img>`
- 定义 HTML 文档主体 `<body>`
- 定义 HTML 整个文档 `<html>`
- 换行(空元素) `<br />`
- 创建水平线(空元素) `<hr />`
- 文本格式化标签
  - 粗体文本 `<b>`
  - 大号字 `<big>`
  - 着重文字 `<em>`
  - 斜体字 `<i>`
  - 小号字 `<small>`
  - 加重语气 `<strong>`
  - 下标字 `<sub>`
  - 上标字 `<sup>`
  - 插入字 `<ins>`
  - 删除字 `<del>`
- 引用和术语定义
  - 长引用: 缩进处理 `<blockquote>`
  - 短引用：引号处理 `<q>`
  - 缩略词：搭配属性`title`使用,为搜索引擎提供有用信息 `<abbr> <dfn>`
  - 联系信息：`<address>`
  - 著作标题：`<cite>`
  - 双向重写：`<bdo>`
- 表格
  - 表格 `<table>`
  - 表格标题 `<caption>`
  - 表头 `<th>`
  - 行 `<tr>`
  - 单元格 `<td>`
  - 页眉 `<thead>`
  - 主体 `<tbody>`
  - 页脚 `<tfoot>`
  - 表格列属性 `<cal>`
  - 表格列的组 `<colgroup>`
- 列表 
  - 有序列表 `<ol> <li>`
    - `type='A/a/1'`
  - 无序列表 `<ul> <li>`
    - `type='disc/circle/square'`
  - 定义列表 `<dl> <dt> <dd>`
  - 嵌套列表
- 分区(块元素)：`<div>`
- 文本(行内元素)：`<span>`
- HTML框架：一个浏览器窗口展示不止一个页面
  - 框架集 `<frameset>`
  - 框架`<frame>`
- HTML脚本: 定义客户端脚本
  - 定义客户端脚本`<script>`
  - 不支持客户端脚本的替代内容`<noscript>`
- HTML表单：定义用户不同的类型输入 
  - `<form action="" method="">`
    - action属性：表单处理程序的服务器页面，省略则设置为当前页面
    - method属性：提交表单时所用的http方法 `get post ...`
  - 文本输入、单选/多选按钮输入、提交按钮：通过`<input>`的属性`type`决定
    - `type="text"`
    - `type="password"`：掩码处理
    - `type="radio"`：单选
    - `type="checkbox"`: 复选框
    - `type="sumbit"`
    - `type="..."`:还有一大堆type值 参考[w3school](https://www.w3school.com.cn/html/html_form_input_types.asp)去吧
    - `name=""`:要被正确提交，就必须设置name属性
    - `value=""`:规定输入字段的初始值
    - `...=""`:还有一大堆属性 参考[w3school](https://www.w3school.com.cn/html/html_form_attributes.asp)去吧
  - 下拉列表 `<select>`
    - 下拉列表选项 `<option>`
  - 文本域，即可输入多行字段 `<textarea>`
  - 按钮 `<button>`
  - 组合相关表单 `<fieldset>`
  - 为`<fieldset>`定义标题 `<legend>`
- 支持HTML助手(插件) `<object>` 音频视频之类的
- 
- 强制：所有元素标签使用小写
- 强制：所有元素添加闭合标签
- 废弃标签：~~`<center>`~~ ~~`<font>`~~ ~~`<basefont>`~~ ~~`<s>`~~ ~~`<strike>`~~ ~~`<u>`~~ ~~`<menu>`~~
- ......

### 块元素 vs 行内元素
- 块：`<div> <h1>... <p> <ul> <table>`
- 行内：`<span> <b> <td> <a> <img>`
- 典型的就是`<div>`和`<span>`，前者通常用来布局，后者用来文本分类统一定制样式
---

## HTML 元素

- 指从开始标签到结束标签的所有内容
  - 开始标签
  - 元素内容 (连续空格被标识为一个空格，包括换行)
  - 结束标签

---

## HTML 属性

- 提供 HTML 元素的更多信息
- 键值对形式展现 `name='value'`
- 总在开始标签中
- 强制：属性和属性值小写
- 强制：属性值包括在引号内(单双都可) `name='"Hello" xtcacti'`
- 废弃属性：~~`align`~~ ~~`bgcolor`~~ ~~`color`~~

---

## HTML 注释

- `<!-- comment-->`
- 条件注释`<!--[if IE 8]> ... <!<endif>--> `
---
## HTML 链接
- 本窗口 `<a href='https://www.baidu.com/'>`
- 新窗口打开文档 `<a href='https://www.baidu.com/' target='_blank'>`
- 锚点跳转 `<a name='锚名'> <a href='#锚名'>`
- 链接始终要书写到子文件下，避免服务器多发一次请求
---
## HTML 图像
- `<img src='图像源' alt='替换文字'>`
- 加载图片是需要时间的，所以慎用图片
--- 
## HTML 响应式Web设计
- RWD：Responsive Web Design
- RWD可以改变尺寸传递网页
- RWD对于平板和移动设备是必须的
- Bootstrap是最流行的开发RWD的框架
- 老式浏览器，可将脚本放在注释中

## HTML实体字符
- 比如使用`<` `>`会被浏览器误认为是标签，所以就定制了实体字符 e.g.：空格：`&nbsp`

## HTML URL
- URL用来定位万维网上的文档或其他数据
- 语法规则：`scheme://host.domain:port/path/filename`
  - scheme:因特网服务类型：http https file
  - host:域主机：默认www
  - domain:因特网域名：w3school.com.cn
  - :port:主机上的端口号: http默认80
  - 服务器上的路径,若省略则在服务器根路径上
  - filename:顾名思义吧~~~
- URL编码
  - URL只能用ASCII通过因特网进行发送
  - 非ASCII字符通过%加两位十六进制来转变
  - 空格用 + 来转

## HTML <!DOCTYPE>
- 不同的文档类型，不同的HTML版本信息都是通过<!DOCTYPE>传递的
- e.g. HTML5：`<!DOCTYPE html>`

> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除
