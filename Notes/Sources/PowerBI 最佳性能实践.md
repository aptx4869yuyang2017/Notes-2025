---
up:
related:
year: 2022
created: 2024-11-19
tags:
type: "[[Book]]"
ch: "00"
finished:
aliases:
---

##  Part 1 - 架构 瓶颈 性能目标

#### CH01-设定目标并识别问题领域

Nah F. (2004) 
tolerable wait time (TWT) 

常规报告 4秒，最差场景 14秒
架构图太乱了，一眼看不到重点


那些原因影响性能：

- **Inappropriate use of DirectQuery/Import**  DQ vs 提取
	- 这里的决策在模型大小、刷新时间、数据新鲜度和报告互动性之间取得平衡。
- **Power Query design** PQ设计
	- 这里的决策可能无法利用数据源的原生功能，因此也可能无法减少混合引擎中的额外工作。
	- **mashup engine 是啥？？**
	- 
- **Data modeling**
	- 可能会使数据模型不必要地变大，浪费内存，消耗更多计算资源，并影响可用性。
- **Inefficient DAX calculations**
	- 没有高效的内部VertiPaq存储引擎，而迫使操作在FE中进行。
- **Complex or inefficient row-level security**
	- 决策可能造成行级权限计算产生大量非必要计算
- **Poorly designed reports**
	- 加载时间太长
- **Data source or network latency**:

#### CH02-架构与配置


###### 1 数据连接与存储模式

三种数据链接模式

- Import
- DQ
- Direct Lake Delta Table（PowerBI都不行，得 Tabular Editor）

###### 2 网关 Gateway 优化




[[PowerBI 最佳性能实践-CH03-性能调优工具]]





## Part 2 - 性能分析 - 提升与管理

CH04-分析日志和指标




CH05-存储模式优化
CH06-第三方实用程序
CH07-新能治理框架


## Part 3 - 获取、转换、可视化数据

CH08-加载 转换和刷新数据
[[PowerBI 最佳性能实践-CH09-报告与仪表板设计]]

## Part 4 - 数据模型、计算和大型语义模型

CH10-维度建模与行级别安全
CH11-改进DAX
CH12-High-Scale Patterns
## Part 5 -  优化 Power BI Enterprise 的功能


CH14-Working with Capacities
CH15-Performance Needs for Fabric Artifacts
CH16-Embedding in Web Apps