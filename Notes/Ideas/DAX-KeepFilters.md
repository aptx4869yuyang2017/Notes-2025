---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
created: 2025-01-04
tags:
  - domain/powerbi
---
KeepFilters 本质上是 **筛选参数调节器**
不会覆盖同一列上已经存在的筛选器


两种用法

用法一：calculate 的参数
![](https://s1.vika.cn/space/2025/01/04/f39ba38c8989470eafade3e7c1391cd0)


用法二：上下文转换形成的筛选上下文参数，添加 KeepFilters 效果
![](https://s1.vika.cn/space/2025/01/04/22686e6a67eb4faf9a50947b69fa4b3d)



[[DAX 权威指南 - CH10 使用筛选上下文]] 有一些高级用法


