---
up:
  - "[[Optimizing DAX 优化DAX(book)]]"
created: 2025-08-26
type: "[[Chapter]]"
ch: "01"
finished: 2025-08-26
---
# CH01 介绍

### 下载数据 测试文件等

[Contoso sample databases· GitHub](https://github.com/sql-bi/Contoso-Data-Generator-V2-data/releases/tag/ready-to-use-data)


### 模型概览


![image.png](https://s1.vika.cn/space/2025/08/26/833252fd2b584d6998d4cae24974c43a)

**优化策略的选择高度依赖于架构设计**。我们可能遇到简单的DAX问题——低效代码导致性能低下。然而，同一段DAX代码在VertiPaq模式下可能运行良好，但在复合模型中却会产生严重问题。有时代码本身没有问题，但在DirectQuery模式下由于物化数据量过大也会引发性能瓶颈。

换言之，除非我们完全理解表格模型中所有组件的协同机制，否则几乎不可能制定出通用的DAX代码编写指南或构建高性能模型的规范。