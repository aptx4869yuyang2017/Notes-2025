---
created: 2024-03-27
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "08"
finished:
---

![400](https://s1.vika.cn/space/2024/03/27/cc41ae99f6034290b2b5645e9a915156)
![400](https://s1.vika.cn/space/2024/03/27/c940ec747d6b44d88d010cabb37a0a84)

## 介绍时间智能


## 构建日期表

![400](https://s1.vika.cn/space/2024/03/27/dff831b108a548c395f27f48a557baf8)


## 理解基础时间智能计算

![400](https://s1.vika.cn/space/2024/03/27/7471b36bcf0f40889bdd38c309cbe372)


- 对日期表的筛选，对一列移除筛选就是对整个日期表移除筛选

## 理解基础时间智能函数

![400](https://s1.vika.cn/space/2024/03/27/f51741720c5948428a0dc774ef287638)
![400](https://s1.vika.cn/space/2024/03/27/710f1256f6554dcdba04875d93860894)

- DateYTD 本质上是一个**表函数**
	- Filter All(date)
	- 日期范围
- 实现了对 计算时间范围的控制

#### YTD/QTD/MTD



#### 对比同期

![600](https://s1.vika.cn/space/2024/03/28/68077ef44979467c824e6cc523a8b63d)

- DateAdd 是一个表函数
- 输入 日期列 / 平移数量 / 平移时间单位
- 输出：根据筛选上下文的日期范围，返回一个新的平移后的日期参数

![600](https://s1.vika.cn/space/2024/03/28/140c91e9692f4996ba3b00004d8406da)

- 给当前筛选上下文的范围，平移制定的日期距离(和DateAdd功能相同的部分)
- 当给定部分日期范围，仍旧能够返回完整的一个单位的时间范围


#### 混合时间智能函数

- 本质上，只写一个字段是语法糖
	- 完整版本第一个参数需要一个表

![400](https://s1.vika.cn/space/2024/03/28/ab1cebca6be04771aa77c5cb4cf79b17)


- 可以嵌套函数（嵌套表）
- 也可以嵌套字段

![400](https://s1.vika.cn/space/2024/03/28/a5c5e57644964cdd870e81d5395316e0)

![400](https://s1.vika.cn/space/2024/03/28/ae072eefbac14614a624c065bdb4db59)
![400](https://s1.vika.cn/space/2024/03/28/b14100871b6c4e1ea0aae4b3cbeff13d)
#### 嵌套时间智能的正确顺序(日期表不完整)



## 理解半累加计算

### LastDate & LastNonBlank





## 理解高级时间智能


## 使用定制日期维度