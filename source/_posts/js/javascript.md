---
title: Javascript
date: 2021-02-20 15:57:23
tags: Javascript
---

## Javascript能做咩？
HTML无非不过是元素标签、内容、属性，js却可以做到改变...
- ...HTML内容
  ```
  document.getElementById('demo').innerHTML='Hello Js';
  ```
- ...HTML属性:获取元素再点属性
  ```
  document.getElementById('demo').src='';
  ```
- ...HTML样式:获取元素点style点样式
  ```
  document.getElemtnById('demo').style.fontSize='24px';
  ```
- ...隐藏显示HTML元素
  ```
  document.getElementById('demo').style.display='none';
  document.getElementById('demo').style.display='block';
  ```
---

## JS输出
- `document.write()`
- `console.log()`
- `window.alert()`
- `innerHTML`

## JS注释
- 单行注释：//
- 多行注释：/* */

---
## JS数据类型
- 原始数据
  - 字符串
  - 数值
  - 布尔
  - undefined
- 复杂数据
  - function
  - object (对象，数组，null)
- typeof 运算符
- undefined：没有值的变量，其值是undefined 可以通过赋值undefined来清空对象
- 空值：就是字符串""
- Null：不存在的事物，数据类型为对象 可以通过赋值null来清空对象
- undefined 和 null数据类型不同，值相同
  ```
  typeof undefined;     //unfined
  typeof null;      //object
  null === undefined;       //false  === 比较类型和值
  null == undefined;        //true   ==  比较值
  ```


### JS函数
- 定义：
  ```
  function name(parameter1,parameter2){
      ...
      var a = 1; //a是局部变量，仅在函数开始时被创建，函数结束时被删除
      return;
  }
  ```
- 调用：
  ```
  name(argument1,argument2);
  ```
- name -> 引用的是函数对象
- name() -> 引用的是函数结果
- var result = name(); -> 可以被函数结果赋值给一个变量

### JS对象
- `var a = 1;` -> 单一值赋值给一个变量
- ```
  var person = {
      firstName = "First";
      lastName = "Last";
      fullName:function(){
          return this.firstName + " " +this.lastName;  //this:拥有者
      }
  } -> 把多个值赋值给一个变量
  ``` 
- JS对象无非不过是一个容器，可以存储多个属性和方法
- 不要使用以下写法，否则该变量会被创建为对象,会拖慢执行速度
  ```
  var x = new String();
  var y = new Number();
  var z = new Boolean();
  ```


### JS字符串
var str = "hello world";
- 内建属性：
  - str.length; //11
- 方法：
  - str.indexOf('o'); //4 -> 指定文本首次出现的位置，从0开始 -1则没有出现
  - str.indexOf('o',1); //3
  - str.lastIndexOf('o'); //7 ->指定文本最后一次次出现的位置，从0开始 -1则没有出现
  - str.lastIndexOf('o'); //6
  - str.search('o'); //4
  - `indexOf() VS search()`
    - serach()：无法设置第二个参数，但是可以设置更强大的搜索值，正则表达式
    - indexOf()：可以设置第二个参数，但是无法设置正则表达式...
  - str.slice(0,5); //hello -> 返回被提取部分的字符串，参数起始位置，结束位置
  - str.slice(-5,-1); //worl -> 若参数为负，则从结尾开始计数
  - str.slice(2); //llo world -> 截取字符串剩余部分
  - `substring() VS slice()`
    - substring()类似于slice()，但是无法赋予负值
  - str.substr(0,3); //hel
  - `substr() VS slice()`
    - substr()类似于slice()，只是substr()第二个参数代表被提取部分的长度
  - str.replace('world','cacti'); //hello cacti -> 匹配首个单词进行替换
  - str.replace(/world/i,'cacti'); //hello cacti -> /i大小写不敏感匹配并替换
    - /i -> 大小写不敏感匹配并替换
    - /g -> 全局搜索并替换
  - str.toUpperCase(); //HELLO WORLD
  - str.toLowerCase(); //hello world
  - str.concat(" yes"); //hello world yes ->concat相当于+运算符
  - str.trim(); // ->删除字符串两端的空格
  - str.charAt(0); //h -> 返回指定下标的字符
  - str.charCodeAt(0); //104 -> 返回指定下标的字符的unicode编码
  - str[0] //h ->ES5支持
  - str.splite(" ") //['hello','world'] -> 通过分隔符分隔返回数组
  - str.splite() //hello world ->省略分隔符，返回本身

### JS数字
var x = 125;
- 方法：
  - x.toString(); //"125"
  - x.toExponential(1); //1.3e+2 -> 返回四舍五入后的指针计数法的数字
  - x.toFixed(2); //"125.00" -> 返回四舍五入后的指定小数位数的数值字符串
  - x.toPrecision(6); //"125.000" -> 返回四舍五入后的指定数字长度的字符串
  - x.valueOf(); //125 -> 所有JS数据类型都有valueOf()和toString()方法

### 变量