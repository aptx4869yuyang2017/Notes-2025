---
up:
related:
created: 2025-10-02
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