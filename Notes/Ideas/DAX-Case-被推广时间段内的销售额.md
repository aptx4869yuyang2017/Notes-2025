---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX-虚拟关系]]"
  - "[[DAX 权威指南 - CH15 高级关系]]"
created: 2025-06-10
tags:
  - domain/powerbi
---
# 案例 - 被推广时间段内的销售额

年月-品牌 粒度的推广信息

![image.png|328](https://s1.vika.cn/space/2025/06/10/0245864ba6d8471195f7ccc3223ab2fa)

### 已经知道方案

- 建立多列关系
- 反规范化到 Sales 表中


### 筛选器转移方案1 - Contains

[[DAX-Contains]]

#### 劣化版本

![image.png](https://s1.vika.cn/space/2025/06/10/e47ecfad4c294f60b8456a39231002c3)

问题
- Filter 迭代 Sales 大表 效率不好
- 没有利用好已有的 度量值 `[Sales Amount]`

#### 优化版本

Filter 迭代的是 Summarize 后的表

![image.png|487](https://s1.vika.cn/space/2025/06/10/d96f6d2a6dc74f90994618411f07da82)
![image.png|486](https://s1.vika.cn/space/2025/06/10/291fa7ab13534ab3bbf70929e3db8e48)



### 筛选器转移方案2 - TreatAs

[[DAX-TreatAs]]

![image.png](https://s1.vika.cn/space/2025/06/10/d729f44b40e0416fa9ee91b31df67bcd)



### 筛选器转移方案3 - Intersect

[[DAX-Intersect]]

![image.png](https://s1.vika.cn/space/2025/06/10/0ebc0208b27d40d198ebf582a501559e)
![image.png](https://s1.vika.cn/space/2025/06/10/93698ae3fe0c4455a7fb81cba39f2ba7)
