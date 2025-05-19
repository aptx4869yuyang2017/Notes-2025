---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related: 
created: 2025-02-09
tags:
---

# 显示矩阵

![image.png|471](https://s1.vika.cn/space/2025/02/09/492bf2a49b834507bd904f5ea6683342)

# Flat Table


![image.png](https://s1.vika.cn/space/2025/02/09/6e402ad0f3be414aa28f5acc8f5ff7f0)


SummarizeColumns 返回的平面表 Flat Table

![image.png](https://s1.vika.cn/space/2025/02/09/afd75e6dd48c45e6bb1e71f95064f685)


# 虚拟表


![image.png](https://s1.vika.cn/space/2025/02/09/8a31c941a7c248efb48c69d772dd951f)

添加 Visual Shape 之后，可以称为虚拟表

![image.png](https://s1.vika.cn/space/2025/02/09/d532353183c2490f8d2da40958bed024)

这个东西可以理解为虚拟表

具有 VISUAL SHAPE 的表不是变量;它是一个查询定义的表。因为它是一个表，所以查询可以定义添加到表中的新列（列不能添加到变量中）。
每个可视化计算都是添加到表中的新列，这些列可以引用 ROWS 和 COLUMNS，因为轴的定义是表定义的一部分。