---
up:
  - "[[Home]]"
related:
  - "[[Relate 相关]]"
  - "[[Communicate 交流]]"
created: 2022-01-01
obsidianUIMode: preview
tags:
  - map/view
---
This **Add** note isn't just an inbox. It's a cooling pad 🧊.
Thoughts come in hot. But after a few days, they cool down.
When cooler thoughts prevail, you can better prioritize. Cool? 

这个 **ADD** 笔记不仅仅是一个收件箱。它是一个冷却垫 🧊。
思绪汹涌而来。但几天后，它们就会冷却下来。
当冷静的想法占据上风时，你就能更好地确定优先顺序。Cool？


> [!activity]+ ## Added Stuff
> This view looks at the 10 newest notes in your **+** folder. As you process each note: add a link, add details, move them to the best folder,  and delete everything that no longer sparks ✨. 
> 
> ``` dataview
> TABLE WITHOUT ID
>  file.link as "",
>  (date(today) - file.cday).day as "Days alive"
> 
> FROM "+" and -#x/readme 
> 
> SORT file.cday desc
> 
> LIMIT 20
> ```

> [!Notes]- This data view 🔬 only renders in the downloadable version.
> You won't be able to see the magic unless you download the kit, but here's kind of what it looks like in "Ideaverse for Obsidian"
> ![[lyt-kit-example-cooling-pad-.png]]

---

If you want to encounter some new things, check out: [🐦](https://www.twitter.com) or [📚](https://readwise.io/lyt/)          