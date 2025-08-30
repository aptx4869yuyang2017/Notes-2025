---
up:
  - "[[Home]]"
related:
created: 2025-08-22
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