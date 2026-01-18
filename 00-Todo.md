


[[Book]]


- [[财务报表分析与证券估值(book)]]
	- [[财务报表分析与证券估值-CH07 估值与主动投资]]
	- [[财务报表分析与证券估值-CH08 透过财务报表看企业]]
- [[股市真规则(book)]]
- [[巴菲特致股东信]]
- [[快速了解一个行业(book)]]


[[可汗学院-金融与资本市场(course)]]





```dataview
TABLE WITHOUT ID
   标签 AS "标签",
   length(rows) AS "出现次数"
WHERE created AND created >= date(today) - dur(3 months) AND file.tags
FLATTEN file.tags AS 标签
WHERE regexmatch("^#domain/[^/]+$", 标签)
GROUP BY 标签
SORT length(rows) DESC
```


```dataview
TABLE WITHOUT ID
   标签 AS "标签",
   length(rows) AS "笔记数量",
   rows.file.link AS "包含的笔记"
WHERE created AND created >= date(today) - dur(3 months) AND file.tags
FLATTEN file.tags AS 标签
WHERE regexmatch("^#domain/[^/]+$", 标签)
GROUP BY 标签
SORT length(rows) DESC
```


