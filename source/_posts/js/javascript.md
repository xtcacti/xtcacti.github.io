---
title: Javascript
date: 2021-02-20 15:57:23
tags: Javascript
---

## Javascript 能做咩？

HTML 无非不过是元素标签、内容、属性，js 却可以做到改变...

- ...HTML 内容
  ```
  document.getElementById('demo').innerHTML='Hello Js';
  ```
- ...HTML 属性:获取元素再点属性
  ```
  document.getElementById('demo').src='';
  ```
- ...HTML 样式:获取元素点 style 点样式
  ```
  document.getElemtnById('demo').style.fontSize='24px';
  ```
- ...隐藏显示 HTML 元素
  ```
  document.getElementById('demo').style.display='none';
  document.getElementById('demo').style.display='block';
  ```

---

## JS 输出

- `document.write()`
- `console.log()`
- `window.alert()`
- `innerHTML`

## JS 注释

- 单行注释：//
- 多行注释：/\* \*/

---

## JS 数据类型

- 原始数据
  - 字符串
  - 数值
  - 布尔
  - undefined
- 复杂数据
  - function
  - object (对象，数组，null)
- typeof 运算符
- undefined：没有值的变量，其值是 undefined 可以通过赋值 undefined 来清空对象
- 空值：就是字符串""
- Null：不存在的事物，数据类型为对象 可以通过赋值 null 来清空对象
- undefined 和 null 数据类型不同，值相同
  ```
  typeof undefined;     //unfined
  typeof null;      //object
  null === undefined;       //false  === 比较类型和值
  null == undefined;        //true   ==  比较值
  ```

### JS 函数

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

### JS 对象

- `var a = 1;` -> 单一值赋值给一个变量
- 对象:

  ```
  var person = {
      firstName = "First";
      lastName = "Last";
      fullName:function(){
          return this.firstName + " " +this.lastName;  //this:拥有者
      }
  } -> 把多个值赋值给一个变量
  ```

- JS 对象无非不过是一个容器，可以存储多个属性和方法
- 不要使用以下写法，否则该变量会被创建为对象,会拖慢执行速度

  ```
  var x = new String();
  var y = new Number();
  var z = new Boolean();
  ```

### JS 字符串

var str = "hello world";

- 内建属性：
  - str.length; //11
- 方法：
  - str.indexOf('o'); //4 -> 指定文本首次出现的位置，从 0 开始 -1 则没有出现
  - str.indexOf('o',1); //3
  - str.lastIndexOf('o'); //7 ->指定文本最后一次次出现的位置，从 0 开始 -1 则没有出现
  - str.lastIndexOf('o'); //6
  - str.search('o'); //4
  - `indexOf() VS search()`
    - serach()：无法设置第二个参数，但是可以设置更强大的搜索值，正则表达式
    - indexOf()：可以设置第二个参数，但是无法设置正则表达式...
  - str.slice(0,5); //hello -> 返回被提取部分的字符串，参数起始位置，结束位置
  - str.slice(-5,-1); //worl -> 若参数为负，则从结尾开始计数
  - str.slice(2); //llo world -> 截取字符串剩余部分
  - `substring() VS slice()`
    - substring()类似于 slice()，但是无法赋予负值
  - str.substr(0,3); //hel
  - `substr() VS slice()`
    - substr()类似于 slice()，只是 substr()第二个参数代表被提取部分的长度
  - str.replace('world','cacti'); //hello cacti -> 匹配首个单词进行替换
  - str.replace(/world/i,'cacti'); //hello cacti -> /i 大小写不敏感匹配并替换
    - /i -> 大小写不敏感匹配并替换
    - /g -> 全局搜索并替换
  - str.toUpperCase(); //HELLO WORLD
  - str.toLowerCase(); //hello world
  - str.concat(" yes"); //hello world yes ->concat 相当于+运算符
  - str.trim(); // ->删除字符串两端的空格
  - str.charAt(0); //h -> 返回指定下标的字符
  - str.charCodeAt(0); //104 -> 返回指定下标的字符的 unicode 编码
  - str[0] //h ->ES5 支持
  - str.splite(" ") //['hello','world'] -> 通过分隔符分隔返回数组
  - str.splite() //hello world ->省略分隔符，返回本身

