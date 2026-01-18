---
up: []
related: 
created: 2026-01-10
tags:
---

[ym:: "2026-02"]

# 总结

```dataviewjs
// ====== 配置区 ======
const targetMonth = dv.current().ym; // 如 "2026-02"
const [targetYear, targetMonthNum] = targetMonth.split("-").map(Number);


// ====== 数据筛选 ======
const pages = dv.pages()
  .where(p => 
    p.created && 
    p.created.year === targetYear && 
    p.created.month === targetMonthNum
  );

// ====== 按日期分组（day → [links]）======
const dayGroups = {};
for (let p of pages) {
  const day = p.created?.day;
  if (day && Number.isInteger(day) && day >= 1 && day <= 31) {
    if (!dayGroups[day]) dayGroups[day] = [];
    dayGroups[day].push(p.file.link);
  }
}

// ====== 渲染 ======

dv.paragraph(`**总计笔记数**：${pages.length} 篇\n\n\n`);

if (pages.length === 0) {
  dv.paragraph("📅 本月暂无笔记。");
} else {
  dv.paragraph("### 📅 每日笔记数量");
  
  // 排序日期（1, 2, ..., 31）
  const sortedDays = Object.keys(dayGroups)
    .map(Number)
    .filter(d => d >= 1 && d <= 31)
    .sort((a, b) => a - b);
  
  // 可视化条形图（最多5格，防过长）
  for (let day of sortedDays) {
    const count = dayGroups[day].length;
    const bar = "█".repeat(Math.min(count, 5));
    dv.paragraph(`${day.toString().padStart(2,'0')}日: ${bar} ${count}篇`);
  }
}
```


# 领域统计

```dataview
table length(rows) AS "数量" 
FROM "" 
WHERE dateformat(created, "yyyy-MM") = "2026-02" FLATTEN tags 
GROUP BY tags SORT length(rows) DESC
```


# 每日明细


```dataview
TABLE WITHOUT ID
	date,
  rows.file.link AS 笔记
  //rows.file.tags
FROM ""
WHERE dateformat(created, "yyyy-MM") = "2026-01"
GROUP BY dateformat(created, "dd") AS date
SORT date
```




