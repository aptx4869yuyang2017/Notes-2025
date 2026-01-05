---
up:
  - "[[Sources Map]]"
related: 
created: 2024-01-01
---

```base
views:
  - type: table
    name: Table
    filters:
      and:
        - and:
            - type == link("Book")
            - '!file.name.contains("Template")'
    order:
      - created
      - file.name
      - year
      - finished
      - tags
    sort:
      - property: created
        direction: DESC
      - property: file.name
        direction: DESC
    columnSize:
      note.created: 115
      file.name: 254
      note.finished: 103

```





