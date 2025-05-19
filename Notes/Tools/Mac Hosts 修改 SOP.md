---
up: 
related: 
created: 2024-09-02
tags:
  - tools/sop
---



其实锁住一行就行：  
sudo chflags schg,uchg /etc/hosts  
  
解开：  
sudo chflags noschg,nouchg /etc/hosts