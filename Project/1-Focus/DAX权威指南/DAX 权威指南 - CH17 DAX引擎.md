---
created: ""
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "17"
---

# 理解 DAX 引擎架构

![](https://s1.vika.cn/space/2024/07/03/b06bd852022d40128c0aea585848c6c1)


- 公式引擎 FE
	-  DAX/MDX -> FE -> 查询计划 Query Plan
	- FE 没有缓存
	- FE 是单线程的
- 存储引擎 SE
	- 聚合表可以用来优化 SE
	- 聚合表通常定义在 SE 中
- VertiPaq 存储引擎
	- 从数据源读取数据加载到内存中进行压缩，然后存储到列数据库中
	- 运算符有限
	- VertiPaq 查询在内部使用 xmSQL 伪SQL
	- 多线程，但是前提是有多个 Segment
	- 缓存系统保留了最近 512 个内部查询
	- 扫描操作比工时引擎快，在压缩数据上进行迭代
- DirectQuery 存储引擎
	- FE 知道 DQ 的存在，发送过来的**查询计划**会利用到 SQL 到运算符，例如 Lower 这种 VertiPaq 不支持的字符串函数
- 理解数据刷新
	1. 读取数据集，转换为 VertiPaq 的列式数据结构，对每一列进行压缩编码
	2. 为每一列创建字典和索引
	3. 为关系创建数据结构
	4. 计算和压缩所有**计算列**和**计算表**


# 理解 VertiPaq 存储引擎


## 1 列式数据库

行式存储的物理内存布局
![92c32b38aa1544edb74b730c109e4300|365](https://s1.vika.cn/space/2024/07/04/92c32b38aa1544edb74b730c109e4300)
![](https://s1.vika.cn/space/2024/07/04/c6df2db0078a44cc97f8b005f16cfc24)


列式存储的物理内存布局

![c6cf8acc1a32498abc3bc22fa2a9a489|481](https://s1.vika.cn/space/2024/07/04/c6cf8acc1a32498abc3bc22fa2a9a489)
![](https://s1.vika.cn/space/2024/07/04/2abdbabeb2c64e078cfe5b8db1d29f69)


不同计算场景 列式存储 如何扫描内存

- 计算所有 Unit Price 的和
	- 直接扫描 Unit Price 列
- 计算所有 红色产品的 Unit Price 的和
	- 先扫描 Color 列，记住红色产品位置
	- 再扫描 Unit Price 列，只扫描对应的位置，然后计算求和
- 单价高于 $50 的蓝色或黑色产品的总和
	- 基于多列的条件 还是逐行扫描吧


## 2 理解 VertiPaq 压缩


### 2.1 值编码 Value Encoding

![6a5581bf6aea4faeaf4453a574f2da61|628](https://s1.vika.cn/space/2024/07/04/6a5581bf6aea4faeaf4453a574f2da61)

- 通过对所有值的加减法，可以调整所有值的区间范围，从而可以使用更小的 bits
- 可以发生在聚合之前或者聚合之后，**提高了 CPU 使用率减少了数据读取量**
- **整数类型** / **货币数据类型**


### 2.2 哈希编码 Hash Encoding

![](https://s1.vika.cn/space/2024/07/04/0e59e6f72568437fb63b5ca7d7ca0e24)


编码操作

1. 生成一个字典，包含列的所有值
2. 将列替换为整数，每个数字是原始值的索引


- 字符串类型 / 64 位整型 / 浮点数类型 都可以使用
- 决定列大小的主要因素不再是数据类型，而是列的不同值的数量 **基数 Cardinality**


### 2.3 行程长度编码  Run Length Encoding（RLE）

![6238eefc1e9946868898c531ad99ab28|509](https://s1.vika.cn/space/2024/07/04/6238eefc1e9946868898c531ad99ab28)


- 为了避免存储重复值，换成指包含该值与相同值的连续行数
- 低 Cardinality 的场景压缩比高，
- **频繁变化的列中，压缩比会变低，甚至占用更多的空间**
	- 如果是这种场景 VertiPaq 会重新选择不使用 RLE 编码
- 可以配合 哈希编码/值编码 使用

![79a4560ac1c24bfd9d06185c0c7790b7|531](https://s1.vika.cn/space/2024/07/04/79a4560ac1c24bfd9d06185c0c7790b7)



影响表格模型压缩率因素排序

1. Cardinality
2. 重复次数
3. 表的行数
4. 数据类型：只影响字典大小


### 2.4 再编码

- 可能根据最初的数据样本判断可以用 **值编码**
- 但是突然出现的离群值可能造成使用 **哈希编码** 更合适

SSAS 不会继续使用错误选择，而是对列重新进行编码



### 2.5 最佳排序顺序


- RLE 压缩率很大程度上取决于排序顺序
- 同一张表所有列必须遵循相同的排序
- 有一个配置可以设定寻找最佳排序的上限时间 百万行10s PBI 不能调整
- 通常重复值最少少的列适合放在排序的首位
- 计算列
	- 先计算再压缩
	- 但是由于选择最佳排序的时候不考虑计算列，所以计算列的压缩效果肯定不是特别好
- 计算表
	- 没有计算列的副作用，压缩比很好
	- 但是因为要创建副本，所以需要的内存比较大


### 2.6 层级/关系

- 关系存储为 行号 的配对表

![5905ab9b149d497ca654067e017a0787|501](https://s1.vika.cn/space/2024/07/04/5905ab9b149d497ca654067e017a0787)


## 3 理解分区分段


![](https://s1.vika.cn/space/2024/07/04/1713dc944c874244bac700cde956dbbb)
 [Source: SSAS Tabular – SQLML](https://sqlml.azurewebsites.net/2017/05/10/ssas-tabular/)


- 存储引擎只有存在多Segement 的时候才会触发多线程
- 分 Segment 有好处也有缺点
	- 分段多：可以多线程计算，需要更多时间处理不同线程的结果
	- 分段少：提升压缩率，处理速度慢

## 4 使用动态管理视图

使用 VertiPaq Analyzer / DAX
 Studio 来查看模型信息

![](https://s1.vika.cn/space/2024/07/04/6f6fea5ff4a7444ab4b6a35053c417c3)


# 理解 关系在VertiPaq 中的运用

查询 Product 表中 Brand 为 "Contoso" 的行数

可以理解为如下 Dax 代码算法

```javascript
EVALUATE
ROW (
	"Result", SUMX (
		Sales,
		IF ( RELATED ( 'Product'[Brand] ) = "Contoso", 1, 0 )
	)
)
```


![782e3d3e65fc4d2da5ffac13a69bca0b|554](https://s1.vika.cn/space/2024/07/04/782e3d3e65fc4d2da5ffac13a69bca0b)

![ceacc061e1934a74befbfbe106998626|560](https://s1.vika.cn/space/2024/07/04/ceacc061e1934a74befbfbe106998626)

1. 扫描 Brand 列 的字典表 检索 Contoso 的编码
2. 检索 Segments 搜索 Product 中字典ID为0的 行号
3. 产出 Product 行号
4. 通过 Product 行号 检索 关系表，将 Product 行号 转化为 Sales 行号
5. 产出 Sales 行号
6. 将行号 筛选应用与 Sales 表



**使用关系的成本取决于定义关系列的基数**
 **the cost of a relationship depends on the cardinality of the column that defines the relationship**




# 物化介绍

这里完全没有看懂, 还是看视频总和理解

[Inside The VertiPaq Engine by Marco Russo](https://www.youtube.com/watch?v=-IxO8eFHR2s)


**物化：将压缩编码存在内存中的数据，转化为未压缩的状态**

![](https://s1.vika.cn/space/2024/07/10/873f504f00eb4b06a760919fd3ce715b)

![](https://s1.vika.cn/space/2024/07/10/c08a56127c724cf48e94eb6b50f9301b)


为了生成用户最总需要的结果，先对压缩数据进行筛选，再物化，这种 Late Materialization 占用内存更小，扫描更快。

![](https://s1.vika.cn/space/2024/07/10/cf47142a242e4089980cffce8e8368c7)



# 聚合表介绍

![4da886e8994b4c6c841f933e9e9ce262|481](https://s1.vika.cn/space/2024/07/04/4da886e8994b4c6c841f933e9e9ce262)

![c46aa1f3bee84b11a6ab71bfdb0ea96d|489](https://s1.vika.cn/space/2024/07/04/c46aa1f3bee84b11a6ab71bfdb0ea96d)

- 只能映射原生表中的原生列，计算列不能设置聚合
- 性能参考
	- DQ 对较小的表 也是有用的
	- VertiPaq 十亿行以上的数据再考虑


# 为VertiPaq 配置合适的硬件

