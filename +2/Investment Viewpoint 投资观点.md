---
up:
  - "[[Investments MOC]]"
related:
created: 2025-09-05
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