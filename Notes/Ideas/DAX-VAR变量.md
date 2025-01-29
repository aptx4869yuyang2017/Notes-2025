---
up: 
related:
  - "[[DAX 权威指南 - CH06 变量]]"
created: 2025-01-08
tags:
  - domain/powerbi
---

# 语法介绍

![](https://s1.vika.cn/space/2025/01/08/9d01c0655ce641b6b2a8c1960166a8c8)


- VAR/RETURN 成对出现
- RETURN 返回单一变量 是最佳实践 #domain/powerbi/BP
- Debug方法 可以通过分次 RETURN SalesAmount/TotalCost/Margin/MarginPerc 来进行测试

# 变量是常数

![](https://s1.vika.cn/space/2025/01/08/405f9d3bb6654a22869f501d79ba67ce)

如果在迭代函数中分配了变量，那么迭代的每一行都会创建并分配变量，只在迭代函数中能用

![](https://s1.vika.cn/space/2025/01/08/0de6eb8b36b64c4d9c322fd2c32f3cb2)

**变量在定义的时候计值，而不是在使用的时候**
- 上图度量值总返回 100%
- 因为 SalesAmount 变量不受 Calculate 影响


![](https://s1.vika.cn/space/2025/01/08/af3c503e7cf0482194e0faaa451f75eb)

这个度量值可以得到正确结果


> [!important] 变量 vs 新建度量值
> - 可以看出这里的用法是 DXA 独有的视角
> - Tableau 之类的工具只能利用 度量值/字段 作为变量的解决方案


# 理解变量的范围 （作用域）


![](https://s1.vika.cn/space/2025/01/08/5e53838c02a945339b48df77b33c03d2)
必须先定义后使用



![500](https://s1.vika.cn/space/2024/03/25/cfddb5616b8742e480091650be724b83)

- VAR/RETURN 可以嵌套使用
- 变量在 RETURN 结束之后不可用

# 变量存表

![600](https://s1.vika.cn/space/2024/03/25/2e08298ae40843a5b9e2e2b8fde369c3)

- 当变量存了一个表，一般是要对这张表进行迭代
- 使用这个表中的字段，需要使用**原始的 表名 + 列名**
- 变量名不能和表名冲突


> [!NOTE] 可能会发生变化的机制
> ![](https://s1.vika.cn/space/2025/01/08/62a26bd540604d5594a92a59c7b21584)

# 理解惰性计算

[[DAX-惰性计算]]


# 常见场景

## 代码文档化

![600](https://s1.vika.cn/space/2024/03/25/c3ca96eed99a401b95e8494a45edab75)


## 多个嵌套上下文保存信息

行上下文计算信息保存

![600](https://s1.vika.cn/space/2024/03/25/c87325271ae949828258c972f88d8cd9)

筛选上下文计算信息保存

![600](https://s1.vika.cn/space/2024/03/25/9857a3038b4f423d93a3ecce862ff64b)