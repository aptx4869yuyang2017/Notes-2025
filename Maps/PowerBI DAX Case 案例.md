---
up:
  - "[[Power BI MOC]]"
  - "[[PowerBI DAX Function 函数]]"
related: 
created: 2024-12-08
---
```base
filters:
  and:
    - up.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
```







 > [!important]- 案例清单
> 
> 
> ```dataview
> LIST
> where up[0] = [[PowerBI DAX Case 案例]]
> SORT file.cday desc
> ```
