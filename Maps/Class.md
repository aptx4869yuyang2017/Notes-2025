---
up:
  - "[[Home]]"
related: 
created: 2025-08-12
tags:
  - map
---


```base
views:
  - type: table
    name: Table
    filters:
      and:
        - and:
            - type == link("Class")
            - '!file.name.contains("Template")'
    order:
      - file.name
      - created
      - finished
    sort:
      - property: file.name
        direction: DESC
      - property: file.ctime
        direction: DESC
    columnSize:
      file.name: 459
      note.created: 118

```











> 
> [!map]+ 课程
> ```dataview
> table dateformat(created, "yy-MM-dd") as Created
> where contains(type, this.file.link) and !contains(file.name, "Template")
> sort created desc
> ```


