---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH15 高级关系]]"
created: 2025-02-10
tags:
  - domain/powerbi
---

# 方案一：CombineValues

![[DAX-CombineValues]]


- DQ 模式下可以生成性能优化的查询语句
- 问题
	- 增加了更多的计算列，可能会对模型大小/查询速度产生影响


# 方案二：LookupValue

[[DAX-LookupValue]]

![image.png](https://s1.vika.cn/space/2025/02/10/0d4e5ab079e946cdb581bc7967106863)


- 如果需要反规范化的列太多，也会有性能问题 大量内存开销