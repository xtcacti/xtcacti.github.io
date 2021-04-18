---
title: leetcode
date: 2021-03-19 20:18:07
tags: algorithm
---

## 时间复杂度 & 空间复杂度
评估一个算法的性能有两个指标：执行事件、内存消耗。
通常服务端更关注执行时间，因为内存消耗可以回收，而且用户也不care你服务器端到底占用了多大空间。
leetcode采用的是事后评估法，采用更多的是事前评估 - 大O复杂度表示法，也就引出了两个概念：
- (渐进)时间复杂度
- (渐进)空间复杂度
- 渐进：当输入规模成倍数增加的时候，相应的时间空间消耗增加了多少
- 时间复杂度和空间复杂度通常不能同时最优，不是有种说法：时间换取空间、空间换取时间，一般选后种，毕竟空间是可以回收的、也可以用钱买么
e.g.
- 从1依次加到100 VS 从1依次加到10000
- 高斯算法 (1+100)*100/2  V$ (1+10000)*10000/2

## 二分查找 - 减而治之
- e.g.
  - [猜数字]
  - [查字典]
  - [debug打印输出语句]
- 应用：
  - 有序数组中查找一个数 - 二分下标
  - 整数范围内查找一个整数 - 二分答案
  - (有序数组 也可以是旋转数组或山脉数组，都是有规律可循的，都可以用二分查找)

     