---
created: ""
tags:
  - domain/data
type: "[[Chapter]]"
up:
  - "[[DAX 权威指南(book)]]"
related: 
ch: "09"
finished:
---

![420](https://s1.vika.cn/space/2024/04/01/77daa94294de4012bac9444a62dc0958)
![82117f3117104b62847fd5e7e62964cc|420](https://s1.vika.cn/space/2024/04/01/82117f3117104b62847fd5e7e62964cc)

因为出版时候没有计算组功能所以有了这个在线版
[Site Unreachable](https://www.sqlbi.com/calculation-groups/)

## 介绍计算组




## 创建计算组




## 理解计算组


[Introducing Calculation Groups - SQLBI](https://www.sqlbi.com/articles/introducing-calculation-groups/)

- 计算组和计算项是两个实体
- 计算组是被归为一组的计算项集合
- 


### 1 理解计算项的应用

![7a2265c07ff741ac9e1cbd5a30443e01|299](https://s1.vika.cn/space/2024/04/01/7a2265c07ff741ac9e1cbd5a30443e01)

![363d223e5993477a9bc79497e7f970d0|293](https://s1.vika.cn/space/2024/04/01/363d223e5993477a9bc79497e7f970d0)





### 2 理解计算组优先级


![50354a29d8804636893e26d0b465156b|365](https://s1.vika.cn/space/2024/04/02/50354a29d8804636893e26d0b465156b)
![e6994d7ca4164e3e8fe2bf9a935863a2|367](https://s1.vika.cn/space/2024/04/02/e6994d7ca4164e3e8fe2bf9a935863a2)

我在 Tabular Editor 中没有找到 优先级的这个选线，不过现在已经可以在 Powerbi 中直接编辑了。

### 3 在计算项中包含或者排除度量值

```
IF (
    NOT ISSELECTEDMEASURE ( [Margin %] ),
    DIVIDE (
        SELECTEDMEASURE (),
        COUNTROWS ( 'Date' )
    )
)
```

涉及某些 度量值可以不参与计算

**IsSelectedMeasere**



## 理解横向递归 sideways recursion


## 使用最佳实践
