---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH08 时间智能计算]]"
created: 2025-02-09
tags:
  - domain/powerbi
---
# 两种方案表示 MAT 周期的第一天

`NEXTDAY ( SAMEPERIODLASTYEAR ( LASTDATE ( 'Date'[Date] ) ) )`

`SAMEPERIODLASTYEAR ( NEXTDAY ( LASTDATE ( 'Date'[Date] ) ) )`


![image.png](https://s1.vika.cn/space/2025/02/09/7e95781106a84666b76345d8470d2f9d)

![image.png](https://s1.vika.cn/space/2025/02/09/86bb7979b86f499c9724d47c6ad16395)

- 原因是 LastDay - NextDay - LY 的顺序会找到没有日期范围的一天