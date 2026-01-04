---
up: 
related: 
year: 
created: 2024-12-29
tags:
  - domain/investment
type: "[[Company]]"
aliases:
---

```base
filters:
  and:
    - file.name.contains("格力电器")
    - '!file.name.contains("Template")'
views:
  - type: table
    name: Table

```