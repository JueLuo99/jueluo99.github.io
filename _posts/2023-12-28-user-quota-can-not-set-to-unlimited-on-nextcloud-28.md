---
layout: post
title: 在 Nextcloud 28 上无法调整用户配额为“无限”的临时解决办法
date: 2023-12-28 23:23
category: Nextcloud
tags: [linux, nextcloud]
---

疑似为 Nextcloud 28.0.1 的 bug，等待官方修复或使用下面的解决方案

### 解决方案

1. 直接链接数据库，找到 Nextcloud 使用的数据库
1. 找到 `oc_preferences` 表
1. 根据 `userid` 字段，找到对应用户的记录
1. 将 `configkey` 字段为 `quota` 的记录的 `configvalue` 值改为 `none`

或者直接使用如下命令，记得修改命令中的 `username`
```sql
UPDATE nextcloud.oc_preferences
	SET configvalue='none'
	WHERE userid='username' AND appid='files' AND configkey='quota';
```


### 参考链接
1. https://github.com/nextcloud/server/issues/34961#issuecomment-1307234975