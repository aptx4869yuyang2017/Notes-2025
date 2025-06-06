---
up: 
related: 
year: 2021
created: 2025-02-15
tags:
  - domain/powerbi
type:
---


```
import seaborn as sns
tips = sns.load_dataset("tips")
```


```
# 下面用于创建数据帧并删除重复行的代码始终执行，并用作脚本报头: 

# dataset = pandas.DataFrame(day, total_bill)
# dataset = dataset.drop_duplicates()

# 在此处粘贴或键入脚本代码:
import seaborn as sns
import matplotlib.pyplot as lib
sns.swarmplot(x="day", y="total_bill", hue="sex", data=dataset, size=12)
lib.show()
```



# 参考



[Youtube](https://www.youtube.com/watch?v=3_DOF_qjguA&t=320s)
[seaborn.swarmplot — seaborn 0.13.2 documentation](https://seaborn.pydata.org/generated/seaborn.swarmplot.html)



