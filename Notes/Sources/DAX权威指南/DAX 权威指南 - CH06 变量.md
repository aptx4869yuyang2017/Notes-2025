---
created: 2024-03-24
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "06"
finished: 2024-03-24
---

### 理解作用域

- 同级别的 VAR 可以使用
- 后定义的可以使用前面定义的
- Return 中可以使用
	- Return 中可以嵌套一组新的 VAR/Return

![500](https://s1.vika.cn/space/2024/03/25/cfddb5616b8742e480091650be724b83)
### 变量存表


![600](https://s1.vika.cn/space/2024/03/25/2e08298ae40843a5b9e2e2b8fde369c3)

- 当变量存了一个表，一般是要对这张表进行迭代
- 使用这个表中的字段，需要使用原始的 表名 + 列名


### 理解惰性计算


- 有时候 引擎对子公式的识别不是特别精准，子公式不一定只计算一次
- 变量一定只计算一次

### 使用变量的场景

- 代码文档化
- 在不同的上下文计算值
	- 行上下文
	- 筛选上下文
- 


![600](https://s1.vika.cn/space/2024/03/25/c3ca96eed99a401b95e8494a45edab75)
![600](https://s1.vika.cn/space/2024/03/25/c87325271ae949828258c972f88d8cd9)

![600](https://s1.vika.cn/space/2024/03/25/9857a3038b4f423d93a3ecce862ff64b)