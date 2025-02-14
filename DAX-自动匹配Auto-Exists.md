---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH13 写查询]]"
created: 2025-02-10
tags:
  - domain/powerbi
---

![image.png](https://s1.vika.cn/space/2025/02/10/bb8a9f38790c45b6bce3167638396759)
![image.png](https://s1.vika.cn/space/2025/02/10/eea4373a23f8463188f5a27891293cfe)


[[DAX-SummarizeColumns]]

- 来自一张表 只返回存在的已有组合
- 来自不同表 
	- 单独查询列：返回完全交叉连接
	- 增加度量值：删除度量值为空的行
	- [[DAX-AddMissingItems]] 只能恢复度量值为空被删除的行，不能恢复自动匹配机制删除的行



[[DAX-Summarize]] 使用了不同的技术，因为先要从 Sales 这种事实表出发



