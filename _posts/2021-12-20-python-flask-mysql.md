---
layout: post
title: 在 flask 中使用 flask-mysql 连接数据库
date: 2021-12-20 13:04
category: Python
tags: [python, flask, mysql]
---

最初尝试了 `pymysql` + `flask` 的方式连接数据库，但是发现会出现超时等各种问题，经 [Stack Overflow 的一个帖子](https://stackoverflow.com/questions/9845102/using-mysql-in-flask)提示，可以使用 `flask-mysql` 来更方便地连接数据库


## 项目地址

GitHub：https://github.com/cyberdelia/flask-mysql
官方文档：https://flask-mysql.readthedocs.io/en/latest/

## 安装

```shell
pip install flask-mysql
```

## 使用示例

```python
from flask import Flask
from flaskext.mysql import MySQL

app = Flask(__name__)
mysql = MySQL()
app.config['MYSQL_DATABASE_USER'] = 'root'
app.config['MYSQL_DATABASE_PASSWORD'] = 'root'
app.config['MYSQL_DATABASE_DB'] = 'EmpData'
app.config['MYSQL_DATABASE_HOST'] = 'localhost'
mysql.init_app(app)

conn = mysql.connect()

@app.route('/')
def foo():
    with conn.cursor() as cursor:
        cursor.execute('SELECT * FROM employees')
        return str(cursor.fetchall())
```
