---
created: 2024-01-11
tags:
  - tools/sop
---

- 更换账号密码 [postgresql 密码修改，忘记密码进行修改重置\_dbeaver修改pg数据库密码-CSDN博客](https://blog.csdn.net/sunny_day_day/article/details/107023722#:~:text=postgresql%20%E5%AF%86%E7%A0%81%E4%BF%AE%E6%94%B9%EF%BC%8C%E5%BF%98%E8%AE%B0%E5%AF%86%E7%A0%81%E8%BF%9B%E8%A1%8C%E4%BF%AE%E6%94%B9%E9%87%8D%E7%BD%AE%201%201%E3%80%81%E5%AF%86%E7%A0%81%E4%BF%AE%E6%94%B9%E7%BC%98%E7%94%B1%201%E3%80%81%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%AE%A4%E8%AF%81%E6%96%B9%E5%BC%8F%E4%B8%BA%E5%AF%86%E7%A0%81%E9%AA%8C%E8%AF%81%EF%BC%8C%E8%AE%BE%E7%BD%AE%E5%88%9D%E5%A7%8B%E5%AF%86%E7%A0%81%EF%BC%8C%E5%88%99%E4%BC%9A%E6%B6%89%E5%8F%8A%E5%88%B0%E4%BF%AE%E6%94%B9%E5%AF%86%E7%A0%81%202%E3%80%81%E5%BF%98%E8%AE%B0%E4%BA%86%E6%95%B0%E6%8D%AE%E5%BA%93%E7%99%BB%E5%BD%95%E5%AF%86%E7%A0%81%EF%BC%8C%E5%88%99%E4%BC%9A%E6%B6%89%E5%8F%8A%E5%88%B0%E4%BF%AE%E6%94%B9%E5%AF%86%E7%A0%81%202%202%E3%80%81%E4%BF%AE%E6%94%B9%E5%AF%86%E7%A0%81%E7%9A%84%E6%96%B9%E5%BC%8F,pg_hba.conf%20%EF%BC%8C%20%E6%8A%8A%E8%BF%9E%E6%8E%A5%E6%9D%83%E9%99%90%E8%AE%BE%E7%BD%AE%E7%9A%84%20md5%20%E5%8A%A0%E5%AF%86%E6%96%B9%E5%BC%8F%20%E6%94%B9%E6%88%90%20trust%20) 使用方法1可以
- 新增电脑入站规则 端口 5432
- [PostgreSQL - 允许远程访问的设置方法-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1932228) 
	- `D:\Database\Postgresql\pg_hba.conf`
	- `D:\Database\Postgresql\postgresql.conf`
	- **0.0.0.0/0   md5**  这个地址设置是可以的



```
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
host    all             all             0.0.0.0/0               md5
# IPv6 local connections:
host    all             all             ::1/128                 md5
# Allow replication connections from localhost, by a user with the
# replication privilege.
host    replication     all             127.0.0.1/32            md5
host    replication     all             ::1/128                 md5
```