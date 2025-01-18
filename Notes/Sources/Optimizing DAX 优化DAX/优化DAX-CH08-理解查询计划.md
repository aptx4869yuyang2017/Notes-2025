---
up:
  - "[[Optimizing DAX 优化DAX(book)]]"
related: 
year: 
created: 2024-08-25
tags: 
type: "[[Chapter]]"
ch: "08"
finished: 2024-08-26
aliases:
---

### 1 查询计划结构

![](https://s1.vika.cn/space/2024/08/24/d56322c0d9d74b60911a06f50e24faf6)

**物理**
![35674f81dbc7465283b5e0211e20c56d|747](https://s1.vika.cn/space/2024/08/24/35674f81dbc7465283b5e0211e20c56d)
**逻辑**
![](https://s1.vika.cn/space/2024/08/25/b62a6f7e7b4f45a0b86197f094404c28)

树状结构
- 每行代表一个 operator
	- Operator 名字
		- AddColumns
	- Operator 类型
		- 逻辑查询计划常用 ScaLogOp / RelLogOp
		- 物理查询计划常用 LookupPhyOp/ IterPhyOp / SpoolPhyOp
	- Operator 属性
- 缩进子节点代表 operands


### 2 查询计划 Operator 类型

![7d1c634302a245efa9e13bdb323429df|624](https://s1.vika.cn/space/2024/08/24/7d1c634302a245efa9e13bdb323429df)

- Logic
	- ScaLogOp
		- 产出标量
	- RelLogOp
		- 产出列表 / 行表
- Physic
	- LookupPhyOp
		- 将当前行作为输入，计算并返回一个标量值。
	- IterPhyOp
		- Given a current row as an optional input, it returns a sequence of rows
		- 如果将当前行作为可选输入，则返回行序列。
	- SpoolPhyOp
		- 读取数据缓存，并将其用于查询计划的下一步。


#### 2.1 ScaLogOp 属性

![](https://s1.vika.cn/space/2024/08/26/f7811592089648edadc18b801c3bdabe)

- DependsOnCols 依赖列
	- - 这种依赖关系从查询计划的叶节点开始，逐步向上传播，直到不再需要这些依赖。
- 数据类型
- DominantValue 显性值





#### 2.2 RelLogOp 属性


![](https://s1.vika.cn/space/2024/08/26/c895df58428b4982aff3e196a79e29c0)

- Relation 描述的是列之间的关系，也就是表


- DependsOnCols
	- 同 ScaLogOp
- Range of columns 产生结果需要的列号
- RequiredCols
	- 虽然拓展表有 68列，但是实际需要的就只有 三列 0/7/9

#### 2.3 LookupPhyOp 属性

![](https://s1.vika.cn/space/2024/08/26/62627e27598b49e2949f2a9f864fe272)


- 负责为父操作提供值
- 依据 LookupCols
- KeyCols 来自 original data
- ValueCols 来自 calculation 计算

#### 2.4 IterPhyOp 


![](https://s1.vika.cn/space/2024/08/26/d100e270ed744590960cd128defeb1c9)

- LookupCols 生成输出列，需要的列（本案例没有）
- IterCols 输出中包含的列
- Lookup / Iter  是否展示的差异
	- 只有 **Iter** ，纯迭代器，返回表格。输入表，返回指定列的所有行
	- **都有** 根据 Lookup 判断要生成哪些行，不仅仅是返回表格
	- **只有 Lookup**  行检查器，主要用于过滤数据，比如从spool 中移除没用的行，没有产出的表


#### 2.5 SpoolPhyOp 属性

![](https://s1.vika.cn/space/2024/08/26/e3b81801e538448293c87d9b933386e4)

- SpoolPhyOp 作用是读取数据缓存（datacache），并将这些数据提供给查询计划中的后续步骤
- 最重要的作用是看 Cache 有多少数据，因为 Cache 本身没有展示这个数据

### 3 FE / SE 发生交互的表现


- SE 查询 出现 CallbackDataID
- **物理查询计划** Cache 出现在了非叶节点 leaf level

原因

- 调用了 SE 没有的函数
- FE 计算了一个 SE 需要的过滤条件


### 4 一般 查询计划 Operator


![](https://s1.vika.cn/space/2024/08/25/186308fe70ce43dfb403e4e911878ec3)
![](https://s1.vika.cn/space/2024/08/25/8d56db1ad5db4767912efeea0fda1af0)
![](https://s1.vika.cn/space/2024/08/25/302847a2d0d64df5ab1293422768bcc8)

#### 4.1 逻辑查询运算符

| 操作符              | 描述                                                                                                                                                                                                                                              |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AddColumns       | Adds columns to a table.  <br>向表中添加列。                                                                                                                                                                                                           |
| Calculate        | Calculates a scalar expression by applying specific filters. It corresponds to the CALCULATE function in DAX.  <br>通过应用特定过滤器计算标量表达式。它对应于DAX中的CALCULATE函数。                                                                                       |
| CalculateTable   | Calculates table expression by applying specific filters. It corresponds to the CALCULATETABLE function in DAX.  <br>通过应用特定过滤器计算表表达式。它对应于 DAX 中的 CALCULATETABLE 函数。                                                                             |
| Filter_VertiPaq  | Returns a table usually applied as a filter to a Calculate operator.  <br>返回通常用作计算运算符的过滤器的表。                                                                                                                                                    |
| GroupBy_VertiPaq | Performs group by of the table using the specified columns.  <br>使用指定的列对表执行分组。                                                                                                                                                                  |
| GroupSemiJoin    | Joins the result of two operators, returning all the rows in the first table if there is a match with the result of the second operator.  <br>连接两个运算符的结果，如果与第二个运算符的结果匹配，则返回第一个表中的行。                                                             |
| ScalarVarProxy   | Returns the value of a scalar variable computed inside a variable scope introduced with the VarScope operator.  <br>返回在 **VarScope** 运算符引入的变量范围内计算的标量变量的值。                                                                                      |
| Scan_Vertipaq    | Performs the scan of a table using the VertiPaq storage engine.  <br>使用 VertiPaq 存储引擎执行表扫描。                                                                                                                                                     |
| Sum_Vertipaq     | Performs SUM aggregation using the VertiPaq storage engine. Similar operators are available for MIN, MAX, and COUNT aggregations.  <br>使用 VertiPaq 存储引擎执行 SUM 聚合。类似的运算符可用于 MIN、MAX 和 COUNT 聚合。                                                  |
| TableVarProxy    | Returns the value of a table variable computed inside a variable scope introduced with the VarScope operator.  <br>返回在 **VarScope** 运算符引入的变量范围内计算的表变量的值。                                                                                        |
| **VarScope**     | Opens variable scope. It contains a list of variable definitions defined with the VarName property. The result of the VarScope operator is the last operator in the scope.  <br>打开变量范围。它包含使用 VarName 属性定义的变量定义列表。 VarScope 运算符的结果是作用域中的最后一个运算符。 |

#### 4.2 物理查询运算符

| 操作符              | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AggregationSpool | Aggregates the result of a Cache operator, by aggregating some of the columns contained in the datacache.  <br>通过聚合数据缓存中包含的一些列来聚合缓存运算符的结果。                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Cache 缓存         | Identifies the use of a datacache. Retrieves the content of a datacache returned by a storage engine query. In a single query plan, there might be several Cache operators reading the same datacache. In this scenario, there will be a single storage engine query generating the datacache, which is then consumed in different parts of the query plan.  <br>标识数据缓存的使用。检索存储引擎查询返回的数据缓存的内容。在单个查询计划中，可能有多个缓存运算符读取相同的数据缓存。在这种情况下，将有一个存储引擎查询生成数据缓存，然后在查询计划的不同部分中使用。                                                                                                             |
| CrossApply       | Performs the Cartesian product (cross-join) between two tables. The cardinality of the resulting table is not exposed directly. If the result is immediately consumed by a Spool operator, then the resulting number of records is visible. However, if a Filter operator is executed before any spool, the number of records produced by the CrossApply and then filtered is not visible and you can see only the number of filtered rows.  <br>在两个表之间执行笛卡尔积（交叉联接）。结果表的基数不直接公开。如果 Spool 运算符立即使用结果，则结果记录数是可见的。但是，如果 Filter 运算符在任何假脱机之前执行，则 CrossApply 生成然后过滤的记录数不可见，您只能看到过滤的行数。 |
| DataPostFilter   | Retrieves a subset of rows from a datacache resulting from a vertical fusion operation. While Cache retrieves the entire datacache, DataPostFilter retrieves some of the values based on a filter condition.  <br>从垂直融合操作产生的数据缓存中检索行的子集。 Cache 检索整个数据缓存，而 DataPostFilter 根据过滤条件检索部分值。                                                                                                                                                                                                                                                                                           |
| Filter           | Filters one table thus reducing the number of rows.  <br>过滤一张表，从而减少行数。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| GroupSemiJoin    | Groups two tables by performing a semi-join.  <br>通过执行半连接对两个表进行分组。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| InnerHashJoin    | Performs an inner join between two tables.  <br>在两个表之间执行内连接。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ProjectionSpool  | Projects the result of a Cache operator; selects some of the columns contained in the datacache.  <br>投影 Cache 运算符的结果；选择数据缓存中包含的一些列。                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| SpoolIterator    | Summarizes a table by performing one aggregation (sum/count/distinct count/min/max/average) over a value obtained from an expression (or a column in simpler cases) and grouping by one or more columns of the original table.  <br>通过对从表达式（或简单情况下的列）获得的值执行一次聚合（总和/计数/非重复计数/最小值/最大值/平均值）并按原始表的一列或多列进行分组来汇总表。                                                                                                                                                                                                                                                                    |
| SpoolLookup      | Summarizes a table by performing an aggregation (sum/count/distinct count/min/max/average) over a value obtained from an expression (or a column in simpler cases). Returns a single value.  <br>通过对从表达式（或更简单情况下的列）获得的值执行聚合（总和/计数/非重复计数/最小值/最大值/平均值）来汇总表。返回单个值。                                                                                                                                                                                                                                                                                                                 |
| TableCtor        | Builds a table from a table constructor syntax.  <br>从表构造函数语法构建表。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| TreatAs          | Changes the data lineage of a table (like TREATAS in DAX).  <br>更改表的数据沿袭（如 DAX 中的 TREATAS）。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### 5 案例

#### 5.1 SUM vs SUMX

> [!important] 
> 查询计划是如何处理普通聚合的


案例：L06

- SUMMARIZECOLUMNS
	- 使用 GroupSemiJoin 
	- 物理查询会简化查询次数 2 -> 1
- ADDCOLUMNS
	- 使用 ADDCOLUMNS

#### 5.2 IF vs IF.Eager

> [!important] 
> 查询计划是如何处理 条件判断的


[Understanding eager vs. strict evaluation in DAX - SQLBI](https://www.sqlbi.com/articles/understanding-eager-vs-strict-evaluation-in-dax/)

案例：L07

- Strict Evaluation 严格计值
- Eager Evaluation 急切计值


![ca15da512a8e46ae82f4d7d7a0e7e5ac|469](https://s1.vika.cn/space/2024/08/27/ca15da512a8e46ae82f4d7d7a0e7e5ac)

**Eager Evaluation 急切计值 的粗略 逻辑查询计划**
- AddColumn
	- 扫描 Color
	- 变量作用域
		- 算 Margin 定义 **变量A**
			- 算 Sales Amount
			- 算 Total Cost
		- 算 Total Cost 定义 **变量B**
		- IF 判断 
			- less than Sales Amount < 1E7
			- PredicateCheck 根据 Color 分组
			- 根据变量 获取对应的值


#### 5.3 使用 DAX 筛选 vs 关系

> [!important] 
> 查询计划是如何处理 
> - **关系** 
> - **变量**


案例：L08

![93530f52e8064f34b6f2a8d7740fd65b|425](https://s1.vika.cn/space/2024/08/25/93530f52e8064f34b6f2a8d7740fd65b)

因为没有关系，所以必须使用 Filter 来过滤 Sales

- 找到当前 筛选上下文 的所有 P - key（触发了上下文转换）
- 对 Sales 表，用 P - key 筛选 S - key 
- 在 筛选表上 计算 指标 sumx


**VarScope的作用**

- `ADDCOLUMNS`的第二个参数是一个`VarScope`。`VarScope`用于引入一个变量范围，这意味着在这个范围内定义的变量在 **整个范围内有效**。
- `VarScope`的所有变量都依赖于当前迭代的`Product[Color]`列。这意味着这些**变量的值取决于当前处理的颜色**。


注意 **变量** 在不同 VarScope 中
- 计算的先后顺序
- 引用关系

![](https://s1.vika.cn/space/2024/08/27/aa7f4c9a9c414123a42cf0679ca409db)


`IN`操作符被转换为一对`Not`和`IsEmpty`操作符

**整个算法相当线性，因此主要问题预计出现在`SalesOfProds`变量的检索上。由于按行号分组，这个变量需要包含`Sales`表中的所有行，这会导致大量的数据物化**

生成/处理 都会有性能损耗



#### 理解 Switch 优化


[Understanding the optimization of SWITCH - SQLBI](https://www.sqlbi.com/articles/understanding-the-optimization-of-switch/)

案例：L09

**场景**

- 我们已经知道了 IF / IF.Eager 在 引擎中处理的差异
- 场景：通过切片器改变参数表，根据需求改变报表内容

![7d3cc0812417402fb2f1d856ebcdebd5|444](https://s1.vika.cn/space/2024/08/28/7d3cc0812417402fb2f1d856ebcdebd5)

![3323601290c74e8b95b987372dc8c6c6|478](https://s1.vika.cn/space/2024/08/28/3323601290c74e8b95b987372dc8c6c6)


![463d45e1ac894a7f9dada491f30185ee|515](https://s1.vika.cn/space/2024/08/28/463d45e1ac894a7f9dada491f30185ee)

物理查询计划框架


- GroupSemiJoin
	- Extend_Lookup 根据IF的不同乘数，乘出结果
		- CrossApply 笛卡尔积
			- 6行 三个条件组成的表
			- 9行 Sales Amount
		- IF 判断
			- 红框为判断条件


场景升级1: 增加分组维度 City：只是增加了处理时间

场景升级2: Scenario 只作为切片器

![](https://s1.vika.cn/space/2024/08/28/436cd41ab89d4954b14c552156dd9176)

![c3ef8329e7b047b58671f6a63af2a102|533](https://s1.vika.cn/space/2024/08/28/c3ef8329e7b047b58671f6a63af2a102)

- 查询计划中 IF 判断不存在了，引擎提前知道 0.9 是唯一值
- 这种针对条件逻辑的优化，建立在**引擎能够静态理解，只有一行数据是有效的**

![61904c0be05f4f0ea60307cbb9c60555|513](https://s1.vika.cn/space/2024/08/28/61904c0be05f4f0ea60307cbb9c60555)
- 发人员可能更倾向于使用 `Scenario[Sort Order]` 列，而不是 `Scenario[Scenario]` 列，因为代码相比字符串更稳定，不会随着时间发生变化
- 但是可能造成**引擎推断不出来唯一有效值**

[Understanding Group By Columns in Power BI - YouTube](https://www.youtube.com/watch?v=xtb5i4sUOTk)

有点困，下次不困了再看

