---
title: CSS
date: 2021-02-18 08:20:42
tags:
---

## CSS是什么？
- Cascading Style Sheet (层叠样式表)
- 样式表就是如何显示HTML元素
- 外部样式表工作效率高
- 样式可保存在：
  - 单个HTML元素中
  - HTML页的头元素中
  - 一个外部的CSS文件中
- 多种样式作用于同一个HTML元素时将层叠为一个，层叠顺序：
  - 浏览器缺省设置 (低)
  - 外部样式表
  - 内部样式表
  - 内联样式表 (高)
---

## CSS语法
- 选择器 + 一条或多条声明(属性+值) 
  ![CSS语法](https://www.w3school.com.cn/i/ct_css_selector.gif)
- 写法：
  ```
  body {
  color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, serif;
  }
  ```
- 选择器分组写法：
  ```
  h1,h2,h3,h4,h5,h6 {
  color: green;
  }
  ```
- 继承
  - 子元素会默认继承最高级元素所拥有的属性
  - 子元素想拥有自己的属性，可针对子元素单独创建CSS规则
---

- 派生选择器(上下文选择器):根据元素在其位置的上下文关系来定义样式
  ```
  li strong {
    font-style: italic;
    font-weight: normal;
  }
  ```
  ```
  <p><strong>我是粗体字，不是斜体字，因为我不在列表当中，所以这个规则对我不起作用</strong></p>
  <p><strong>我是粗体字，不是斜体字，因为我不在列表当中，所以这个规则对我不起作用</strong></p>
  <ol>
  <li><strong>我是斜体字。这是因为 strong 元素位于 li 元素内。</strong></li>
  <li>我是正常的字体。</li>
  </ol>
  ```
## id选择器
- id选择器以`#`来定义(id在元素中必须是唯一的)
  ```
  #red {color:red;}
  #green {color:green;}
  ```
  ```
  <p id="red">这个段落是红色。</p>
  <p id="green">这个段落是绿色。</p>
  ```
- id选择器常常用于建立派生选择器，当然也可以用于单独的
  ```
  #sidebar p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}
  ```

## 类选择器
- 类选择器以`.`来定义(class可以不是唯一的)
  ```
  .red {color:red;}
  ```
  ```
  <h1 class="red">这个段落是红色。</p>
  <p class="red">这个段落是红色。</p>
  ```
- 类选择器用法：
  - 用于派生
  ```
  .fancy td {
	color: #f60;
	background: #666;
	} 
  ```
  - 基于元素
  ```
  td.fancy {
	color: #f60;
	background: #666;
	} 
  ```
## 属性选择器
- 对带有指定属性的HTML元素设置样式，而不仅限于class和id，通常用于设置表单样式
- `[attribute]`:选取有这个属性的
- `[attribute=value]`:选取属性是这个value的
- `[attribute~=value]`:选取属性值包含这个value的，value是一个词汇
- `[attribute|=value]`:选取属性值以这个value开头的，value是一个词汇
- `[attribute^=value]`:匹配以这个value开头的
- `[attribute$=value]`:匹配以这个value结束的
- `[attribute*=value]`:匹配属性值中包含这个value的
  ```
  [title]
  {
   color:red;
  }
  ```
  ```
  <h2 title="Hello world">Hello world</h2>
  ```

---
## 如何创建CSS
- 外部样式表
 ```
 <head>
 <link rel="stylesheet" type="text/css" href="mystyle.css" />
 </head>
 ```
- 内部样式表
 ```
 <head>
 <style type="text/css">
   hr {color: sienna;}
   p {margin-left: 20px;}
   body {background-image: url("images/back40.gif");}
 </style>
 </head>
 ```
- 内联样式 `慎用`
 ```
 <p style="color: sienna; margin-left: 20px">
 This is a paragraph
 </p>
 ```

- 多重样式层叠

---

## CSS样式

### CSS背景
- `background-color` 背景色,不能继承,默认值是transparent
- `background-image` 背景图像,不能继承,默认值是none
- `background-repeat` 在页面上对背景图像进行平铺
- `background-position` 改变图像在背景中的位置
- `background-attachment` 声明背景相对于文字滚动还是固定，默认是scroll
  ```
  body{
      background-image:url(eg.png);
      background-repeat:repeat-x; //repeat-y repeat no-repeat
      background-position:center; //top bottom left right center 100px 5cm
      background-attachment:fixed;
  }
  ```
- `background` 简写属性
  ```
  body{
      background:#00FF00 url(image.png) no-repeat fixed top;
  }
  ```


### CSS文本
- `color`： 文本颜色
- `word-spacing`： 字间距,默认值normal也就是0，正值拉远，负值拉近
- `letter-spacing`： 字母间距，修改字符与字母之间的间距
- `text-align`： 对齐文本,`left right center justify`
- `tetx-decoration`： 装饰文本,`none underline overline line-through  blink`
- `text-indent`： 文本缩进,可继承，作用于块元素 
- `text-transform`： 处理文本的大小写 `none uppercase lowercase capitalize`
- `white-space`： 处理空白符
  - `normal` - 不换行 不空格 自动换行
  - `pre` - 换行 空格 不自动换行
  - `nowrap` - 不换行 不空格 不自动换行
  - `prewrap` - 换行 空格 自动换行
  - `pre-line` - 换行 不空格 自动换行
- `direction`：文本方向，文本显示方向，默认值ltr `ltr rtl`
  - 行内元素前提 `unicode-bidi:embed | unicode-bidi:bidi-override`
- ...

### CSS字体
- `font-family`:可以一次罗列多种字体，用户代理不适用时会往后选
- `font-style`:用于规定斜体文本 `normal italic oblique`
- `font-variant`:设置小型大写字母 `small-caps`
- `font-weight`:设置文本的粗细 `normal bold 900`
- `font-size`:字体大小，与标题元素两回事，`60px 3.75em`
### CSS链接
### CSS列表
### CSS表格
### CSS轮廓


