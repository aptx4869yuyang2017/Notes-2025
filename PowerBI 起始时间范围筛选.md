---
up: 
related: 
year: 
created: 2025-06-12
tags: 
type: 
url: https://smootherconsulting.com/learn/filter-power-bi-by-2-datetime-ranges
---

[Filter Power BI Report by 2 Date/Time Ranges — Smoother Consulting](https://smootherconsulting.com/learn/filter-power-bi-by-2-datetime-ranges)

[Filtering Date and Time Ranges in Power BI: Two Alternatives and Code Optimization \| by Mateusz Mossakowski \| Microsoft Power BI \| Medium](https://medium.com/microsoft-power-bi/filtering-date-and-time-ranges-in-power-bi-two-alternatives-and-code-optimization-335245fc9b4e)


DRC Offline = 1 - DIVIDE([N.I.O], [Total KANR])
修改为
DRC Offline = DIVIDE([Total KANR]-[N.I.O], [Total KANR])


```
hour_minute_num

Time.Hour([dts]) * 100 + Time.Minute([dts])

date_hour_minute_num

Time.Hour([dts]) * 100 + Time.Minute([dts]) 
+ Date.Year([dts]) * 1e8 + Date.Month([dts]) * 1e6 
+ Date.Day([dts]) * 1e4


hour_minute_15min_num

Time.Hour(#time(
    Time.Hour([dts]),
    Number.RoundDown(Time.Minute([dts])/15)*15,
    0
)) * 100 + Time.Minute(#time(
    Time.Hour([dts]),
    Number.RoundDown(Time.Minute([dts])/15)*15,
    0
))
```


```
DateTimeFilter = 
VAR _startdatetime = MIN( DateStart[Date Num] ) * 10000 + MIN( TimeStart[Hour Minute Num] )
VAR _enddatetime = MAX( DateEnd[Date Num] ) * 10000 + MAX( TimeEnd[Hour Minute Num] )
VAR _filtered_sales_fact =
    FILTER( FactData, FactData[Date Hour Min Num] >= _startdatetime && FactData[Date Hour Min Num] < _enddatetime )
RETURN
CALCULATE( SELECTEDMEASURE(), _filtered_sales_fact )
```
