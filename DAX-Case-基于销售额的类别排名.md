---
up:
  - "[[PowerBI DAX Case 案例]]"
related:
  - "[[DAX 权威指南 - CH07 使用迭代函数Calculate组合]]"
created: 2025-01-29
tags:
  - domain/powerbi
---
# 需求：基于销售额的类别排名

![image.png|588](https://s1.vika.cn/space/2025/01/29/4857160613f54568bc97fd5253621dfb)



# 版本一：基础版本


![image.png](https://s1.vika.cn/space/2025/01/29/4d614353577e41e29c817c8ecce2ed4a)

RankX 的执行步骤

- 构建查询表（通过迭代第一参数）
	- 迭代第一参数
	- 迭代期间，行上下文，对第二参数计值
	- 对 **查询表进行排序**
- 在原始的计值上下文对第二参数计值
- 返回 第二步计算结果在查询表中的位置


![500](https://s1.vika.cn/space/2024/03/26/4412d2ce7f834789a6f7e2b22ec32b38)

# 版本二：避免 Total 返回排序

![image.png](https://s1.vika.cn/space/2025/01/29/bdbbef09c0224b52800bf6e99ff46f58)

版本一存在的问题：Total 返回了排序

![image.png](https://s1.vika.cn/space/2025/01/29/9cb953995f4b40b3b0752f05a66e3eed)


**使用 HasOneValue 可以避免，在 Total 返回排序值**

# 版本三：使用另外的表进行排序


- 第三参数：表达式 使用不同的表达式来用于排序
- 第四参数：Asc/Desc


![image.png](https://s1.vika.cn/space/2025/01/29/b78807dbd8aa49f592e4cccdd49e6079)


![400](https://s1.vika.cn/space/2024/03/26/95c6855507564ed5b58569fa89883b44)

使用 `'Sales Ranking'[Sales]` 来进行排序

![image.png](https://s1.vika.cn/space/2025/01/29/4c267206c5e4427a93e92cfb6b22776c)


![image.png](https://s1.vika.cn/space/2025/01/29/4cb25dc233f04c049aa52213fa760448)


# 版本四：使用不同的排序方式

- 第五参数：Dense/Skip

![image.png](https://s1.vika.cn/space/2025/01/29/0541fb2dac624d158345c878ceea0eaf)


![image.png](https://s1.vika.cn/space/2025/01/29/e777ff1fbde341a4a9904cdb534cce0e)

![image.png](https://s1.vika.cn/space/2025/01/29/5675eee3eca74fcfbcc8b8301c576b0a)


# HasOneValue 检查的重要性


![image.png](https://s1.vika.cn/space/2025/01/29/2c65af4a203a412cbccb0c8febaa3ad2)

如果使用非预期的字段展示，没有 HasOneValue 进行判断，会造成问题


# 切片器造成排名不连续的问题

![image.png](https://s1.vika.cn/space/2025/01/29/34f801db6289495d87f1923e44127737)

[[DAX-AllSelected]] 可以解决这个问题

![image.png](https://s1.vika.cn/space/2025/01/29/96d587fe0b074b438b2100f3e4a50d2e)
