---
layout: post
title: Python 调用 `sys.clock()` 报错
date: 2021-04-27 08:18
category: Python
tags: [python] 
---

## 问题产生过程

在编码过程中，尝试统计程序运行时间，使用了 `sys.clock()`

运行时，解释器给出了如下错误：

```sh
AttributeError: module 'sys' has no attribute 'clock'
```

## 问题产生原因

自 Python 3.8 起，该方法已被正式移除

## 问题解决方法

改用 `time.perf_counter()` 即可

## 信息来源

官方文档：https://docs.python.org/3.7/library/time.html

> *Deprecated since version 3.3, will be removed in version 3.8:* The behaviour of this function depends on the platform: use [`perf_counter()`](https://docs.python.org/3.7/library/time.html#time.perf_counter) or [`process_time()`](https://docs.python.org/3.7/library/time.html#time.process_time) instead, depending on your requirements, to have a well defined behaviour.
