---
up:
  - "[[Sources Map]]"
related: []
created: 2022-01-01
---

```base
filters:
  and:
    - type.contains(link("Movie-Series"))
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
    order:
      - year
      - file.name
      - created
      - finished
      - short
    sort:
      - property: created
        direction: DESC
    columnSize:
      note.year: 79
      file.name: 248
      note.created: 120
      note.finished: 122
      note.short: 109

```




