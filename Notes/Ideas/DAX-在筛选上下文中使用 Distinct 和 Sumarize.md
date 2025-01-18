## 6 在筛选上下文中使用 Distinct 和 Sumarize 函数


#### 案例学习：Contoso 计算 客户 粒度上的 平均购买年龄

#domain/powerbi/case


> [!note] 需要进一步明确需求
> 1 当前年龄还是购买时候的年龄
> 2 如果客户购买了三次，那么计算平均的时候应该算一次还是三次
> 3 当多次购买行为发生在不同年龄呢？

Compute the average age of customers **at the time of sale**, counting each customer only once if they made multiple purchases at the same age



第一步：计算发生消费的时候的客户年龄

![600](https://s1.vika.cn/space/2024/03/22/8aab3661844b4c4cadc2ae15ffab4ea0)

行上下文通过 Related 传递

第二步：计算对应粒度上的平均年龄

错误版本一：一个年龄只算了一次，没有考虑客户粒度

![600](https://s1.vika.cn/space/2024/03/22/68e0420f951c435a9d5fc0fc7171d548)

错误版本二：遍历的表中没有 计算信息

![600](https://s1.vika.cn/space/2024/03/22/398f8fbb2b1d4876ab3beecf0b3cb85a)

正确版本

[[DAX 权威指南 - CH03 基础表函数]] 中提到了 **[[DAX-Summarize]]是可以聚合多列的 Distinct/Values** 

![800](https://s1.vika.cn/space/2024/03/22/23fe4463b48a49bc9073fb83124d8a1a)