### JS 数字

-数字属性：

- Number.MAX_VALUR;
- Number.MIN_VALUE;
- Number.POSITIVE_INFINITY;
- Number.NEGATIVE_INFINITY;
- Number.NaN;
- var x = Number.NEGATIVE_INFINITY; //undifined -> 数字属性不可赋值给变量

var x = 125;

- 方法：
  - x.toString(); //"125"
  - x.toExponential(1); //1.3e+2 -> 返回四舍五入后的指针计数法的数字
  - x.toFixed(2); //"125.00" -> 返回四舍五入后的指定小数位数的数值字符串
  - x.toPrecision(6); //"125.000" -> 返回四舍五入后的指定数字长度的字符串
  - x.valueOf(); //125 -> 所有 JS 数据类型都有 valueOf()和 toString()方法

### 变量转换为数值

全局方法

- Number();
  - Number(false); //0
  - Number(true); //1
  - Number("10"); //10
  - Number("10 20 30"); //NaN ->无法转换为数字就返回 NaN(Not a Number)
  - Number(new Date("2021/2/23")); //1614009600000
- parseInt(); ->解析字符串，并返回首个数字
  - parseInt("10"); //10
  - parseInt("10.56"); //10
  - parseInt("10 20 30"); //10
  - parseInt("10 years"); //10
  - parseInt("years 10"); //NaN
- parseFloat(); ->解析字符串，并返回首个数字
  - parseFloat("10"); //10
  - parseFloat("10.56"); //10.56
  - parseFloat("10 20 30"); //10
  - parseFloat("10 years"); //10
  - parseFloat("years 10"); //NaN

### JS 数组

创建数组

- `var x = [1,2,3];`
- `var x = new Array(1,2,3);` // ->不建议使用(简洁、可读、执行速度)

访问数组

- `x[0];`

更改数组元素

- `x[0]='first'`
- `x[x.length-1]='last'`

添加元素 -> 在数组的末尾添加一个元素

- `x.push('yes');`
- `x[x.length]='yes'`
- `x[10]='ok'` // -> 在数组的指定位置添加元素，中间没有元素的都是 undefined

遍历数组

- for

```
for(i=0;i<x.length;x++>){
    x[i];
}
```

- forEach()

```
var txt = '';
var number = [1,4,3,2,5];
number.forEach(myFunction);

function myFunction(value,index,array){
    txt = txt + value + '</br>';
}
```

- map()

```
var number = [1,4,3,2,5];
number.map(myFunction);

function myFunction(value){
    return value * 2;
}
```

- filter()

```
var number = [1,4,3,2,5];
number.filter(myFunction);

function myFunction(value){
    return value > 2;
}
```

- reduce()

```
var number = [1,4,3,2,5];
number.mareducrp(myFunction,100); //100初始值

function myFunction(total,value){
    return total + value;
}
```

- every()

```
var number = [1,4,3,2,5];
number.every(myFunction);

function myFunction(value){
    return value > 4;  //false
}
```

- some()

```
var number = [1,4,3,2,5];
number.some(myFunction);

function myFunction(value){
    return value > 4;  //true
}
```

- indexOf()

```
var number = [1,4,3,2,5];
number.indexOf(1); //0 -> 返回参数值所在数组的索引位置，第一位是0
```

```
var number = [1,4,3,2,5];
number.indexOf(1，3); //-1 -> 第二个参数为起始搜索位置
```

- lastIndexOf() -> 从后向前搜索

- find()

```
var number = [1,4,3,2,5];
number.find(myFunction);

function myFunction(value){
    return value > 2;  //4 -> 返回符合条件的第一个值
}
```

- findIndec()

```
var number = [1,4,3,2,5];
number.findIndec(myFunction);

function myFunction(value){
    return value > 2;  //1 -> 返回符合条件的第一个值的索引
}
```

如何识别数组

