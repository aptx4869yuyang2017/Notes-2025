---
up: 
related:
  - "[[DP600 Fabric Learn]]"
created: 2024-12-29
tags:
  - domain/data
type: "[[Class]]"
finished: 2024-12-31
Section: 5
aliases:
  - Getting data into Fabric
---

![bb33fb8568944453a52125a07df5d09c|439](https://s1.vika.cn/space/2024/12/29/bb33fb8568944453a52125a07df5d09c)

![](https://s1.vika.cn/space/2024/12/29/19dcc882452d4002b16266361a33afea)

![](https://s1.vika.cn/space/2024/12/29/41ecf19fbe7547c49f309d8fcfbe08d6)

## Dataflow

![](https://s1.vika.cn/space/2024/12/29/04a4b2275cdf436496e5055a94caccaa)

你可以使用150多个连接器将数据从外部系统导入到熟悉的Power Query低代码/无代码界面，执行数据转换，然后写入Fabric数据存储。

#### 优点（何时应考虑使用）

- 使用150多个外部连接器
- 无需代码或低代码解决方案
- 可以进行提取、转换和加载（ETL）
- 访问本地数据（OPDG）
- 当你需要同时获取多个数据集并合并它们时（尽管你可能希望分批处理以允许数据验证）。
- 可以上传原始本地文件（静态文件）

#### 缺点（也许不应使用的情况）

- 在处理大型数据集时可能会遇到困难（尽管最近引入了快速复制功能，这应该会加速你的ETL过程）！
- 实现数据验证困难
- 目前无法传递外部参数


## Data Pipeline

![](https://s1.vika.cn/space/2024/12/31/c7a4712a81fb48f5874b1f5abaac5805)

主要是一个编排工具（先做这个，再做那个）。也可以用来将数据导入Fabric，使用Copy Data活动（和其他活动！）。

**优点（何时应考虑使用）**

大型数据集（尽管现在Dataflow有快速复制功能，因此性能应该在这两者之间相当）。
导入“云”数据（例如Azure中的数据）。
当你需要控制流逻辑时。
触发Fabric内外的各种操作，如Dataflows、Notebooks、存储过程、KQL脚本、Webhooks、Azure Functions、Azure ML、Azure Databricks。

**缺点（也许不应使用的情况）**

不能原生执行转换（但可以嵌入笔记本或数据流）。
没有能力上传本地文件。
不支持跨工作区工作（目前虽然此功能正在计划中：））


## Notebook

![](https://s1.vika.cn/space/2024/12/31/92ecec19a1114fa98cefee2114070400)

通用的编码笔记本，可以用来通过连接到API或将数据导入Fabric使用客户端Python库。

**优点（何时应考虑使用）**

从API中提取（使用Python requests库或类似工具）
使用客户端库（例如Azure库，或使用Hubspot客户端库在Python中访问Hubspot数据）
适用于代码重用（可以参数化）
对于传入数据的数据验证和数据质量测试
在数据摄入方面最快（并且对于CU支出最高效 - 参见此处）

**缺点（也许不应使用的情况）**

当您的组织没有Python能力时
当您想要写入数据仓库时（目前不可能）

## Shortcuts

![](https://s1.vika.cn/space/2024/12/31/9b208e3886b048fb8563176c7b194b5b)



![](https://s1.vika.cn/space/2024/12/31/b067d032bb694c409412def7908a3610)


