---
up:
related:
created: 2025-08-11
tags:
  - domain/math
---


```base
views:
  - type: table
    name: Table
    filters:
      and:
        - up.contains(link("Math Concept 数学概念 MOC"))
    order:
      - created
      - file.name
      - related
    sort:
      - property: created
        direction: DESC
      - property: file.ctime
        direction: DESC
    columnSize:
      note.created: 118
      file.name: 198
      note.related: 361
  - type: cards
    name: View
    filters:
      and:
        - up.contains(link("Math Concept 数学概念 MOC"))
    sort:
      - property: file.ctime
        direction: DESC

```








