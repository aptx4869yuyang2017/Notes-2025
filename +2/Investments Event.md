---
up: []
related:
created: 2025-09-14
tags:
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
