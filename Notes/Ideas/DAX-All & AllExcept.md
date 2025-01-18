---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH03 基础表函数]]"
created: 2024-11-30
tags:
  - domain/data
---

# CH03 内容


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

---

### 案例 - Top 类别子类别

#domain/powerbi/case 

> [!important]  Top 类别子类别
> EN-P66/CH-P62
> 
> the category and subcategory of products that sold more than twice the average sales amount
> 销售额超过平均销售额两倍的产品类别和子类别
> 
> 怎么用 Calculate 写更高效的版本呢？
> #domain/powerbi/performance 
> #TODO 

^f02df8



显示销售额超过平均值两倍的类别和子类别， 存到一个表中

- 使用 All 列出所有 类别-自类别组合
- 计算 类别-子类别组合 销售额 的平均值
- 筛选出 符合条件 的类别-子类别组合
	- 这里 创建变量的方式很有意思，要理解 **变量计算使用的是创建时候的计值上下文**

#### 方案一 - CH03

```
BestCategories =
VAR Subcategories =
    ALL ( 'Product'[Category], 'Product'[Subcategory] )
VAR AverageSales =
    AVERAGEX (
        Subcategories,
        SUMX ( RELATEDTABLE ( Sales ), Sales[Quantity] * Sales[Net Price] )
    )
VAR TopCategories =
    FILTER (
        Subcategories,
        VAR SalesOfCategory =
            SUMX ( RELATEDTABLE ( Sales ), Sales[Quantity] * Sales[Net Price] )
        RETURN
            SalesOfCategory >= AverageSales * 2
    )
RETURN
    TopCategories
```


#### 方案二 - 预计算版本

```
VAR Subcategories =
    ALL('Product'[Category], 'Product'[Subcategory])
VAR SalesPerSubcategory =
    ADDCOLUMNS(
        Subcategories,
        "@TotalSales", SUMX(RELATEDTABLE(Sales), Sales[Quantity] * Sales[Net Price])
    )
VAR AverageSales =
    AVERAGEX(SalesPerSubcategory, [@TotalSales])
VAR TopCategories =
    FILTER(
        SalesPerSubcategory,
        [@TotalSales] >= AverageSales * 2
    )
RETURN
    TopCategories

```


#### 方案三 -  使用 Calculate 预计算 (上下文转换)

```
VAR Subcategories =
    ALL('Product'[Category], 'Product'[Subcategory])

VAR AverageSales =
    AVERAGEX(
        Subcategories,
        CALCULATE(
            SUMX(Sales, Sales[Quantity] * Sales[Net Price])
        )
    )

VAR TopCategories =
    FILTER(
        Subcategories,
        CALCULATE(
            SUMX(Sales, Sales[Quantity] * Sales[Net Price])
        ) >= AverageSales * 2
    )

RETURN
    TopCategories

```