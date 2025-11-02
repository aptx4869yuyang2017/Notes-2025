---
up:
related:
  - "[[Figma]]"
created: 2025-09-23
tags:
  - map
---



[Figma 文件教程](https://www.figma.com/community/file/1393592818065741247)

```base
filters:
  and:
    - related.contains(this.file.name)
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table
    sort:
      - property: file.name
        direction: ASC

```