---
up: 
related: 
created: 2024-03-08
tags:
  - tools/sop
---


[0成本3分钟做一个不限速+全平台+自动同步超级网盘！\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV18u411d7tv/?spm_id_from=333.999.0.0&vd_source=6d4ef5f8b8b73d69ea854cb9321a50ac)

```yaml
services:
  db:
    image: mariadb:10.11
    container_name: seafile-mysql
    environment:
      - MYSQL_ROOT_PASSWORD=14309123  # Requested, set the root's password of MySQL service.
      - MYSQL_LOG_CONSOLE=true
      - MARIADB_AUTO_UPGRADE=1
    volumes:
      - /home/seafile-mysql/db:/var/lib/mysql  # Requested, specifies the path to MySQL data persistent store.
    networks:
      - seafile-net

  memcached:
    image: memcached:1.6.18
    container_name: seafile-memcached
    entrypoint: memcached -m 256
    networks:
      - seafile-net
          
  seafile:
    image: seafileltd/seafile-mc:latest
    container_name: seafile
    ports:
      - "81:80"
#     - "4433:443"  # If https is enabled, cancel the comment.
    volumes:
      - /home/seafile-data:/shared   # Requested, specifies the path to Seafile data persistent store.
    environment:
      - DB_HOST=db
      - DB_ROOT_PASSWD=14309123  # Requested, the value should be root's password of MySQL service.
      - TIME_ZONE=Asia/Shanghai  # Optional, default is UTC. Should be uncomment and set to your local time zone.
      - SEAFILE_ADMIN_EMAIL=aptx4869yuyang2017@gmail.com # Specifies Seafile admin user, default is 'me@example.com'.
      - SEAFILE_ADMIN_PASSWORD=14309123     # Specifies Seafile admin password, default is 'asecret'.
#      - SEAFILE_SERVER_LETSENCRYPT=false   # Whether to use https or not.
#      - SEAFILE_SERVER_HOSTNAME=docs.seafile.com # Specifies your host name if https is enabled.
    depends_on:
      - db
      - memcached
    networks:
      - seafile-net

networks:
  seafile-net:
```