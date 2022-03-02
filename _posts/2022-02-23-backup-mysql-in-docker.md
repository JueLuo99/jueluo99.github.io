---
layout: post
title: 备份 Docker 中的 MySQL 数据库
date: 2022-02-23 23:24
category: Docker
tags: [mysql, docker, mariadb]
---

备份全部数据库

```bash
$ docker exec some-mysql-docker sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > /some/path/on/your/host/all-databases.sql
```

备份指定的某个数据库
```bash
$ docker exec some-mysql-docker sh -c 'exec mysqldump --databases db_name -uroot -p"$MYSQL_ROOT_PASSWORD"' > /some/path/on/your/host/db1.sql
```