---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH05 Calculate & CalculateTable]]"
created: 2025-01-01
tags:
  - domain/powerbi
---


# 参数介绍



![600](https://s1.vika.cn/space/2024/03/23/e6fb83b7bc464a1ea848e3ab3280fa40)
![600](https://s1.vika.cn/space/2024/03/23/68552bb6545248448700844e4090c448)
![600](https://s1.vika.cn/space/2024/03/23/54bc7ef1bd21463dbe0147a49303ddf6)

- 完整语法格式，**值的列表**， 形式是一个 **表的表达式**
	- 结果可以是任意数量的列
- 布尔条件是一种 **语法糖**  [[DAX-语法糖]] ^e30627
	- **语法糖不存在功能和性能上的任何差异** [[PowerBI 性能 MOC|PowerBI Performance]]
	- 结果必须是**单值的值列表**

# 基础语义


![500](https://s1.vika.cn/space/2024/03/23/c3046843cb69486eb51a6ecc4ec57dc8)


- 对筛选上下文的覆盖效果
- **只覆盖来自同一列的筛选器，合并不同列上的筛选器**

![](https://s1.vika.cn/space/2024/03/23/a80ac07849254c13acfca4775ec33200)

**语义**

- 复制筛选上下文
- 对 筛选参数 计值，给每一个列具体列生成一个 值的列表 list of values
- 如果两个条件对同一列生效，取**交集**
- 覆盖来自同一列的筛选上下文，不需要覆盖的就直接添加
- 用新的筛选，对 Calculate 的第一个参数进行 计值
- 恢复原始上下文



# 计算百分比

[[DAX-Case-计算百分比]]


# KeepFilters

如果不想覆盖当前列上存在的上下文怎么办？

- 当然不是又回去用 Filter
- 而是使用 [[DAX-KeepFilters]]



# 单列上的多个条件


![image.png](https://s1.vika.cn/space/2025/01/28/43a2c496c2da4a559516789abaff1967)
![image.png](https://s1.vika.cn/space/2025/01/28/60265a1d0c774e1e845e982eda471fe5)


- 语法有效
- 从转化完整语法的角度思考

[[PowerBI 性能 MOC|PowerBI Performance]]：这里性能会有差异么？



# 由多个列构成的筛选条件

- 书中的内容可以扫一眼，版本更新之后很多写法开始支持了
- [[DAX-Calcualte-多条件筛选(21-03之后)]] 



# 多层嵌套 calculate 计值顺序

![400](https://s1.vika.cn/space/2024/03/23/a3ea4a1dd5774fec849aa27ab838a641)

![400](https://s1.vika.cn/space/2024/03/23/2f03f3aaf6f94e06bd0b164d2e8f6470)

**内侧覆盖外侧，但是可以用 KeepFilter 保持外层的筛选**
