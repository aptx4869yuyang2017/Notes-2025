---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX-Calculate]]"
  - "[[DAX-KeepFilters]]"
created: 2025-01-29
tags:
  - domain/powerbi
---

# 清晰的概念

区别于 Calculate 调节器，筛选参数调节器的**作用对象是 Calculate的筛选参数**



- Calculate 调节器
	- 更改关系结构/删除一些筛选器
- 筛选参数调节器
	- 没有改变 Calculate 的计算过程，只是改变了 其中**某个参数作用于** **最终筛选上下文** 的方式


# 导致作用顺序的差异



![image.png](https://s1.vika.cn/space/2025/01/29/deee2b9ca8934cdd9612423672962ce6)


EN171 CH161
- 两种写法的结果相同
- 注意 All 先生效，KeepFilters 后生效


