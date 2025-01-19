---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH04 理解计值上下文EC]]"
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
created: 2024-12-07
---
## CH04 基础定义

> [!important] 记值上下文
> 记值上下文是计算 DAX 表达式的被记值时候的的背景环境

#### 基础效果

> [!important] 筛选上下文 Filter Context
> DAX evaluates all formulas within a respective context. Even though the formula is the same, the result is different because DAX executes the same code against different subsets of data.
> DAX 在各自的上下文中评估所有公式。尽管公式相同，但结果不同，因为 DAX 会针对不同的数据子集执行相同的代码。

#### 更正式的定义

![](https://s1.vika.cn/space/2024/12/07/2bda09692fc44d1b923724ad3a005846)

- 筛选上下文是 筛选器 的集合
- 筛选器是 一组值（Tuple） 的列表


#### 公式的语意解读


`Sales Amount := SUMX ( Sales, Sales[Quantity] * Sales[Net Price] )`

度量计算
- 遍历 **当前筛选上下文中可见的 Sales 表**
- 对每一行 Quantity数量 与 Net Price净价 计算乘积
- 对上一步所有计算结果求和


