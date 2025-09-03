---
up:
  - "[[Accounting 会计 Map]]"
related:
created: 2025-09-02
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