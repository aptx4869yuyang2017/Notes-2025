---
up:
  - "[[会计 Accounting Map]]"
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
    order:
      - file.name
      - created
    columnSize:
      file.name: 352

```