---
up:
  - "[[Investments MOC]]"
related:
  - "[[Investment Target 投资标的]]"
created: 2026-01-01
tags:
  - map
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


