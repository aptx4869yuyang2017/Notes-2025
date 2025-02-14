---
up:
  - "[[BI 工具对比 Map]]"
related: 
created: 2025-01-26
tags:
  - domain/bi
---



- 基础类比
	- Tableau 是一个大漏斗
	- PowerBI 则是一块橡皮泥


![image.png](https://s1.vika.cn/space/2025/01/26/8f721c779a4946139b3405e9da084ea1)

[Tableau Order of Operation Overview (Tableau Filters) - YouTube](https://www.youtube.com/watch?v=ehQpTa127tU)

- Tableau 的不同计算的执行顺序非常重要
- 其实在每次筛数据前其实都有调整数据的机会，比如 Fixed LOD 就是一种调整数据的方式
- 这也就是为什么 Tableau 是 **宽表思维**


![](https://s1.vika.cn/space/2024/12/07/2bda09692fc44d1b923724ad3a005846)

这张图可以重构一下

- 本身并没有严格的顺序，所有的筛选条件可以说是同时生效的
- 但是 Calculate/All 这种调整动作，作用顺序一定在后面
- 这也就为什么 PowerBI 是 **模型思维** 的一部分原因



案例：

[[怎么使用 LOD 来实现 DAX-All 函数的功能]]