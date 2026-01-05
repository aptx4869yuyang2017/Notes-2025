---
up:
  - "[[PowerBI MOC]]"
related:
created: 2025-09-13
tags:
  - map
---

```base
filters:
  and:
    - up.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: cards
    name: View
    order:
      - file.name
    sort:
      - property: file.ctime
        direction: DESC
    image: note.cover
  - type: table
    name: Table
  - type: table
    name: View 2

```

