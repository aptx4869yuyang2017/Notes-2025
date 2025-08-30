---
up:
  - "[[PowerBI DAX 概念 Concept]]"
related:
  - "[[DAX 权威指南 - CH13 写查询]]"
created: 2025-02-10
tags:
  - domain/powerbi
---
# 权威指南总结

![image.png](https://s1.vika.cn/space/2025/02/10/bb8a9f38790c45b6bce3167638396759)
![image.png](https://s1.vika.cn/space/2025/02/10/eea4373a23f8463188f5a27891293cfe)


[[DAX-SummarizeColumns]]

- 来自一张表 只返回存在的已有组合
- 来自不同表 
	- 单独查询列：返回完全交叉连接
	- 增加度量值：删除度量值为空的行
	- [[DAX-AddMissingItems]] 只能恢复度量值为空被删除的行，不能恢复自动匹配机制删除的行



[[DAX-Summarize]] 使用了不同的技术，因为先要从 Sales 这种事实表出发


# 补充材料

[Understanding DAX Auto-Exist - SQLBI](https://www.sqlbi.com/articles/understanding-dax-auto-exist/)

### 问题

![image.png|260](https://s1.vika.cn/space/2025/08/10/b8655e7a0b1c451bae4936b366cfd6ef)



```
# Projects = COUNTROWS ( Projects )
 
# Projects All Time = CALCULATE (
    [# Projects],
    ALL ( Projects[Year] )
)
```


![image.png|429](https://s1.vika.cn/space/2025/08/10/32e0a2fc9784411a8c62ec0e4d2fc93f)

![image.png|436](https://s1.vika.cn/space/2025/08/10/94af1dc90c1b4114a824588041da2d5b)

当选择 2018 的时候，【历史项目数量】数据不对，是因为 Auto-Exist 的机制
查询中转换时，它们会合并为对 [[DAX-SummarizeColumns]] 的单个调用。

```
EVALUATE
SUMMARIZECOLUMNS (
    TREATAS ( { "DAX", "Python" }, 'Projects'[Language] ),
    TREATAS ( { 2018 }, 'Projects'[Year] ),
    "Result", [# Projects All Time]
)
```

在同一表的列上接收两个过滤器。这时自动存在就开始了。作为同一表的列，它们被合并到一个**包含两个列并且仅过滤现有值的单个过滤器** 中。不幸的是，2018 年没有 Python 行。因此，生成的筛选器仅包含 （2018， DAX）

### 解决方案

![image.png](https://s1.vika.cn/space/2025/08/10/8a55ded873ff4fbc9729779881aeeca7)

度量值都换成 维度表的字段

![image.png](https://s1.vika.cn/space/2025/08/10/57eeec167a414882b0cefb9f77e027d3)

![image.png](https://s1.vika.cn/space/2025/08/10/6dd2fffb9a4747e192349a97bb1ebe7b)
