---
up: 
related: 
created: 2024-02-28
tags:
  - tools/sop
---

[Docker部署Odoo 系统 - 知乎](https://zhuanlan.zhihu.com/p/668109554)

```yaml
version: '3.1'
services:
  web:
    image: odoo:16.0
    container_name: odoo16
    restart: always  # 总是重新启动容器
    depends_on:
      - db  # 依赖于名为db的服务
    ports:
      - "8069:8069"  # 映射端口 8069 到宿主机端口 8069，ODOO默认使用的是8069端口
    volumes:
      - odoo-web-data:/var/lib/odoo  # 映射数据卷，用于保存Odoo的数据
      - ./config:/etc/odoo  # 映射配置文件目录
      - ./addons:/mnt/extra-addons  # 映射附加模块目录

  db:
    image: postgres:15
    container_name: odoo16_db
    restart: always  # 总是重新启动容器
    environment:
      - POSTGRES_DB=postgres  # 设置数据库名称为postgres
      - POSTGRES_PASSWORD=odoo  # 设置数据库密码为odoo
      - POSTGRES_USER=odoo  # 设置数据库用户为odoo
      - PGDATA=/var/lib/postgresql/data/pgdata
    volumes:
      - odoo-db-data:/var/lib/postgresql/data/pgdata  # 映射数据卷，用于保存PostgreSQL的数据

volumes:
  odoo-web-data:  # Odoo数据卷
  odoo-db-data:  # PostgreSQL数据卷
```