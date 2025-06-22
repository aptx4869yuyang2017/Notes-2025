---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH14 DAX高级概念]]"
  - "[[DAX 权威指南 - CH12 使用表函数 Work With Tables]]"
created: 2025-02-09
tags:
  - domain/powerbi
---

- 模型表中的每一列都有唯一的 **数据沿袭** 
- 筛选上下文筛选模型，筛选的是与筛选上下文中的列具有相同  **数据沿袭**  的列
- 筛选器的本质是表，不同表函数对  **数据沿袭**  有不同影响
	- **分组数据**对列保持数据沿袭
	- **聚合结果**的列保持数据沿袭
	- [[DAX-Row]] &  [[DAX-AddColumns & SelectColumns|AddColumns]] 创建的新列，产生新的数据沿袭
	- [[DAX-AddColumns & SelectColumns|SelectColumns]] 返回的只是列副本，保持数据沿袭，否则创建新的数据沿袭

![image.png|569](https://s1.vika.cn/space/2025/02/09/f989d56d69bb48c2bdf1992a8687f474)

因为 C2 和 'Product'[Color] 没有共同的数据沿袭，结果中的 Sales Amount 都一样

![image.png|388](https://s1.vika.cn/space/2025/02/09/c4975d06b09c4a05a79c095006a20496)

可以用 [[DAX-TreatAs]] 修改数据沿袭

![image.png|540](https://s1.vika.cn/space/2025/02/09/90bf4b8dee6c4dfe89eff552e1690600)

![image.png|375](https://s1.vika.cn/space/2025/02/09/3e65d72475d940868e31c2682c8a0a2e)
