---
up:
  - "[[Optimizing DAX 优化DAX(book)]]"
created: 2025-08-26
type: "[[Chapter]]"
ch: "03"
finished:
---


### 数据孤岛与跨岛查询


![](https://s1.vika.cn/space/2024/08/21/4923283e8c524993a68705f461016fc9)


- Product / Sales 存在远程的 AS 模型上，也就是 DQ over AS
- Customer DQ over SQL
- Date VertiPaq


![](https://s1.vika.cn/space/2024/08/21/6cb03dea0569479f991bb61c6fd40c9a)


![775109ddfd30417ab52d93beb7c417ca|468](https://s1.vika.cn/space/2024/08/21/775109ddfd30417ab52d93beb7c417ca)

- 解决思路：
	- 因为分别的岛屿并不知道其他岛屿的信息，所以只能在关联粒度上查询数据，最后让 FE 进行处理
- 问题
	- 服务器之间有大量的数据移动，例如 CustomerKey 包含的值远比 Continent 多

![6be5ebff509f481dac23dbde0473af44|589](https://s1.vika.cn/space/2024/08/21/6be5ebff509f481dac23dbde0473af44)

- 实际方案：
	- 把 Customer / Date 两个岛屿， 聚合维度 - 键  查询出来
	- 传给 remote 的有 Sales 的岛屿处理