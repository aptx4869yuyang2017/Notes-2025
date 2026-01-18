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



```base
filters:
  and:
    - related.contains(this.file.name)
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