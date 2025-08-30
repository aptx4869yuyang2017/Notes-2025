---
up:
related:
created: 2025-08-21
tags:
  - map
---

```base
formulas:
  Untitled: format([created time])
properties:
  formula.Untitled:
    displayName: created
views:
  - type: table
    name: Table
    filters:
      and:
        - up.contains(link("研究报告 MOC"))
    order:
      - file.name
      - created
      - file.ctime
    sort:
      - property: file.ctime
        direction: ASC

```


