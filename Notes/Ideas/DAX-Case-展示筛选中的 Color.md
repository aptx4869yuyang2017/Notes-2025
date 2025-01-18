---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH07 使用迭代函数Calculate组合]]"
created: 2025-01-12
tags:
  - domain/powerbi
---
# 需求 
展示筛选器选中的 Color

![400](https://s1.vika.cn/space/2024/03/26/dcfef6ec5151461383ab06235a1b46bc)

# 基础版本

![](https://s1.vika.cn/space/2025/01/12/e7363322b9b0412f86481082e0a2c0de)

问题
- 超过5种颜色的情况下，列表太长，用户体验不够理想


# 优化用户体验

![ee97b518275a4cffbdf410a2adcb8146|501](https://s1.vika.cn/space/2025/01/12/ee97b518275a4cffbdf410a2adcb8146)


![500](https://s1.vika.cn/space/2024/03/26/2e723fa4a6a14f08934418e76f8d0d5f)

问题 
- 假如用户选择了5个 Color 但是因为其他筛选条件的影响，导致颜色展示不全
- [[DAX 权威指南 - CH10 使用筛选上下文]] 会完善这个案例

# CH10优化版本