---
up:
  - "[[PowerBI DAX Function 函数]]"
related:
  - "[[DAX 权威指南 - CH03 基础表函数]]"
created: 2024-12-07
---



表 -> 表函数 -> 表
**表函数 输入和输出都是表**


- 标量表达式概念
- 就算是返回标量函数，参数也会用到表
	- **SUMX 函数中参数需要提供一个表，用来遍历，这个位置可以用表函数返回结果替换**
	- ![400](https://s1.vika.cn/space/2024/03/20/c84ce937849f4235b0afed095936768d)
	- 注意不是**最佳实践**，后面会有 **Calculate** 详见 [[DAX 权威指南 - CH04 理解计值上下文EC]]
- **变量 既可以存标量，也可以存表**
	- ![400](https://s1.vika.cn/space/2024/03/20/82715af319174abcad8041ba1f4112ff)
- RelatedTable 可以获取相关表
- **表函数可以嵌套**
	- **计值顺序，由内向外**
	- 这个是 Product 表的 **计算列**， 存在一个默认的对 Product 的遍历
	- ![400](https://s1.vika.cn/space/2024/03/20/d7fef2f3fe3344cd979e041c7b73b527)
	- Filter 嵌套 RelatedTable，先对RelatedTable记值，然后是 Filter
- **表函数的结果不能直接用于 计算列/度量值，但是可以直接用作 calculated table 计算表（虚拟表）**
	- ![300](https://s1.vika.cn/space/2024/03/20/da66e072beef4b259adbb0c6cb4da032)