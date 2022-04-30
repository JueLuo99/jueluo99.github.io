---
layout: post
title: 解决 Python 处理 json 时报错“Unexpected UTF-8 BOM”
date: 2020-03-10 17:18
category: Python
tags: [python, json]
---

### 出现错误

在使用 ```requests``` 库发送请求后，接收的返回值解析成 json 时出错

即执行

```python
result = session.post(url).json()
```

时，出现如下错误

```
json.decoder.JSONDecodeError: Unexpected UTF-8 BOM (decode using utf-8-sig)
```

### 原因分析

疑似返回的值内包含了一个 BOM 头


### 解决方法

导入 ```json``` 库

```python
import json
```

先使用该库配合处理返回的 json 后在对其进行操作

```python
result = result.text
    if result.startswith(u'\ufeff'):
        result = result.encode('utf8')[3:].decode('utf8')
    result = json.loads(result)
```