---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH04 理解计值上下文EC]]"
created: 2024-12-08
---

### Filter 如何影响

![500](https://s1.vika.cn/space/2024/03/21/80acd231c32d4b6d80cb4205efaf07f1)

![6d2fdb37e6304723beb0eafdc9620e92|491](https://s1.vika.cn/space/2024/12/08/6d2fdb37e6304723beb0eafdc9620e92)

[[DAX-Filter]]

- 外部筛选器 - 筛选上下文
- Filter - 行上下文
- **Filter 只是迭代并不改变筛选上下文，只是扫描被筛选上下文筛选过的表**


### All

![500](https://s1.vika.cn/space/2024/03/21/29d7b50efc2a4c5b876ec8dadc3f04c0)

![382ba9b2448c44f296aa97672f5ffca1|556](https://s1.vika.cn/space/2024/12/08/382ba9b2448c44f296aa97672f5ffca1)

[[DAX-All & AllExcept]]

- All 对筛选上下文的忽略作用
	- 同时忽略了 Color & Brand 两个筛选条件
- 行标题的计算，没有受到 All 函数的影响
	- 当选择 Azure 时候，只返回了 Azure 的 Brand，当然 数量还是 红色产品的数量