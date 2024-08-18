---
layout: post
title: JavaScript setTimeout 不工作
date: 2024-08-18 17:37
category: JavaScript
tags: [javascript, tampermonkey]
---

帮朋友写了一个 Tampermonkey 脚本，用于爬取一个多页的表格，其中有一个小功能需要翻页后等待几秒以确保数据加载完成。

但是发现这玩意儿中的 `setTimeout()`  函数并没有按照我想象中的等待一定时间后再执行下一行代码。


### 原因分析

> 原因是 setTimeout() 作为同步代码执行，并且对 setTimeout() 的多次调用均同时运行。每次调用 setTimeout() 都会创建异步代码，该代码将在给定延迟后稍后执行。
> 就其本身而言，`setTimeout()` 不能用作 `sleep()` 函数，但是你可以使用 `async` 和 `await` 创建自定义JavaScript `sleep()` 函数。


### 解决方案

结合 `Promises` 、 `async` 和 `await` 编写一个 `sleep()` 函数，然后从 `async` 函数中调用它，并且需要与 `await` 关键字一起使用。

```javascript
const sleep = (delay) => new Promise((resolve) => setTimeout(resolve, delay))

const repeatedGreetings = async () => {
  await sleep(1000)
  console.log(1)
  await sleep(1000)
  console.log(2)
  await sleep(1000)
  console.log(3)
}

repeatedGreetings()
```


### 参考资料

1. [如何使JavaScript休眠或等待 - 程序员张张 - SegmentFault 思否](https://segmentfault.com/a/1190000023490085)