---
up:
  - "[[Econ Fin 经济金融 Map]]"
related: 
created: 2025-06-17
tags:
  - map
---


```base
filters:
  and:
    - up.contains(this.file.name)
properties:
  related:
    displayName: realted
  file.name:
    displayName: note
  file.path:
    displayName: path
views:
  - type: table
    name: Table
    order:
      - file.name
      - related
      - file.path
    columnSize:
      file.name: 270

```




> [!map]- Data 备份
> ```dataview
> table created
> where contains(up, this.file.link) and !contains(file.name, "Template")
> sort file.name
> ```


