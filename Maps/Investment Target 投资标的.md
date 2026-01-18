---
up:
  - "[[00-Home]]"
related:
  - "[[Investments MOC]]"
created: 2024-12-29
tags:
  - map
---

```base
filters:
  or:
    - and:
        - type.contains(this.file.name)
        - '!file.name.contains("Template")'
    - and:
        - up.contains(this.file.name)
        - '!up.contains("Template")'
views:
  - type: table
    name: Table
    order:
      - file.name
      - created
    sort:
      - property: file.mtime
        direction: DESC

```



