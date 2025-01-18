---
created: {{date}}
---

## Daily


## Notes

> [!summary]+ Today Notes
> ```dataview
> list
> where created = date(this.created)  and file.name != this.file.name
> ```