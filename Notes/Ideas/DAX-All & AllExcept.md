---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH03 基础表函数]]"
created: 2024-11-30
tags:
  - domain/data
---

# CH03 内容（作为表函数）


- All 系列函数的本质可以和 Filter 对照理解，是为了扩展行数实现特定计算
- AllCrossFiltered 会在 [[DAX 权威指南 - CH14 DAX高级概念]] 中介绍，本章没有任何涉及
- 计算百分比/比率时候非常有用
	- ![400](https://s1.vika.cn/space/2024/03/20/7123d7defec14f118090e02d8ab65ce8)![400](https://s1.vika.cn/space/2024/03/20/c344ac4749694b42b79475521b95b904)
- All 的参数不能是表达式，**必须是 表名或者列名**
	- 输入表名：返回整个没有被筛选的表
	- 输入一列：返回表中所有列值组成的表
	- 输入两列：表中两个列的所有组合情况
- AllExcept 
	- 为了自动引入自动加入到表中的列



[[DAX-Case-Top类别子类别]]



# CH05 作为调节器

### All in Calculate

> [!error] 错误理解
> ![400](https://s1.vika.cn/space/2024/03/23/f8ab9d8f5b5f4cf090247bae5799f7ad)
> 

> [!important] 正确理解
> ![400](https://s1.vika.cn/space/2024/03/23/3055825904fc4b36bdad0c3832d24086)


- 本质上和 All 作为表函数是不同的功能
- 应该被称为 RemoveFilter 但是因为历史原因保留了这个名字
- Calculate 执行的筛选器参数也有执行顺序，All类会先执行

![400](https://s1.vika.cn/space/2024/03/23/fdebbc3070f344b68582ef05e25c422d)

 - 第一次看还是没有搞清楚 [[DAX-Calculate-筛选参数调节器]] 的概念
 - 现在看这个逻辑很清晰，All 先生效移除了所有 Color 筛选，KeepFilters 作用在最终筛选上下文上，保留 Red。其实效果和 简单实用 `'Product'[Color] = "Red"` 效果一致