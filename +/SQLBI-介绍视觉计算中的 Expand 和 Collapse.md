---
up:
  - "[[DAX-视觉计算]]"
related: 
created: 2025-02-09
tags: 
type: "[[Article]]"
finished: 2025-02-09
aliases:
---


- [Introducing EXPAND and COLLAPSE for visual calculations in Power BI](https://www.sqlbi.com/articles/introducing-expand-and-collapse-for-visual-calculations/)

# 使用视觉上下文操作虚拟表的晶格




![image.png](https://s1.vika.cn/space/2025/02/09/c853cad81ca441c3b97b68c85c7a89ef)




- 虚拟表 Lattice
	- 这个 Lattice 代表了一个虚拟表
	- 每个虚拟表都是
- 最细粒度的虚拟表（橙色）是基础数据，蓝色的则都是 各种 total

![image.png](https://s1.vika.cn/space/2025/02/09/f6ae4894783e4f059dc6aec5d2a4c482)

- 视觉上下文可以被认为是对 虚拟表中的行的筛选
	- 可以筛选一行，也可以筛选很多行
- 同时视觉上下文还知道自己所在的层级


## 自己的理解

![image.png](https://s1.vika.cn/space/2025/02/09/e6afd0c7e97d4aaea13167783ae530b6)

- 矩阵中的每个格子都对应着虚拟表Lattice 中的一个位置
- 其实 Collapse/Expand 就是对 视觉上下文的修改（当然得使用 Calculate）

# 了解 Collapse 和 Expand


![image.png](https://s1.vika.cn/space/2025/02/09/75b23c07e3c04b5ebec73c94736706d3)

Collapse 和 Expand 可以被认为是 context modifier

## Collapse 一个层级

![image.png|554](https://s1.vika.cn/space/2025/02/09/11b6054d3257413eb44e0dc3974ee967)

![image.png|447](https://s1.vika.cn/space/2025/02/09/8eab4df9bb414c518626f864221994f9)


## Collapse 到指定级别


![image.png|495](https://s1.vika.cn/space/2025/02/09/a110f1d63c80493a8906ed06e2e1881d)


![image.png|461](https://s1.vika.cn/space/2025/02/09/bf93ca47f40d47839f91de4ca358a6d0)

作为 COLLAPSE 参数提供的列的上方的级别 （**第一个不存在参数的层级**）

![image.png|451](https://s1.vika.cn/space/2025/02/09/c84e3345ce2e4062b46a6444db530d54)

下图显示 _Year_ 列存在于除总计之外的所有级别上。因此，总计是不包括 _Year_ 的最低级别。

## Expand 到的层级永远会有多行 所以需要使用聚合函数


![image.png|573](https://s1.vika.cn/space/2025/02/09/e6d8e99966624d8483d2cb886b0d0d27)

![image.png|559](https://s1.vika.cn/space/2025/02/09/fd783ce95f244311ba92d65b29ff9ebb)


![image.png|558](https://s1.vika.cn/space/2025/02/09/ccd851b552c24685b305ec95aee1963d)


## Expand 到指定列


![image.png|414](https://s1.vika.cn/space/2025/02/09/4982492d6c0b4031a5bf9be1e6e0114d)

视觉上下文移动到包含 列 的**最高层次结构级别**[[DAX-Case-处理层级占比]]


## Collapse 和 Expand 参数一致 层级也不一定一致

![image.png|417](https://s1.vika.cn/space/2025/02/09/5c0584416c4c458aa8f2f5d026ac4680)



