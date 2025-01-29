---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
created: 2025-01-28
tags:
  - domain/powerbi
---

> [!important]
> Calculate 可以**使行上下文无效**，自动添加当前行上下文中迭代所有列作为筛选参数（筛选上下文）

# 上下文转换介绍

![image.png](https://s1.vika.cn/space/2025/01/28/e5ea60bec8054538886a8ab4e84f8fed)


- 上下文转换开销很大
- 上下文转换不仅筛选一行
- 上下文转换会使用到公式中不存在的列
- 当行上下文被转换成筛选上下文的时候，就开始筛选整个模型了
- 只要有行上下文，使用 calculate 就会发生上下文转换
- 作用于所有行上下文
- 行上下文失效

# 计算列中的上下文转换

**没有key的表上执行上下文转换会非常危险⚠️**

[[DAX-Case-高业绩产品]]


# 度量值中的上下文转换

**每个被引用的度量值都被隐式封装在列 Calculate 中**


# 上下文转换造成的循环依赖问题

[[DAX-循环依赖问题]]