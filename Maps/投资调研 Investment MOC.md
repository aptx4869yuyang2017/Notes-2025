---
up:
  - "[[Investments MOC]]"
related:
created: 2025-08-13
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
      - property: file.ctime
        direction: DESC

```


