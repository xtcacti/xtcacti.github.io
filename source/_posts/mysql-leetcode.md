---
title: mysql-leetcode
date: 2021-04-22 17:01:55
tags: mysql
---

## 176.第2高薪水
```
SELECT IFNULL((
    SELECT DISTINCT Salary
    FROM Employee
    ORDER BY Salary DESC
    LIMIT 1,1
),NULL) 
AS SecondHighestSalary
``` 

## 177.第N高薪水
- 经典排序问题：
1. row_number() - 连续排名，3000、2000、2000、1000 -> 1,2,3,4
2. rank() - 同薪同名不连续，3000、2000、2000、1000 -> 1,2,2,4
3. dense_rank() - 同薪同名连续，3000、2000、2000、1000 -> 1,2,2,3
4. ntile() - 分桶排名，即首先按桶的个数分出第一二三桶，然后各桶内从1排名，实际不是很常用
- 第3种实现：
1. 窗口函数
2. `LIMITE` 后面只能接正整数，变量表达式负数0都不可以
3. `GROUP BY` 给同薪分组
```
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
SET N := N-1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT IFNULL((
          SELECT DISTINCT Salary
          FROM Employee
          GROUP BY Salary
          ORDER BY Salary DESC
          LIMIT N,1
      ),NULL)
  );
END
```

## 178.分数排名
```
SELECT 
    Score,
    dense_rank() over(ORDER BY Score DESC) AS 'Rank'
FROM Scores
```
