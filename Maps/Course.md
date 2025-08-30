---
up:
  - "[[Sources Map]]"
related: []
created: 2022-01-01
---


```base
filters:
  and:
    - type.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
    order:
      - file.name
      - tags
    sort:
      - property: file.ctime
        direction: DESC

```






> [!map]- 课程
> ```dataview
> table dateformat(created, "yy-MM-dd") as Created
> where contains(type, this.file.link) and !contains(file.name, "Template")
> sort created desc
> ```
