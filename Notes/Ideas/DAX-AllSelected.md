---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH03 基础表函数]]"
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
  - "[[DAX 权威指南 - CH14 DAX高级概念]]"
created: 2024-11-30
tags:
  - domain/data
---

# CH03 作为表函数

![600](https://s1.vika.cn/space/2024/03/20/ae028b94058b4ae5b43a71b9129d22b0)

- 为了让外部筛选器生效，使用 AllSelected 替换 All
- 只考虑当前视觉对象之外的筛选器


# CH05 作为 Calculate 调节器

CH05-03  没有参数的 All / AllSelected

> [!important]
>  只有作为 Calculate 调节器 的时候可以没有参数

![image.png](https://s1.vika.cn/space/2025/01/29/640c447e0d2f486db5a0e08748879b66)

![image.png](https://s1.vika.cn/space/2025/01/29/5e3917d317d94a5d8d3b4f723fe308e5)

- `AllSelected()` 恢复当前视觉对象之外所有活动的筛选上下文
- `All()` 从模型中的所有表中清除筛选上下文，得到一个没有活动筛选器的上下文


# CH14 高级概念

[[DAX 权威指南 - CH14 DAX高级概念]]