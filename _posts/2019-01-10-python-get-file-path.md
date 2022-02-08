---
layout: post
title: Python 判断当前运行的文件所在的位置
date: 2019-01-10 16:15
category: Python
tags: [python]
---

```
os.path.split(os.path.abspath(__file__))[0]
```

## 原理
```os.path.abspath(__file__)``` 获取当前运行的文件的绝对路径
```os.path.split(path)[0]``` 分割路径，元组的第一部分为路径，第二部分为文件名