- ES5 方法：`Array.isArray(x);`
- 自己创建方法：
  ```
  function isArray(x){
      return x.constructor.toString().indexOf("Array") > -1;
  }
  ```
- instanceof 运算符：
  ```
  x instanceof Array; //true
  ```

数组方法：
var arr = ['aaa','bbb','ccc','ddd'];

- `arr.toString();` //'aaa,bbb,ccc,ddd'
- `arr.join(' @ ');` //'aaa @ bbb @ ccc @ ddd'
- `arr.pop();` //'ddd' -> 从数组删除最后一个元素并返回删除的元素
- `arr.push('eee');` //5 -> 从数组末尾添加若干个元素并返回数组的长度
- `arr.shift();` //'aaa' -> 从数组第一位移除一个元素并返回移除的元素，其他元素索引减 1
- `arr.unshift('eee');` //5 -> 从数组第一位添加元素并返回数组的长度，其他元素索引加 1
- `delete arr[0];` //true -> delete 把数组指定索引元素删除，置为 empty
- `arr.splice(1,3,'111','222');` //['bbb','ccc','ddd'] -> 返回删除的元素，从索引 1 删掉 3 个元素，并加入'111'，'222'两个元素
  - 参数 1:拼接新元素的位置
  - 参数 2：删除多少个元素
  - 其余参数：定义要添加的元素
- `arr.splice(1,3);` //['bbb','ccc','ddd'] -> 返回删除的元素，从索引 1 删掉 3 个元素
- `arr.concat('hello','hi')`;//['aaa','bbb','ccc','ddd','hello','hi'] -> 数组合并，不改变原来数组，返回一个新的数组
- `arr.slice(1);` //['bbb'] -> 从 arr 中截取元素生成新的数组，不改变原有数组
- `arr.slice(1,3);` //['bbb','ccc'] -> 其实索引，终止索引，前闭后开 [1,3)

var arr = [1,4,2,3];

- `arr.sort();` //1,2,3,4
- `arr.reverse();` //4,3,2,1
- `arr.sort(function(a,b){return a-b});` //1,2,3,4
- `arr.sort(fucntion(a,b){return b-a});` //4,3,2,1
- `arr.sort(function(){return 0.5 - Math.random()});` // -> 随机排序

## JS 日期

var d = new Date(年，月，日，时，分，秒，毫秒);

- 其中只有 getDate()获取几号是从 1 开始。
- JS 日期将存储为自 1970 年 1 月 1 日 00:00:00 UTC 以来的毫秒数.
  |format |out|
  |:----|:----|
  |d.toDateString()| "Sun Feb 28 2021"|
  |d.toGMTString()| "Sun, 28 Feb 2021 13:44:38 GMT"|
  |d.toISOString()|"2021-02-28T13:44:38.173Z"|
  |d.toUTCString()|"Sun, 28 Feb 2021 13:44:38 GMT"|
  |d.toLocaleDateString()|"2/28/2021"|
  |d.toLocaleTimeString()|"9:44:38 PM"|
  |d.toLocaleString()|"2/28/2021, 9:44:38 PM"|

## JS Math

- Math.round(3.4); //3 -> 四舍五入
- Math.pow(2,3); //8 -> 2 的 3 次方
- Math.sqrt(64); //8 -> 64 的开方
- Math.abs(-3); //3 -> -3 的绝对值
- Math.ceil(3.4); //4 -> 3.4 入(天花板)
- Math.floor(3.6); //3 -> 3.6 舍(地板)
- Math.random(); //返回 [0,1) 之间的随机数
- Math.floor()和 Math.randon()一起用：
  - Math.floor(Math.random()\*10); //[0,9]
  - Math.floor(Math.random()\*10)+1; //[0,10]
  - Math.floor(Math.random()\*11); //[0,10]
  - Math.floor(Math.random()\*(max-min))+min; //[min,max)
  - Math.floor(Math.randon()\*(max-min+1))+min; //[min,max]

## Hoisting & 严格模式

- Hoisting:变量提升 var，可以先使用变量再声明变量
- 严格模式："use strict;" 禁止使用坏语法



> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除
