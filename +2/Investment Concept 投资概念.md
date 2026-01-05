---
up:
  - "[[Investments MOC]]"
related:
created: 2025-11-22
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
    sort:
      - property: file.name
        direction: ASC

```