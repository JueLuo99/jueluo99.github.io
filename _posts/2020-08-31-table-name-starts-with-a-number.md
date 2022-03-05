---
layout: post
title: 表名是数字开头的，在 sql 语句中必须得用 [ ] 把表名括起来
date: 2020-08-31 09:46
category: SQL
tags: [sql, mysql, sqlite, postgresql, access]
---

例如如下语句：
```sql
SELECT '3DS' as 平台, [3DS].游戏名称, [3DS].通关日期, [3DS].游戏评分
FROM 3DS
WHERE (([3DS].游戏游玩状态)='愿望单') OR (([3DS].游戏游玩状态)='排队中');
```

若不带 ```[]``` 则会提示语法错误
