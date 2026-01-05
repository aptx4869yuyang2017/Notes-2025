---
up:
  - "[[PowerBI MOC]]"
related:
created: 2025-11-16
tags:
  - map
---



```base
filters:
  and:
    - related.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
```